---
name: meeting-digest
description: "Digest all work meetings from a given day — uses Google Calendar as source of truth and Zoom AI Companion notes as content. Extracts decisions, action items, and blockers, writes structured notes to Context/Meeting Notes/."
---

# Meeting Digest

Fetch all work meetings for a target day, read the Zoom AI Companion notes for each, produce a structured digest, and save it locally. The target day defaults to today; pass "yesterday" to process the prior day.

## Configuration

Read `Context/agent-config.md` at the start. Use:
- `timezone` — for all date calculations (e.g. `Australia/Sydney`)
- `base_directory` — for file path construction and idempotency check
- `personal_channel_id` — for Slack error alerts
- `calendar_exclusions` — list of meeting title patterns to skip

Read the G&I Goals file (path in agent-config) for the epic matching table used in Step 4.

---

## Instructions

Run all steps in sequence. Do not ask for confirmation between steps unless explicitly told to pause.

---

### Step 1 — Fetch all undigested meetings for the target day

**This step uses Google Calendar as the source of truth and Zoom AI Companion notes as content. Do NOT use `search_meetings` or `get_meeting_assets` — those tools cannot reliably identify specific past occurrences of recurring meetings.**

#### Phase A — Calendar: get the meeting list

1. Compute the target date in the user's timezone (from `Context/agent-config.md`). Default = today; if the user passed "yesterday", subtract one day.

2. Call `mcp__4cf876bf-4b8b-4c42-896f-3db6ae3e2298__list_events` with:
   - `startTime` = start of target date in local timezone (ISO 8601 with offset, e.g. `2026-05-18T00:00:00+10:00`)
   - `endTime` = end of target date in local timezone (e.g. `2026-05-18T23:59:59+10:00`)
   - `timeZone` = user's timezone (e.g. `Australia/Sydney`)
   - `orderBy` = `startTime`

3. **Filter to work meetings only.** Remove any event where:
   - `summary` matches a pattern in `calendar_exclusions` from `Context/agent-config.md`
   - `eventType` is `focusTime` or `workingLocation`
   - `attendees` list is empty or contains only the user (solo blocks)
   - Event has no attendees field at all and is clearly a personal block

4. **Sort chronologically** (oldest first). This is the ordered list of meetings to process.

#### Phase B — Zoom: fetch all AI Companion notes for the day

1. Convert the target date to a UTC range:
   - `from` = start of target date in local time → UTC (e.g. AEST 00:00 = previous day 14:00 UTC)
   - `to` = end of target date in local time → UTC (e.g. AEST 23:59 = same day 13:59 UTC)

2. Call `mcp__9edf655b-9ecb-4911-aa24-26584c7014e0__search_zoom` with:
   ```
   search_entities: [{ "entity_type": "zoom_doc", "filters": { "doc_view": "notes", "from": "<UTC start>", "to": "<UTC end>" } }]
   page_size: 50
   ```
   This returns all Zoom AI Companion note documents created during that day. Each result includes `title`, `file_id`, `create_time`, and `modify_time`.

3. **Error handling** — if the call fails or returns an error:
   - Post a Slack alert: call `mcp__0deb4b0b-cc05-4ae4-8e5e-08d6c09985dd__slack_send_message` with:
     - `channel_id`: use `personal_channel_id` from `Context/agent-config.md`
     - `message`: `⚠️ *Meeting digest blocked — Zoom error*\n\n[error message]. Check the Zoom for Claude connector in Claude settings.`
   - Then stop.

#### Phase C — Match calendar events to Zoom notes

For each calendar event from Phase A, find the matching Zoom doc from Phase B:

1. **Title match**: The zoom_doc `title` typically starts with the calendar event `summary` followed by the date/time (e.g. `"HCF Planning 2026-05-18 10:17(GMT+10:00)"`). Match on the leading words of the title.
2. **Time match (fallback)**: If the title match is ambiguous, check that `zoom_doc.create_time` falls within the calendar event's `start` → `end` window (±30 min tolerance).
3. **No match**: If no zoom_doc corresponds to a calendar event, mark it as `"no Zoom notes available"` and skip it — do not attempt to fetch from any other source.

#### Phase D — Idempotency check

Before reading content for any meeting:

1. First (once, before the loop): run `git -C [base_directory] pull --ff-only` to sync the working directory.
2. Derive the expected notes filename: `YYYY-MM-DD - [Meeting Name].md` using the calendar event `summary` (same format as Step 5).
3. Check if a file with that name already exists: `ls "[base_directory]/Context/Meeting Notes/" | grep "[filename]"`
4. If it exists → skip this meeting. Output: *"Notes already exist for [meeting name] — skipping."*
5. If it does NOT exist → proceed to Phase E.

