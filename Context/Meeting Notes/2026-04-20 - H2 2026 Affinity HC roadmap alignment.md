# H2 2026 Affinity HC Roadmap Alignment
*2026-04-20 | 25 min | [[Tash Kelly]], [[Marlene Ensor]], [[Kunday]], [[Arnee]], Amy Capstick, [[Priscila Wagner]]*

## Summary
A roadmap alignment call with [[Tash Kelly]] (Affinity) to map H2 HC priorities and agree on success metrics. Two threads emerged: (1) content pipeline — the new lock-request publishing system targeting June (possibly extending to August) is the right direction but capacity has been squeezed by Canva Create; (2) metrics gaps — Affinity HC has no help engagement or retention metrics on its dashboard, and old pages continue to outrank new HC content. Both gaps need to be addressed before Affinity can measure the impact of HC improvements.

## Decisions
- Add help engagement + retention metrics to the data request now — don't wait for the AI transition to be complete ([[Tash Kelly]] + Pri agreed)
- Pipeline priorities to get proper focus in the post-Canva Create recovery period (no new deadline set, but agreed it's the next unlock)
- No formal H2 goals committed — this was an alignment and gap-identification session

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Check with data scientists: how to measure activation, retention, and engagement for Affinity HC — flag offline usage edge case | Pri | [[HELP-3090]] | — |
| 2 | Chat with marketing/SEO team: why do old Affinity pages rank higher than new HC content, and what's the fix | Pri | [[HELP-3090]] | — |
| 3 | Check with Hank (Hype) re: pending actions on [[UVSG-615]] integration | Pri | [[UVSG-615]] | — |
| 4 | Follow up with content team on content models review, content creation, troubleshooting, and 4-level architecture progress | Pri | [[HELP-3090]] | — |
| 5 | Coordinate with content team on how they want to structure 4 levels in the HC architecture | Pri | [[HELP-3090]] | — |
| 6 | Add help engagement + retention metrics as an explicit data request for Affinity | Pri | [[HELP-3090]] | — |

## Open Questions & Blockers
- What % of Affinity users use the tool offline? (Tash unsure — blocks activation metric design)
- Why do old Affinity pages rank better than new HC content? (SEO team consultation needed)
- Where does "Ask about this page" sit in the new [[HC AI mode]] experience — on current or new AI mode surface? (Open per #uv-help-ai-platform thread today)
- No help engagement or retention metrics currently exist for Affinity — broader data request needed before any baseline can be set

## Context
- [[Affinity]] HC is currently only tracked with basic data — missing engagement and retention dimensions
- New Contentful publishing system (lock-request based) expected by June, possibly August — removes the manual gate that caused late-night engineer scrambles during Create
- Affinity's H2 goal includes increasing MAUs and contributing to ARR via ProDesign upgrades (free → pro) — HC improvements are a supporting lever
- Canva Create consumed bandwidth over the past month; post-event recovery is the window to tackle pipeline
- [[AI-First Help Center]] transition adds urgency to metrics baseline — measuring AI-era help success requires more than CSAT
