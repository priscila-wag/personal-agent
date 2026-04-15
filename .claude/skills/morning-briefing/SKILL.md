---
name: morning-briefing
description: "Automated daily brief — pulls calendar, Jira, and Slack overnight signals, picks 3 focus items, and posts a compact briefing to #prw-personal-agents. Runs unattended at 8:30am Mon–Fri via launchd."
---

# Morning Briefing

Pull today's signals from all connected tools, synthesise into a compact brief, and post to Slack. No interaction required — this runs unattended.

This is NOT `/today`. It does not do deep 1:1 prep, does not update the weekly scratchpad, and does not ask for confirmation. It is a read-only morning snapshot, delivered to Slack.

---

## Instructions

Run all steps in sequence. If a tool is unavailable or returns an error, skip that section gracefully — post what's available and note what was skipped.

---

### Step 1 — Get today's context

Compute today's date and yesterday's date. Sydney timezone (Australia/Sydney).

**Calendar** — call `list_events` for today (midnight → 11:59pm Sydney time):
- Extract: meeting title, time, duration, attendees
- Flag: 1:1s (2 attendees or title contains "1:1", "121", "catch up", person name only)
- Flag: back-to-back stretches (< 15 min between meetings)
- Flag: any deep work blocks or focus time events

**Jira** — run these three queries in parallel:
```
searchJiraIssuesUsingJql: assignee = currentUser() AND status = "In Progress" ORDER BY updated DESC
searchJiraIssuesUsingJql: assignee = currentUser() AND due <= now() AND statusCategory != Done ORDER BY due ASC
searchJiraIssuesUsingJql: assignee = currentUser() AND due = today() AND statusCategory != Done ORDER BY priority DESC
```
Deduplicate across the three result sets by issue key. Max 8 issues total.

**Slack** — search for overnight messages (since 6pm yesterday) in priority channels:
```
slack_search_public_and_private: in:#hcf-team after:yesterday
slack_search_public_and_private: to:me after:yesterday
slack_search_public_and_private: in:C0A0JA960SV after:yesterday
```
Extract: any questions directed at Pri, any decisions made without her, any blockers raised. Ignore automated bot messages and FYI broadcasts unless they name Pri.

**Draft request detection** — while scanning Slack results, flag any message that mentions Pri (`<@U0701AR9B35>`) and matches any of these patterns:

| Pattern | Draft type | Example trigger |
|---------|-----------|-----------------|
| "update", "JIRA", "goal", "GA", "align", "deadline", "by [day]" + goal/UVSG context | `goal_update` | Eve asking goal owners to update Jira |
| "PRD", "product brief", "write up", "kickoff doc", "requirements" | `prd` | Andi asking for a PRD on a new initiative |
| "notes", "minutes", "recap", "write up the meeting", "can you document" | `meeting_minutes` | Colleague asking for meeting notes after a sync |

For each match, extract:
- What specifically is being requested
- The relevant ticket, meeting, or initiative name
- The deadline, if mentioned
- Who asked

Store all matches as `DRAFT_TRIGGERS` — used in Step 1b below.

**Tasks** — scan `Tasks/` for files with `status: s` (in progress) or `priority: P0`. Note titles and due dates only — do not read full files.

---

### Step 1b — Auto-draft goal updates (if triggered)

If `DRAFT_TRIGGERS` is non-empty, run this step before posting the morning brief.

For each triggered item, call the `/draft` router:

1. Read `/Users/priscila/Documents/Agents/personal-agent-main/.claude/skills/draft/SKILL.md` and execute it, passing the full context of what was requested (goal update, meeting notes, PRD request — whatever was detected).
2. The `/draft` skill routes to the correct sub-skill and posts its output to `#prw-personal-agents` (C0AM6E2D4R2) — do not suppress it.
3. After the draft is posted, add a line to the morning brief under `*⚠️ Heads Up*`:
   > *🖊️ Draft ready: [type] — [subject]. Check #prw-personal-agents.*

If `DRAFT_TRIGGERS` is empty, skip this step entirely.

---

### Step 2 — Pick 3 focus items

Select exactly 3 focus items for today. Priority order:
1. Overdue Jira items (due date passed, not done)
2. P0 tasks from `Tasks/`
3. Jira items due today
4. In-progress Jira items most recently updated
5. Active tasks (`status: s`) by priority field

State each item as: what it is, why it's the priority today (due date, overdue, or goal ref).

---

### Step 3 — Compose the Slack message

Format for Slack markdown. Keep the whole message under 2800 characters. Omit any section where there's nothing to report — don't write "None" or empty headers.

```
*☀️ Morning Brief — [Weekday, DD Mon]*

*📅 Today's Calendar*
• [HH:MMam] — [Meeting name] ([duration]) [🔁 if recurring] [👥 1:1 flag if applicable]
• ...
_[Flag if back-to-back stretches exist, e.g. "⚡ Heads up: 10am–1pm is back-to-back"]_

*🎯 Top 3 for Today*
1. *[Item]* — [why: overdue / due today / goal ref]
2. *[Item]* — [why]
3. *[Item]* — [why]

*🔴 Jira — Overdue*
• [[KEY-123]](jira-url) [summary] _(due [date])_

*🟡 Jira — Due Today*
• [[KEY-456]](jira-url) [summary]

*💬 Overnight Slack*
• [1-line summary of anything actionable or decision-relevant. No FYIs.]

*⚠️ Heads Up*
• [Any risk, blocker, or time-sensitive thing worth knowing before starting the day]
```

Rules:
- Jira issue keys must link to the issue: `https://canva.atlassian.net/browse/[KEY]`
- Omit the *Overnight Slack* section if nothing actionable was found
- Omit the *Heads Up* section if nothing to flag
- Omit *Jira — Overdue* or *Jira — Due Today* sections individually if empty
- If calendar is empty, write: `• No meetings today 🎉`
- Do not add "have a great day" or any motivational language

---

### Step 4 — Post to Slack

Call `slack_send_message` with:
- `channel_id`: `C0AM6E2D4R2` (#prw-personal-agents)
- `message`: the composed brief from Step 3

If the post succeeds: done. Output nothing to stdout except a single confirmation line for the log: `morning-briefing posted to #prw-personal-agents`.

If the post fails: log the error and exit. Do not retry.

---

## Edge cases

- **Weekend run**: If today is Saturday or Sunday, post a single line: `*🗓️ No brief today — it's [Saturday/Sunday].*` and exit.
- **Public holiday / OOO**: If the calendar shows an all-day OOO or public holiday event, note it at the top of the brief: `_📴 OOO today — brief is for reference only._`
- **All tools fail**: Post: `*☀️ Morning Brief — [date]* \n⚠️ Could not reach tools (Calendar, Jira, Slack). Check connections.`
- **No Jira items**: Omit both Jira sections entirely.
- **No overnight Slack signals**: Omit the Overnight Slack section.
