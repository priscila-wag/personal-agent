---
name: meeting-digest
description: "Fetch the most recent Zoom meeting, extract decisions and action items, deduplicate against existing Jira issues, write a structured note to Context/Meeting Notes/, and create or update Jira tickets after Pri reviews them."
---

# Meeting Digest

Automatically fetch the latest Zoom meeting, produce a structured digest, save it locally, check each action item against existing Jira issues to avoid duplicates, and create or update tickets only after Pri reviews the recommendations.

---

## Instructions

Run all steps in sequence. Do not ask for confirmation between steps unless explicitly told to pause.

---

### Step 1 — Fetch the most recent Zoom meeting

1. Call `mcp__9edf655b-9ecb-4911-aa24-26584c7014e0__search_meetings` with `from` set to 5 days ago in ISO 8601 UTC (e.g. `2026-04-15T00:00:00Z`), `to` set to now, and `page_size: 10`. Pri's timezone is `Australia/Sydney` (AEST UTC+10 / AEDT UTC+11) — convert accordingly when computing the date range.
2. **Error handling** — if the call fails or returns an error:
   - Post a Slack alert: call `mcp__0deb4b0b-cc05-4ae4-8e5e-08d6c09985dd__slack_send_message` with:
     - `channel_id`: `C0AM6E2D4R2`
     - `message`: `⚠️ *Meeting digest blocked — Zoom error*\n\n[error message]. Check the Zoom for Claude connector in Claude settings.`
   - Then stop.
3. Identify the **most recent** meeting by `schedule_start_time`. If there are multiple on the same day, pick the one with the latest start time.
4. **Idempotency check** — before fetching the transcript:
   - First, run `git -C /Users/priscila/Documents/Agents/personal-agent-main pull --ff-only` to ensure the working directory reflects any notes written by previous scheduled runs.
   - Derive the expected notes filename: `YYYY-MM-DD - [Meeting Name].md` using the meeting's `topic` field (same format as Step 5).
   - Check if a file with that name already exists in `Context/Meeting Notes/` using the Bash tool: `ls "/Users/priscila/Documents/Agents/personal-agent-main/Context/Meeting Notes/" | grep "[filename]"`.
   - If it exists, stop immediately and output: *"Notes already exist for [meeting name] ([date]) — skipping to avoid duplicates."* Do not fetch the transcript.
   - Also check git log: `git -C /Users/priscila/Documents/Agents/personal-agent-main log --oneline -10 | grep "[Meeting Name]"` as a secondary check in case the file was written but not visible.
5. Using the `meeting_uuid` from the search result:
   - **a.** Call `mcp__9edf655b-9ecb-4911-aa24-26584c7014e0__get_meeting_assets` with `meetingId` set to the `meeting_uuid`. This returns the Zoom AI summary, my notes, recording status, and participant list.
   - **b.** If a recording exists and `processing` is not `true`, call `mcp__9edf655b-9ecb-4911-aa24-26584c7014e0__get_recording_resource` with `meetingId` set to the `meeting_uuid` and `types: "transcript,summary,nextStep"`. This returns the full transcript, Zoom's AI-generated summary, and auto-extracted next steps.
6. If no transcript content is available (`recording` is `null`, `processing: true`, or `get_recording_resource` returns no transcripts), tell the user: *"Transcript not ready yet — Zoom usually takes 5–10 min after the meeting ends. Run `/meeting-digest` again shortly."* Then stop.

---

### Step 2 — Read context

Before processing the transcript, read:
- `GOALS.md` — to understand active projects and know which Jira epics exist
- `Context/Memory/pri-brain.md` — to understand how Pri thinks, her vocabulary, and what she considers a decision vs. a discussion
- `Context/Memory/Reference/jira-epic-map.md` — epic matching reference (if it exists)

---

### Step 3 — Analyse the transcript

