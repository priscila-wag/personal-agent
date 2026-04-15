---
name: draft-goal-update
description: "Draft a monthly progress update for a UVSG goal ticket. Gathers context from Jira, linked HELP tickets, and Slack. Checks for Andi Schuster sign-off. Posts draft to #prw-personal-agents for review before any Jira write."
---

# Draft Goal Update

Draft the monthly progress comment for a UVSG goal ticket, following the standard template. Always post to #prw-personal-agents for review — never write to Jira until Pri confirms.

---

## Known goal → ticket map

| Goal | Ticket |
|------|--------|
| Increase logged in AI Help Center sessions by 5% to provide tailored help guidance | UVSG-614 |
| Launch Integrated AI Help Centre & Assistant | UVSG-615 |

Update this table when new goals are created.

**Pri's Slack user ID:** `U0701AR9B35`
**Andi Schuster (sign-off):** Slack `U06RUJU3URE`, Jira `andi.schuster@canva.com`
**#prw-personal-agents channel ID:** `C0AM6E2D4R2`

---

## Instructions

### Step 1 — Resolve the ticket

If a ticket key was passed as an argument (e.g. `UVSG-614`), use it directly.
If only a goal name was passed, match it to the table above.
If neither, check for the most recent goal update request in Slack and infer from context.

---

### Step 2 — Fetch Jira context (parallel)

Run all of these in parallel:

**A. Goal ticket details**
Call `getJiraIssue` with the UVSG ticket key. Extract:
- Current goal description / scope
- Target metric and current value (if in description)
- Milestone list and their statuses
- Any recent description changes (note the date of last edit)

**B. Existing comments — extract the template**
Call `getCommentsForJiraIssue` on the UVSG ticket. Find the most recent comment that follows the monthly update structure. Extract the exact heading format being used (some goals use slightly different headings). Use that exact structure for the new draft — do not invent a new format.

**C. Linked HELP tickets**
Call `searchJiraIssuesUsingJql`:
```
"Epic Link" = [UVSG-ticket] AND updated >= -30d ORDER BY updated DESC
```
Also run:
```
project = HELP AND "Epic Link" = [UVSG-ticket] AND statusCategory = Done AND updated >= -30d
```
Extract: what was completed, what's in progress, any blockers.

---

### Step 3 — Gather Slack context (parallel)

Run all of these in parallel:

**A. Goal channel discussions (past 30 days)**
```
slack_search_public_and_private: [goal name keywords] in:uvsg-hcf OR in:hcf-team after:[30-days-ago]
```
Extract: decisions made, scope changes, blockers raised.

**B. Andi Schuster sign-off check**
```
slack_search_public_and_private: from:U06RUJU3URE [goal keywords] after:[30-days-ago]
```
Also search DMs between Pri (U0701AR9B35) and Andi (U06RUJU3URE).

Classify the Andi sign-off as one of:
- ✅ **Signed off** — explicit LGTM, approval, or agreement on scope/decision. Quote the message.
- ⚠️ **Discussed** — relevant conversation found but no explicit sign-off. Quote the closest message.
- ❌ **Not found** — no relevant recent messages.

**C. Meeting notes**
Scan `Context/Meeting Notes/` for files from the past 30 days containing the goal name or ticket key. Extract any decisions or milestones mentioned.

---

### Step 4 — Draft the update and GA slide sentence

Write the update following the template structure from Step 2B (most recent existing comment). If no existing comment found, use this default structure:

```
Progress Update
[1–2 sentences. What shipped or moved since last update. Lead with the result, not the effort. Be specific — name the milestone or metric change if known.]

What's Changed
[Scope changes, direction shifts, or key decisions made this month. If Andi signed off on something, cite it: "Agreed with Andi to [decision]." If nothing changed, write "No scope changes."]

What's next
[Specific upcoming milestones. Name them. If dates are known, include them. Not "continuing work" — name the thing.]

Risks & Blockers
[Real blockers only. If none, write "N/A".]
```

**Voice rules (from pri-brain.md):**
- Direct, no effort framing — leads with result
- Specific over vague — name things
- Short — no sentence should be padded
- Cite Andi by name when referencing signed-off decisions: *"Agreed with Andi to..."*

**Also draft a GA slide sentence** — one sentence for the Goal Alignment deck (the stakeholder-facing update, not the Jira comment). This is separate from the full update.

Rules for the GA sentence:
- One sentence only — max 20 words
- Stakeholder-facing: written for people who don't track the goal week to week
- Snappy and outcome-focused: what changed or what's happening that they should know
- Not a summary of the Jira comment — a headline
- Examples of good GA sentences:
  - *"Goal rescoped to focus on login incentives — personalisation moved to H2."*
  - *"Logged-out HA launching soon, unlocking the key driver for this goal."*
  - *"On track — Quick Actions milestone shipped to 100% of users."*

---

### Step 5 — Post draft to #prw-personal-agents

Call `slack_send_message` with channel `C0AM6E2D4R2`:

```
*📋 Goal update draft — [[UVSG-XXX]](https://canva.atlassian.net/browse/UVSG-XXX)*
[Andi sign-off status: ✅ Signed off — "[quote]" OR ⚠️ Discussed — "[quote]" OR ❌ Not found — confirm before posting]

*🎯 GA slide sentence*
[One snappy sentence for the Goal Alignment deck]

*📝 Jira comment*
Run `/jira comment UVSG-XXX` and paste:
```
[Full Jira comment text]
```
```

No confirmation needed — both outputs are ready to use directly.

---

### Step 6 — Reply to the original Slack request (if source thread is known)

If the Slack thread where the update was requested is known (e.g. Eva or Simone's post in the goal channel), reply there:
> *Updated! [UVSG-XXX] — [GA sentence]. Jira comment added.*

Otherwise, skip this step.

---

## Edge cases

- **No existing comment template found**: use the default structure above, note in Slack message: *"No previous comment template found — using default structure."*
- **Goal ticket not found in Jira**: post to #prw-personal-agents: *"⚠️ Couldn't find [ticket] in Jira. Check the ticket key and try again."*
- **No HELP tickets linked**: note in the draft context but do not block — draft based on goal description and Slack only.
- **Andi sign-off not found**: include the ❌ flag prominently in the Slack post. Do not block the draft, but make the flag hard to miss.
- **Metric data missing**: write "[metric data needed — check with Damien]" in the Progress Update section rather than inventing a number.
