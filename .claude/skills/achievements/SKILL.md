---
name: achievements
description: "Weekly G&I achievements log. Pulls official goal progress from Jira (UVSG goals/milestones + HELP epics assigned to Pri), surfaces extra work from Slack, maps everything to Pri's 3 G&I goals, flags growth behaviours (AI judgment, strategic leverage, visible prioritisation, signal-first comms), and appends a dated entry to a running achievements log. Use whenever Pri says: /achievements, 'log my achievements', 'what did I deliver this week', 'update my G&I log', 'capture my wins', 'log my extra work', 'track what I shipped', 'G&I prep', or anything about recording weekly progress for review season. Always use this skill — not generic note-taking — for Pri's achievements workflow."
---

# /achievements — Weekly G&I Achievements Log

Build a weekly achievements entry that maps Pri's work to her G&I goals, flags growth behaviours, captures extra work beyond her official remit, and appends everything to a running log. The goal: G&I self-review becomes a copy-paste exercise, not a memory test.

Run this standalone any day — Friday afternoon is ideal, but it works mid-week too.

---

## Pri's 3 G&I Goals (Feb 2026 feedback cycle)

**`#ai-first-hc` AI-First Help Center**
Deliver visible AI-driven HC surfaces (side panels, dynamic recommendations) with a clear evaluation framework. Evidence bar: shipped UX changes with measurable improvements in task success or resolution quality.

**`#content-pipeline` Automated Content Pipeline**
Transform HC processes toward automation — from manual "push" updates to PR or source-of-truth-driven "pull" models. Evidence bar: reduced content update latency, fewer manual handoffs, higher confidence in content freshness.

**`#scalable-delivery` Scalable Delivery & Leverage**
Design a delivery model for multiple initiatives without dilution — through explicit sequencing, ownership, and capacity planning. Evidence bar: sustained progress across parallel streams, quality maintained, tradeoffs made visible.

**`#extra` — Extra Work & Emerging Initiatives**
Work beyond official goals: capability building for the team, cross-functional problem-solving, new initiatives being seeded, process improvements others adopted. This category is how "extra work becoming new goals" gets tracked over time — cluster patterns = next goal-setting proposals.

---

## Growth Behaviours to Flag

Flag these when there is a concrete example. One sentence is enough. Skip if it's a stretch.

- **🧠 AI judgment** — eval rigor, incremental UX in chat UIs, designing AI-ready systems (not just features), owning quality bars
- **🔭 Strategic leverage** — sequencing work explicitly, protecting focus, doing less to create more impact, seeding initiatives that others pick up
- **📣 Visible prioritisation** — explicitly communicating what was deprioritised and why, making tradeoffs legible to stakeholders before they ask
- **🎙 Signal-first comms** — concise communication to senior stakeholders (Andi, Carl, cross-org leads) that leads with the "so what", not the backstory

---

## Pri's Goal → Milestone Hierarchy (verified in Jira)

**Always group achievements under the correct UVSG parent goal.** Use the `parent` field from Jira to verify — never assume. The verified hierarchy is:

| UVSG Goal | Summary | Key Milestones |
|-----------|---------|----------------|
| UVSG-615 | Launch Integrated AI Help Centre and Assistant | HELP-3014 (Persist HC HowTo in HA); research tasks under HELP-1918 (HC 3.0 continuous discovery epic) |
| UVSG-614 | Increase logged-in HC Sessions | HELP-3813 (Incentivise logged-out to login); HELP-4340 (No-Reply Emails); HELP-4319 (Logged-out HA version) |
| UVSG-630 | Launch platformised Help Assistant into 3+ teams | HELP-3785 (Canva AI Help in ChatGPT MCP) |
| UVSG-642 | Launch automate visual asset creation across locales | HELP-4298 (Storylane POC); HELP-4291 (Auto-capture screenshots) |
| UVSG-617 | Integrate help into 2+ search bars | HELP-3814, HELP-3815 — **Cancelled CW14** |

**HELP Epics (extra work + emerging initiatives):**

| Epic | Summary | Notes |
|------|---------|-------|
| HELP-4139 | Mobile Help Experience Strategy & Discovery | Future goal track — tasks HELP-4295, HELP-4296 sit here |
| HELP-3812 | Enable split panel view for HA (Milestone, Delivered) | Eval tasks like HELP-4281 (FullStory SPAIT) sit here |
| HELP-1918 | Continuous discovery & research for HC 3.0 | Research tasks like HELP-4176, HELP-4312 sit here |
| HELP-3090 | Pri's miscellaneous tasks | Admin/coordination tasks like HELP-4318, HELP-4325, HELP-4279 |

