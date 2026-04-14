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

1. Call `mcp__zoom-notes__list_notes` with `limit: 10` and `from` set to 5 days ago (YYYY-MM-DD format).
2. Identify the **most recent** note by date. If there are multiple meetings on the same day, pick the one that started latest.
3. **Idempotency check** — before fetching the transcript, derive the expected notes filename: `YYYY-MM-DD - [Meeting Name].md` (same format as Step 5). Check if a file with that name already exists in `Context/Meeting Notes/`. If it does, stop immediately and output: *"Notes already exist for [meeting name] ([date]) — skipping to avoid duplicates."* Do not fetch the transcript, do not create Jira tickets.
4. Call `mcp__zoom-notes__fetch_transcript` with the exact note name returned.
5. If no transcript content is available (meeting too recent, recording not yet processed), tell the user: *"Transcript not ready yet — Zoom usually takes 5–10 min after the meeting ends. Run `/meeting-digest` again shortly."* Then stop.

---

### Step 2 — Read context

Before processing the transcript, read:
- `GOALS.md` — to understand active projects and know which Jira epics exist
- `Context/Memory/pri-brain.md` — to understand how Pri thinks, her vocabulary, and what she considers a decision vs. a discussion
- `Context/Memory/Reference/jira-epic-map.md` — epic matching reference (if it exists)

---

### Step 3 — Analyse the transcript

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

### Step 6 — Deduplicate against Jira

Before presenting anything to Pri, check each action item against existing Jira issues to avoid creating duplicates.

For each action item:

1. **Search by keywords across both projects** — extract 2–4 key terms from the task description and run two queries in parallel:
   ```
   searchJiraIssuesUsingJql: project = HELP AND summary ~ "[keyword]" AND statusCategory != Done ORDER BY updated DESC
   searchJiraIssuesUsingJql: project = UVSG AND summary ~ "[keyword]" AND statusCategory != Done ORDER BY updated DESC
   ```
   Always search both HELP and UVSG. UV goals live in UVSG; task-level work lives in HELP. Missing the UVSG search will miss official goals entirely.

2. **Search within the target epic** — run a second query scoped to the matched epic:
   ```
   searchJiraIssuesUsingJql: "Epic Link" = [epic-key] AND statusCategory != Done ORDER BY updated DESC
   ```
   If the action item mentions a mobile/UV goal, also check `project = UVSG AND issuetype = "Team Goal"` for matches.

3. **Classify each action item** into one of three outcomes:

   | Outcome | When to use | What to do |
   |---|---|---|
   | **CREATE** | No matching issue found, or existing issues are clearly different in scope | Will create a new Jira ticket |
   | **LINK** | An existing open issue covers this action item — same intent, same scope | No new ticket; note the existing issue number |
   | **OVERLAP** | An existing issue is related but not identical — partial match | Flag for Pri to decide: add a comment to existing, or create a sub-task |

4. Note the confidence level for LINK/OVERLAP matches: **high** (title clearly matches) or **low** (loose keyword match only).

---

### Step 7 — Review action items with Pri

Display a single consolidated table combining action items, dedup findings, and recommendations. Say:

> **Action items checked against Jira — review before I create tickets:**
>
> [table]
>
> **Legend:** ✅ CREATE — no duplicate found &nbsp;|&nbsp; 🔗 LINK — existing issue covers this &nbsp;|&nbsp; ⚠️ OVERLAP — related issue exists, your call
>
> Say **"create"** to action all ✅ rows, **"skip [#]"** to drop an item, **"edit [#]"** to change a row, or **"link [#]"** to confirm a 🔗 match instead of creating.

**Table format:**

| # | Task | Owner | Epic | Due | Jira match | Rec |
|---|------|-------|------|-----|------------|-----|
| 1 | Create HELP-4139 milestones | Pri | HELP-4139 | Today | — | ✅ CREATE |
| 2 | Schedule team walkthrough | Pri | HELP-4139 | Today | HELP-4XXX: "Mobile UX team sync" (open) | ⚠️ OVERLAP |
| 3 | Share Figma audit design with Kunday | Pri | HELP-4139 | Today | — | ✅ CREATE |

Wait for Pri's response before proceeding.

---

### Step 8 — Create or link Jira tickets

Process each confirmed row based on its outcome:

**For ✅ CREATE rows:**
1. Call `mcp__3b804fcf-2cd6-468f-999d-75e72c3392d3__createJiraIssue` with:
   - **project**: HELP (or UVSG if the epic is a UVSG goal)
   - **summary**: the action item text (concise, imperative: "Fix prompts review for logged-out HA")
   - **issue type**: Task
   - **assignee**: the confirmed owner's Jira account ID (look up with `lookupJiraAccountId` if needed)
   - **description**: include the meeting name, date, and the context sentence from the transcript
   - **parent/epic link**: the confirmed epic key

**For 🔗 LINK rows (confirmed by Pri):**
1. Call `mcp__3b804fcf-2cd6-468f-999d-75e72c3392d3__addCommentToJiraIssue` on the matched issue with:
   - *"Raised in [Meeting Name] on [date]: [1-sentence context from transcript]"*
2. No new ticket created.

**For ⚠️ OVERLAP rows — follow Pri's instruction:**
- "add comment" → treat as 🔗 LINK above
- "create sub-task" → create a child task under the matched issue instead of a standalone ticket

After all rows are processed, output a summary:

> **Jira update complete:**
> - ✅ HELP-XXXX created: [task] → @[owner]
> - 🔗 HELP-XXXX commented: [existing issue title]
>
> Meeting notes file updated with ticket numbers.

Update the meeting notes file: replace each action item's Epic column with the actual Jira issue number (created or linked).

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

## Edge cases

- **No decisions found**: Write "No decisions made — discussion/update meeting." Do not invent decisions.
- **No action items found**: Write "No action items." Do not create Jira tickets.
- **Transcript is a standup or <5 min**: Still run the digest, but keep the summary to 1 sentence and skip Jira ticket creation unless action items are explicitly present.
- **Multiple meetings today**: List the top 3 by recency and ask: *"I found [N] meetings today — I fetched the most recent ([name]). Is that the right one, or should I use a different one?"*
- **Person not found in Jira**: Flag the item: "Couldn't find [name] in Jira — assigning to Pri by default. Confirm?"
