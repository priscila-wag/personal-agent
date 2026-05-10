---
name: achievements
description: "Weekly G&I achievements log. Pulls official goal progress from Jira (UVSG goals/milestones + HELP epics assigned to the user), surfaces extra work from Slack, maps everything to the user's G&I goals, flags growth behaviours, and appends a dated entry to a running achievements log. Use whenever someone says: /achievements, 'log my achievements', 'what did I deliver this week', 'update my G&I log', 'capture my wins', 'log my extra work', 'track what I shipped', 'G&I prep', or anything about recording weekly progress for review season."
---

# /achievements — Weekly G&I Achievements Log

Build a weekly achievements entry that maps the user's work to their G&I goals, flags growth behaviours, captures extra work beyond their official remit, and appends everything to a running log. The goal: G&I self-review becomes a copy-paste exercise, not a memory test.

Run this standalone any day — Friday afternoon is ideal, but it works mid-week too.

---

## Configuration

At the start of the skill, read:
- `Context/agent-config.md` — for the user's Slack ID and G&I goals file path
- The file referenced under **G&I Goals File** in agent-config (e.g. `Context/G&I Goals H1 2026.md`) — for the user's current goals, goal tags, milestone hierarchy, growth behaviours, and routing rules

All goal descriptions, tags, milestone tables, and routing rules come from those files. Do not hardcode them here.

---

## Step 1: Pull Official Goal Progress from Jira

Run these JQL queries. Focus on what *moved* this week — status transitions, comments, decisions — not just what exists.

**UVSG goals and milestones assigned to the user:**
```
project = UVSG AND assignee = currentUser() AND updated >= -7d ORDER BY updated DESC
```

**HELP milestones with status changes this week:**
```
project = HELP AND assignee = currentUser() AND issuetype = Milestone AND updated >= -7d AND status changed DURING (-7d, now()) ORDER BY updated DESC
```

**HELP tasks with status changes this week (catches significant deliverables):**
```
project = HELP AND assignee = currentUser() AND updated >= -7d AND status changed DURING (-7d, now()) ORDER BY updated DESC
```

For each result, extract: issue key, summary, current status, parent key, and parent summary. Use the parent to determine which UVSG goal or HELP epic the work sits under — refer to the routing rules in the G&I Goals file. A ticket moving Done = achievement. A ticket moving In Progress = momentum.

---

## Step 2: Pull Extra Work Signals from Slack

Search for substantive public channel messages from the user in the last 7 days. Use the Slack user ID from `Context/agent-config.md`. Look for:
- Meeting summaries or decisions posted to channels
- New initiatives being kicked off or scoped
- Capability building or tool adoption driven by the user
- Cross-functional coordination that isn't tracked in a Jira ticket
- Things the user said no to (deprioritisation decisions)

Query: `from:<@[slack_user_id]> after:[date 7 days ago]`

Skip DMs unless they contain a decision or outcome. Focus on channels — that's where the cross-functional signal lives.

---

## Step 3: Synthesise Achievements

Write 4–8 entries. Quality over volume — a week with 5 sharp entries is better than 10 vague ones.

Use the goal tags and growth behaviour flags defined in the G&I Goals file.

**Entry format:**
```
**[JIRA-ID · Jira issue title]** `#[goal-tag]`

[Action taken — one line.]
[What was decided or delivered — one line.]
[Who was involved and what it unblocks — one line.]

[Optional: growth behaviour flag — one phrase, no explanation needed]
[Optional: → future goal candidate: [name]]
```

**Formatting rules:**
- Always include the Jira ID AND the issue title in the header so it's clear what goal or ticket this maps to.
- Use line breaks between each fact — not full paragraphs, not a wall of prose.
- Lead with the action (what was done), then the outcome, then the names involved.
- Keep each line to one idea. If you need more than 4 lines, the entry is too long.
- Growth behaviour flag goes on its own line at the end, no explanation — the entry itself should make it obvious.
- Only flag a growth behaviour if the entry clearly shows it. Skip if it's a stretch.
- Only add `→ future goal candidate` if this topic has appeared in 2+ entries or has explicit stakeholder endorsement.

---

## Step 4: Ask for Additions

After presenting the synthesised entries, ask:

> "Anything I missed? Think about: decisions made that aren't in Jira, capability work done for the team, things explicitly said no to (visible prioritisation), extra coordination that isn't tracked anywhere, or new initiatives being seeded."

Wait for the user's response. Add anything they name with `#extra` and the appropriate goal tag(s). If they describe something that will likely become a formal goal, note it with a `→ future goal candidate` flag.

---

## Step 5: Append to the Achievements Log

Append to `Context/Progress Updates/achievements-log.md`.

If the file doesn't exist yet, create it with this header first:

```markdown
# Achievements Log

Running weekly record of G&I-relevant work. Built for self-review, goal tracking, and G&I season prep.

**Goal tags:** _(from current G&I Goals file)_

**Growth behaviour flags:** 🧠 AI judgment · 🔭 Strategic leverage · 📣 Visible prioritisation · 🎙 Signal-first comms

---
```

Then append the week's section (most recent at top):

```markdown
## CW[XX] — Week of [DD Mon YYYY]

[entries]

---
```

Confirm: *"Logged to `Context/Progress Updates/achievements-log.md`."*

---

## What Good Looks Like Over Time

After 8–10 weeks, the log should show:
- All goals represented most weeks — if one goes cold for 3+ weeks, flag it
- Growth behaviour flags appearing with increasing frequency, especially 🧠 and 🔭
- `#extra` entries clustering around 1–2 repeating themes → these are next goal-setting proposals
- A trail of names, metrics, and decisions that can be cited verbatim in G&I self-review

When `#extra` entries have appeared 3+ weeks in a row around the same theme, surface it: *"This pattern keeps showing up in #extra — worth considering as a formal goal next cycle."*
