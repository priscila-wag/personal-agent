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

### Step 4 — Draft the update

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

---

### Step 5 — Post draft to #prw-personal-agents

Call `slack_send_message` with channel `C0AM6E2D4R2`:

```
*📋 Goal update draft ready — [[UVSG-XXX]](https://canva.atlassian.net/browse/UVSG-XXX)*
_[Goal name]_

[Andi sign-off status: ✅ Signed off — "[quote]" OR ⚠️ Discussed — "[quote]" OR ❌ Not found — confirm before posting]

---
[Full draft text, formatted exactly as it would appear in Jira]
---

Reply *confirm* to post to Jira · *edit [section] [new text]* to change · *skip* to discard
```

Wait for Pri's response.

---

### Step 6 — On "confirm": post to Jira

Call `addCommentToJiraIssue` on the UVSG ticket with the confirmed draft text.

Then reply in the same Slack thread:
> *✅ Posted to [[UVSG-XXX]](https://canva.atlassian.net/browse/UVSG-XXX)*

Optionally: if the Slack thread where the goal update was requested is known (e.g. the channel where Eva or Simone asked for updates), reply there too:
> *Updated! [[UVSG-XXX]](https://canva.atlassian.net/browse/UVSG-XXX) — [1-line summary of the update]*

---

### Step 7 — On "edit [section] [new text]"

Replace the named section in the draft and re-post the full updated draft to the same Slack thread. Repeat Step 5 logic.

---

## Edge cases

- **No existing comment template found**: use the default structure above, note in Slack message: *"No previous comment template found — using default structure."*
- **Goal ticket not found in Jira**: post to #prw-personal-agents: *"⚠️ Couldn't find [ticket] in Jira. Check the ticket key and try again."*
- **No HELP tickets linked**: note in the draft context but do not block — draft based on goal description and Slack only.
- **Andi sign-off not found**: include the ❌ flag prominently in the Slack post. Do not block the draft, but make the flag hard to miss.
- **Metric data missing**: write "[metric data needed — check with Damien]" in the Progress Update section rather than inventing a number.