#### Phase E — Read Zoom note content

For each undigested meeting that has a matched zoom_doc:

Call `mcp__9edf655b-9ecb-4911-aa24-26584c7014e0__get_file_content` with the `file_id` from the matched zoom_doc. This returns the full AI Companion note in Markdown.

If the content is empty or only whitespace → mark as `"no content available"` and skip.

#### Phase F — Report

After processing all meetings, report:
- How many were digested
- How many were skipped (with reason: already exists / no Zoom notes / no content)

---

### Step 2 — Read context

Before processing any note content, read:
- `GOALS.md` — to understand active projects and know which Jira epics exist
- `Context/Memory/pri-brain.md` — to understand how Pri thinks, her vocabulary, and what she considers a decision vs. a discussion
- `Context/Memory/Reference/jira-epic-map.md` — epic matching reference (if it exists)

---

### Step 3 — Analyse the note content

For each meeting with content, extract four things:

**A. Summary**
2–3 sentences. Signal-first: what was the meeting about and what was the key outcome or shift. Not a list of topics covered — a single coherent outcome statement. Use Pri's voice: direct, no effort framing, leads with result.

**B. Decisions**
Explicit commitments that changed direction, locked something in, or closed an open question. Only real decisions — not suggestions, not maybes. Format: what was decided, and who made the call (if attributable).

**C. Action items**
Concrete next steps with a named owner. Apply this logic per item:
- If the note names a specific person as the driver with high confidence → assign to them
- If ownership is ambiguous or shared → assign to Pri (priscila.wagner@canva.com)
- For each item, suggest the best Jira epic match using the logic in Step 4
- Note the suggested due date if mentioned in the meeting, otherwise leave blank

**D. Open questions / blockers**
Unresolved questions, blockers raised, or topics parked for a future meeting. These do NOT become Jira tickets — they go in the notes file only.

---

### Step 4 — Match action items to Jira epics

For each action item, determine the best Jira epic by reading the meeting context against `GOALS.md` and the milestone hierarchy in the G&I Goals file (path in `Context/agent-config.md`).

Use the goal routing rules from that file to match action items to UVSG goals or HELP epics. When nothing clearly matches, use the miscellaneous epic (typically the catch-all epic listed in the G&I Goals file) as the default fallback.

State your epic suggestion in the review output. The user will confirm or override before tickets are created.

---

### Step 5 — Write the meeting notes file

Save the digest to `Context/Meeting Notes/` using this filename format:
`YYYY-MM-DD - [Meeting Name].md`

Use the calendar event `summary` as the meeting name (not the Zoom doc title, which may include timestamps or "Google Calendar Meeting (not synced)").

**File format:**

```markdown
# [Meeting Name]
*[YYYY-MM-DD] | [Duration if available] | [Attendees from calendar if available]*

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

### Step 10 — SKIP

Meeting notes contain personal data and are never pushed to GitHub. Skip this step entirely and proceed to Step 11.

---

### Step 11 — Show summary in chat

After saving notes locally, display a compact summary in chat:

```
📝 **Meeting digest complete — [Meeting Name] ([YYYY-MM-DD])**

**Decisions:** [count] | **Action items:** [count]

[Action items as bullets: • [task] → [owner] [KEY-XXX]]

Notes saved to `Context/Meeting Notes/[filename].md`
```

If there are no action items: `📝 [Meeting Name] digested — no action items.`

Do NOT call `slack_send_message` unless Pri explicitly asks to post to Slack.

---

## Edge cases

- **No decisions found**: Write "No decisions made — discussion/update meeting." Do not invent decisions.
- **No action items found**: Write "No action items." Do not create Jira tickets.
- **Meeting is a standup or <5 min**: Still run the digest, but keep the summary to 1 sentence and skip Jira ticket creation unless action items are explicitly present.
- **Zoom doc title is "Google Calendar Meeting (not synced)"**: The meeting was held via a room system. Match it to the calendar event by `create_time` falling within the event's time window. Use the calendar event `summary` as the meeting name in the notes file.
- **Multiple zoom_docs match the same calendar event**: Use the one whose `create_time` is closest to the event's start time.
- **No zoom_doc found for a calendar event**: Note it as skipped — "no Zoom AI notes for [meeting name]". Do not attempt `search_meetings` or `get_meeting_assets` as a fallback.
- **Person not found in Jira**: Flag the item: "Couldn't find [name] in Jira — assigning to Pri by default. Confirm?"