**Rules:**
- Always fetch the `parent` field when pulling HELP tickets — do not group by keyword guessing.
- Milestones under UVSG-615 are AI-first HC work → `#ai-first-hc`
- Milestones under UVSG-614 are logged-in session growth → `#ai-first-hc`
- Milestones under UVSG-630 are platform/distribution → `#ai-first-hc`
- Milestones under UVSG-642 are content automation → `#content-pipeline`
- Tasks under HELP-4139 (Mobile) → `#scalable-delivery`
- Tasks under HELP-3090 (Pri's misc) → `#extra` unless clearly tied to a goal

---

## Step 1: Pull Official Goal Progress from Jira

Run these JQL queries. Focus on what *moved* this week — status transitions, comments, decisions — not just what exists.

**UVSG goals and milestones assigned to Pri:**
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

For each result, extract: issue key, summary, current status, parent key, and parent summary. Use the parent to determine which UVSG goal or HELP epic the work sits under — refer to the hierarchy table above. A ticket moving Done = achievement. A ticket moving In Progress = momentum.

---

## Step 2: Pull Extra Work Signals from Slack

Search for substantive public channel messages from Pri in the last 7 days. Look for:
- Meeting summaries or decisions posted to channels
- New initiatives being kicked off or scoped
- Capability building or tool adoption driven by Pri
- Cross-functional coordination that isn't tracked in a Jira ticket
- Things Pri said no to (deprioritisation decisions)

Query: `from:<@U0701AR9B35> after:[date 7 days ago]`

Skip DMs unless they contain a decision or outcome. Focus on channels — that's where the cross-functional signal lives.

---

## Step 3: Synthesise Achievements

Write 4–8 entries. Quality over volume — a week with 5 sharp entries is better than 10 vague ones.

**Entry format:**
```
**[JIRA-ID · Jira issue title]** `#ai-first-hc` / `#content-pipeline` / `#scalable-delivery` / `#extra`

[Action taken — one line.]
[What was decided or delivered — one line.]
[Who was involved and what it unblocks — one line.]

[Optional: 🧠 / 🔭 / 📣 / 🎙 growth behaviour flag — one phrase, no explanation needed]
[Optional: → future goal candidate: [name]]
```

**Formatting rules:**
- Always include the Jira ID AND the issue title in the header so it's clear what goal or ticket this maps to.
- Use line breaks between each fact — not full paragraphs, not a wall of prose.
- Lead with the action (what Pri did), then the outcome, then the names involved.
- Keep each line to one idea. If you need more than 4 lines, the entry is too long.
- Growth behaviour flag goes on its own line at the end, no explanation — the entry itself should make it obvious.
- Only flag a growth behaviour if the entry clearly shows it. Skip if it's a stretch.
- Only add `→ future goal candidate` if this topic has appeared in 2+ entries or has explicit stakeholder endorsement.

---

## Step 4: Ask for Additions

After presenting the synthesised entries, ask:

> "Anything I missed? Think about: decisions made that aren't in Jira, capability work done for the team, things explicitly said no to (visible prioritisation), extra coordination that isn't tracked anywhere, or new initiatives being seeded."

Wait for Pri's response. Add anything she names with `#extra` and the appropriate goal tag(s). If she describes something that will likely become a formal goal, note it with a `→ future goal candidate` flag.

---

## Step 5: Append to the Achievements Log

Append to `Context/Progress Updates/achievements-log.md`.

If the file doesn't exist yet, create it with this header first:

```markdown
# Achievements Log

Running weekly record of G&I-relevant work. Built for self-review, goal tracking, and G&I season prep.

**Goal tags:**
- `#goal-1` AI-First Help Center
- `#goal-2` Automated Content Pipeline & AI-First Content Ops
- `#goal-3` Scalable Delivery & Leverage
- `#extra` Extra work beyond official goals

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
- All 3 goals represented most weeks — if one goes cold for 3+ weeks, flag it
- Growth behaviour flags appearing with increasing frequency, especially 🧠 and 🔭
- `#extra` entries clustering around 1–2 repeating themes → these are next goal-setting proposals
- A trail of names, metrics, and decisions that can be cited verbatim in G&I self-review

When `#extra` entries have appeared 3+ weeks in a row around the same theme, surface it: *"This pattern keeps showing up in #extra — worth considering as a formal goal next cycle."*
