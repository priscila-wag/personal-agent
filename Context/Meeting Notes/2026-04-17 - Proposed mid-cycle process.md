---
title: Proposed mid-cycle process
description: "Alignment on Jira-first mid-cycle goal change process: Kanban flagging, weekly batch reviews, Slack-to-Jira bot, pilot with TASSIE-DEVIL goals before full rollout."
type: meeting-note
created_date: 2026-04-17
---

# Proposed mid-cycle process
*2026-04-17 | ~45 min | [[Pri]] (TASSIE-DEVIL), Kate, and other UV delivery/ops members*

## Summary
The team reached alignment on replacing ad-hoc, multi-tool mid-cycle change management with a Jira-first process. The key shift: goal owners submit changes via Jira comments/forms, which auto-flag the goal card; Kate filters by flags for a weekly Monday batch review with Mark — dramatically reducing noise and making LGTM tracking auditable. Pilot starts with Pri's AI and unstuck [[UVSG]] goals before cascading to all 74.

## Decisions
- [[Jira]] is the single source of truth for all goal changes — replaces scattered updates across Confluence, PRDs, and Slack threads
- PRDs remain living documents for problem definition only; they are secondary to Jira for tracking
- Change request form submission in Jira automatically creates a flag on the goal card
- Weekly batch review cadence: changes submitted by Friday midday → reviewed from Monday → consolidated into single sync with [[Mark]]
- Kanban board view for leadership reviews, filtered by flagged items only (mirrors [[Pri]]'s personal banking experience managing ~100 leaders, 500 people)
- Goal owners stay in Jira; [[Mark]] and company goal owners ([[Andy]], Simone, Sally) can remain in Slack initially to reduce friction
- Slack-to-Jira bot will comment LGTMs back into Jira for audit trail
- Pilot scope: [[UVSG]] AI and unstuck goals (~99% capacity) before rolling out to all goals

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Document complete process flow and map workflows for review | Pri + Kate | HELP-3090 | Next 2 weeks |
| 2 | Create whiteboard alignment session before diving into tool configuration | Pri | HELP-3090 | Before Kate starts board setup |
| 3 | Set up Jira Kanban board view with flag automation and Slack integration | Kate | HELP-3090 | Next 2 weeks |
| 4 | Map out when people use which tool for what purpose; establish clear guidelines | Kate | HELP-3090 | Next 2 weeks |
| 5 | Test pilot workflows with unstuck goals subset before cascading to all 74 goals | Pri | HELP-3090 | — |

## Open Questions & Blockers
- Slack-to-Jira LGTM bot not yet built — automation requirements need to be specced before Kate sets up the board
- [[Mark]] doesn't work in Jira regularly — mechanism for his LGTM still unclear (Slack screenshot? Direct comment? Delegate?)
- Custom LGTM icons per company goal owner (Andy, Mark, Simone) — good idea raised but not actioned yet
- Streamlit dashboard integration with Kanban board — flagged, not scoped
- Risk: if anyone can remove flags, approval audit trail breaks — needs clear access/role rules

## Context
- [[Pri]] described the same problem solved at personal banking: ~100 leaders, 500 people, weekly head-of-department sync, only flagged goals appeared in leadership review — dramatically reduced cognitive load
- Goal: mid-cycle changes should feel continuous (agile iteration), but Mark has waterfall preferences — the flagging system bridges both
- [[UVSG-615]] goal change was recently LGTM'd (2026-04-16) after confusion about tool and process — this meeting is a direct response to that friction
- "We haven't done a formal mid-cycle review before because we wanted goal changes to feel continuous rather than quarterly big peaks" — this process is new territory
- Jira Kanban already exists for [[UVSG]] goals; filtering by flags is the lightweight addition needed
