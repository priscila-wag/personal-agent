---
name: draft-meeting-minutes
description: "Draft structured meeting minutes from Zoom transcript, calendar event, or verbal description. Posts to #prw-personal-agents and saves to Context/Meeting Notes/."
---

# Draft Meeting Minutes

Produce clean, structured meeting minutes from whatever source is available — Zoom transcript, calendar context, or a description of what happened. Save locally and post to #prw-personal-agents for review.

**Channel ID:** `C0AM6E2D4R2`

---

## Instructions

### Step 1 — Identify the meeting

From the request, extract:
- Meeting name (or infer from context)
- Date (default to today if not specified)
- Attendees (from calendar or request)

Then check for source material in priority order:

**1. Zoom transcript** — call `mcp__9edf655b-9ecb-4911-aa24-26584c7014e0__search_meetings` with `from` set to 3 days ago in ISO 8601 UTC, `to` set to now, and `page_size: 5`. If the meeting name is known, pass it as `q` to narrow results. Find the matching meeting by `topic`. If found, call `mcp__9edf655b-9ecb-4911-aa24-26584c7014e0__get_meeting_assets` with the `meeting_uuid`, then call `mcp__9edf655b-9ecb-4911-aa24-26584c7014e0__get_recording_resource` with `meetingId` set to the `meeting_uuid` and `types: "transcript,summary"`.

**2. Existing meeting note** — scan `Context/Meeting Notes/` for a file matching the meeting name or date.

**3. Calendar event** — call `list_events` for the meeting date. Extract: title, attendees, description, any attached pre-reads.

**4. Verbal description** — if the user described what happened in their request, use that as the source.

Note which source(s) were used at the top of the draft.

---

### Step 2 — Draft the minutes

```markdown
# [Meeting Name]
*[YYYY-MM-DD] | [Duration if known] | [Attendees — first names or @handles]*
*Source: [Zoom transcript / calendar / verbal description]*

## Purpose
[1 sentence — what this meeting was for. Not a list of topics. What was the intent?]

## Decisions
- [Decision — what was locked in, and who made the call if attributable]
- [Each decision is a closed question — something that was open before the meeting and is now resolved]
- *(None made — discussion/update meeting)* if applicable

## Action Items
| # | Task | Owner | Due | Jira? |
|---|------|-------|-----|-------|
| 1 | [concrete next step] | [Name] | [date or —] | [ticket or —] |

## Key Discussion Points
- [Substantive points raised — the "so what" of each topic, not a transcript summary]
- [Include: options considered, tradeoffs discussed, context shared that affects future decisions]
- [3–7 bullets max. If it doesn't affect a decision or action, leave it out]

## Open Questions & Parking Lot
- [Unresolved questions — what's still open and who owns following up]
- [Topics deferred to a future meeting]

## Context
- [Background or framing that's useful for future reference — max 3 bullets]
- [Links, references, or docs mentioned in the meeting]
```

**Formatting rules:**
- Lead with decisions and actions — that's what people need
- Key discussion points: synthesise, don't transcribe
- Attribute ownership for actions — "Pri to follow up" not "follow up needed"
- Use [[wiki-links]] for Obsidian: people names, Jira keys, key concepts

---

### Step 3 — Save to Context/Meeting Notes/

Filename: `YYYY-MM-DD - [Meeting Name].md`

Add YAML frontmatter:
```yaml
---
title: [Meeting Name]
description: "[~150 chars — key decisions or outcomes]"
type: meeting-note
created_date: [YYYY-MM-DD]
---
```

---

### Step 4 — Post to #prw-personal-agents

Call `slack_send_message` with channel `C0AM6E2D4R2`:

```
*📋 Meeting minutes drafted — [Meeting Name] ([date])*
Saved to: Context/Meeting Notes/[filename]

*Decisions:* [count or "none"]
*Action items:* [count] — [list owners]
*Open questions:* [count]

[If action items exist, list them as bullets for quick scanning]

Review and confirm, or reply with edits.
```

---

### Step 5 — Create Jira tickets for action items (if requested)

If the user says "create tickets" or "add to Jira" after reviewing:

For each action item without an existing ticket:
- Call `createJiraIssue` with project HELP, type Task
- Summary: the action item text (imperative: "Fix X", "Review Y")
- Assignee: look up with `lookupJiraAccountId` if needed
- Description: meeting name, date, 1-sentence context

Update the minutes file: replace the Jira? column with the created ticket key.

---

## Edge cases

- **No transcript, no calendar, no description**: ask — *"What meeting are these minutes for? Give me the date, attendees, and a quick summary of what happened."*
- **Transcript too long**: summarise by section — don't try to include everything. Signal over noise.
- **Standup or < 5 min meeting**: keep to Purpose + Action Items only. Skip Key Discussion Points.
- **1:1 meeting**: after saving minutes, check `Context/121s/[Person Name].md` and append a session log entry: date, 1-line summary, open loops.
- **Recurring meeting**: check `Context/Meeting Notes/` for previous notes from the same meeting. Note any standing open questions that carry forward.