**Additional signal:** If `get_recording_resource` returned `summaries` or `next_steps` arrays (Zoom's AI-generated content), use them as supplementary cross-checks — but do not copy them verbatim. Your job is to extract meaning through Pri's lens, not relay Zoom's output.

Extract four things from the transcript:

**A. Summary**
2–3 sentences. Signal-first: what was the meeting about and what was the key outcome or shift. Not a list of topics covered — a single coherent outcome statement. Use Pri's voice: direct, no effort framing, leads with result.

**B. Decisions**
Explicit commitments that changed direction, locked something in, or closed an open question. Only real decisions — not suggestions, not maybes. Format: what was decided, and who made the call (if attributable).

**C. Action items**
Concrete next steps with a named owner. Apply this logic per item:
- If the transcript names a specific person as the driver with high confidence → assign to them
- If ownership is ambiguous or shared → assign to Pri (priscila.wagner@canva.com)
- For each item, suggest the best Jira epic match using the logic in Step 4
- Note the suggested due date if mentioned in the meeting, otherwise leave blank

**D. Open questions / blockers**
Unresolved questions, blockers raised, or topics parked for a future meeting. These do NOT become Jira tickets — they go in the notes file only.

---

### Step 4 — Match action items to Jira epics

For each action item, determine the best Jira epic by reading the meeting context against `GOALS.md`. Use this matching logic:

| If the action item is about... | Suggest this epic |
|---|---|
| AI Help Center, HA, logged-in sessions, UVSG-614 | UVSG-614 |
| Integrated AI HC + Assistant, split panel, AI chat, UVSG-615 | UVSG-615 |
| Logged-out HA, login incentive, TIMDL | HELP-4319 |
| No-reply email help access | HELP-4340 |
| Canva AI Help + ChatGPT MCP | HELP-3785 |
| Mobile help experience, mobile UX, mobile audit | HELP-4139 |
| LLM readability, article structure for AI | HELP-3222 |
| CMS integration, in-context tutorials, Design School | HELP-3820 |
| Content pipeline, Contentful, publishing automation | Use HELP-3090 |
| Affinity, China, global/local HC | Use HELP-3090 |
| Anything else, unclear, or cross-cutting | Use HELP-3090 (default fallback) |

State your epic suggestion in the review output. Pri will confirm or override before tickets are created.

---

### Step 5 — Write the meeting notes file

Save the digest to `Context/Meeting Notes/` using this filename format:
`YYYY-MM-DD - [Meeting Name].md`

Use the meeting name from the Zoom note title. Strip any Zoom-generated suffixes (e.g. "Zoom Meeting" or long IDs).

**File format:**

```markdown
# [Meeting Name]
*[YYYY-MM-DD] | [Duration if available] | [Attendees if available]*

## Summary
[2–3 sentence signal-first summary. What happened and what changed.]

## Decisions
- [Decision 1 — who made it if known]
- [Decision 2]

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | [Task description] | [Name / Pri] | [HELP-XXXX or UVSG-XXX] | [Date or —] |
| 2 | ... | ... | ... | ... |

## Open Questions & Blockers
- [Question or blocker — what's unresolved and why it matters]

## Context
[Any background, links, or framing from the meeting that's useful for future reference. Keep to 3–5 bullets max.]
```

**Before saving**, add `[[wiki-links]]` to the note for Obsidian graph connectivity:
- All people mentioned by name → `[[Name]]`
- All Jira ticket keys (HELP-XXXX, UVSG-XXXX) → `[[HELP-XXXX]]`
- Key concepts and themes: `[[logged-out HA]]`, `[[half-sheet]]`, `[[HC AI mode]]`, `[[Mobile Help UX]]`, `[[AI-First Help Center]]`, `[[Content Automation]]`, `[[HCF]]`
- Only link meaningful mentions — not every word, not inside code blocks or URLs

Confirm to the user: *"Meeting notes saved to Context/Meeting Notes/[filename].md"*

---

### Step 6 — SKIP

Jira deduplication is disabled. Skip this step entirely and proceed to Step 7.

---

### Step 7 — SKIP

Jira review table is disabled. Skip this step entirely and proceed to Step 8.

---

### Step 8 — SKIP

Jira ticket creation is disabled. Skip this step entirely and proceed to Step 9.

---

### Step 9 — Compound on touch

After saving:
1. Check if any decision or blocker from this meeting relates to an open task in `Tasks/` — if so, note it inline.
2. If a blocker was raised that already exists in `GOALS.md` as a known blocker, flag it: *"This blocker ([name]) was also raised in [previous context]. Consider whether it's systemic."*
3. If the meeting is a recurring 1:1 with a named person who has a doc in `Context/121s/`, append a session log entry to their doc: date, 1-line summary, any open loops added.

---

### Step 10 — Push to GitHub

After all notes and Jira updates are complete, commit and push the meeting notes file to the remote repo so it's available to other agents and automations.

Run these commands from the repo root (`/Users/priscila/Documents/Agents/personal-agent-main`):

```bash
cd /Users/priscila/Documents/Agents/personal-agent-main
git add "Context/Meeting Notes/"
git commit -m "meeting digest: [Meeting Name] ([YYYY-MM-DD])"
git push
```

Replace `[Meeting Name]` and `[YYYY-MM-DD]` with the actual meeting title and date.

**If the push succeeds:** confirm quietly — *"Pushed to GitHub."*

**If the push fails** (no remote, auth error, network issue): warn without blocking — *"Note: couldn't push to GitHub ([error]). Notes saved locally — push manually when ready."* Do not retry or hang.

---

### Step 11 — Post summary to Slack

After GitHub push (or failure), post a compact summary to `#prw-personal-agents` (`C0AM6E2D4R2`).

Call `slack_send_message` with:
- `channel_id`: `C0AM6E2D4R2`
- `message`:

```
*📝 Meeting digest complete — [Meeting Name] ([YYYY-MM-DD])*

*Decisions:* [count] | *Action items:* [count] | *Jira tickets:* [count created] / [count linked]

[List action items as bullets: • [task] → [owner] [[KEY-XXX]](https://canva.atlassian.net/browse/KEY-XXX)]

_Notes saved to `Context/Meeting Notes/[filename].md`_
```

If there are no action items, post a 1-liner: `*📝 [Meeting Name] digested — no action items.*`

If the Slack post fails, log and continue — do not block.

---

## Edge cases

- **No decisions found**: Write "No decisions made — discussion/update meeting." Do not invent decisions.
- **No action items found**: Write "No action items." Do not create Jira tickets.
- **Transcript is a standup or <5 min**: Still run the digest, but keep the summary to 1 sentence and skip Jira ticket creation unless action items are explicitly present.
- **Multiple meetings today**: List the top 3 by recency and ask: *"I found [N] meetings today — I fetched the most recent ([name]). Is that the right one, or should I use a different one?"*
- **Person not found in Jira**: Flag the item: "Couldn't find [name] in Jira — assigning to Pri by default. Confirm?"
