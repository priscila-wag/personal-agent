---
title: HCF Planning — Museum of Tomorrow sprint
description: "Sprint planning for 'Museum of Tomorrow' sprint. Ask about this page deferred to H2; Search vs AI Mode launch May 6; HYPE knowledge-sharing kickoff agreed."
type: meeting-note
created_date: 2026-04-20
---

# HCF Planning
*2026-04-20 | ~50 min | [[Priscila Wagner]], [[Kunday]], [[Tahlia Giann]], [[Mann]], [[Jenna Murphy]], [[Pat Santos]], [[Leo Kuang]], [[Carl | Contextual Self-Help | EM]]*

## Summary
The team planned the "Museum of Tomorrow" sprint against two months remaining in the cycle. [[UVSG-615]] Search vs AI Mode launch is confirmed for May 6 and is on track; the "Ask about this page" [[HC AI mode]] feature is officially deferred to H2 — design solution and technical LGTM targeted by end of June. The bigger shift: [[AI-First Help Center]] integration with [[Help Assistant]] (Magic Answers service) is now identified as the H2 north star, and the team agreed to start HYPE knowledge-sharing this cycle as onboarding groundwork.

## Decisions
- **Ask about this page deferred to H2.** Feature blocked by Canva AI (page context referencing) and potentially [[HYPE]] dependencies. Team to deliver design LGTM + technical solution by end of June for H2 execution. Decision made by [[Priscila Wagner]] + [[Kunday]].
- **HYPE knowledge-sharing to start this sprint.** Backend team to book sessions with [[HYPE]] to understand Magic Answers service architecture — explicitly framed as onboarding for HC–[[Help Assistant]] integration in H2. Decision: [[Priscila Wagner]].
- **Storylane embed trial: MVP only.** Treat embeds like YouTube videos — no tabbed content support, desktop-only, fewer than 5 high-traffic articles. Start trial Tuesday April 23, 7-day window. Decision: [[Carl | Contextual Self-Help | EM]] + [[Priscila Wagner]] + team.
- **Logged-out HA: kickoff needed with HYPE.** Before moving forward, [[Priscila Wagner]] to organize a kickoff with the HYPE team to understand content implications and login-prompting behavior for account-specific queries.

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Kickoff meeting for triggering in-context action [[Help Assistant]] | [[Tahlia Giann]] | [[UVSG-615]] | Before Thu Apr 24 |
| 2 | Confirm HYPE dependency status for "ask about this page" before Wednesday goal alignment | [[Tahlia Giann]] | [[UVSG-615]] | Before Wed Apr 22 |
| 3 | Design exploration: AI Mode 2.0 — follow-up questions in AI mode vs articles, contextual awareness | [[Tahlia Giann]] + Pri | [[UVSG-615]] | — |
| 4 | Schedule knowledge-sharing sessions with HYPE team on Magic Answers service architecture | [[Kunday]] | [[UVSG-615]] | This sprint |
| 5 | Organize kickoff with HYPE team for [[logged-out HA]] launch; understand content implications + personalization limitations | Pri | [[HELP-4319]] | This sprint |
| 6 | Prioritization meeting with marketing team to select no-reply emails for HC linking; confirm HYPE support needs | Pri | [[HELP-4340]] | Thu Apr 24 |
| 7 | Deploy Storylane embed; coordinate with [[Tahlia Giann]] on padding/UI adjustments | [[Jenna Murphy]] | [[HELP-3820]] | By Tue Apr 23 |
| 8 | Start Analytics SDK → Telemetry SDK migration (4–5 days estimated; first cards slower, rest simpler) | [[Mann]] | [[HELP-3090]] | This sprint |
| 9 | Complete Terraform config update to fix queue spike alert noise | [[Leo Kuang]] | [[HELP-3090]] | This sprint |
| 10 | Share handover doc before 3-week leave; remain on-call for Canva Create 2025 fast-follows | [[Pat Santos]] | [[HELP-3090]] | Before end of sprint |

## Open Questions & Blockers
- **Ask about this page blocker:** Blocked by both Canva AI (page context referencing) and potentially HYPE (Magic Answers architecture). [[Tahlia Giann]] to verify HYPE dependency status before Wednesday goal alignment — if HYPE is a dependency, risk of "you should have consulted with us" pushback.
- **HYPE capacity:** Multiple H1 features depend on HYPE team (no-reply email links, [[logged-out HA]], follow-up questions in AI mode). No confirmed capacity. Escalation path needed if unavailable — Pri noted she will escalate if needed.
- **Logged-out HA deployment status:** Waiting on [[Willian]] (currently in Brazil) to confirm whether logged-out HA is deployed. No response yet as of this meeting. ⚠️ *This blocker also appears as open in Week-2026-W15 tasks (multiple unchecked items: "Willian — confirm logged-out HA prompts are reviewed + go-live unblocked"). Now surfacing a second cycle — consider whether this needs a forcing deadline before next check-in.*
- **AI Mode 2.0 follow-up questions — technical spike needed:** [[Mann]] flagged Guy's suggestion to include article context in every request; needs spike to verify JSON format compatibility with HYPE backend before committing to approach.
- **Backend capacity constraints:** One engineer out until May 5; AI week May 5; new starter May 16–17 limiting backend work. New Help Assistant backend work unlikely this sprint — flagged as unfamiliar territory.
- **Storylane tabbed content:** Decision taken to skip tabbed content support for MVP. If selected articles use tabbed content, may need minor content edits — to be assessed once article list is confirmed.

## Context
- Sprint name "Museum of Tomorrow" — Rio de Janeiro museum. Sprint duration: 8–9 days (Sydney has Anzac Day public holiday Mon Apr 28; Melbourne status unclear but effectively same effective capacity).
- Affinity is live; ~700 content entries migrated to production last week via content pipeline. AutoML optimization expected to save ~40 min in pipeline per run.
- [[Pat Santos]] going on 3-week leave after this sprint; handover doc needed.
- Storylane trial kicks off Tue Apr 23 — comparing against existing Treble video work on same articles to get tool viability signal.
- Search vs AI Mode ([[UVSG-615]]) remaining cards added to sprint; test party set up with temporary translations while waiting for new label translations. May 6 deadline is the team's next big public milestone.
- Content pipeline consolidation goal: unify staging/production flows into the same pipeline to reduce complexity and prevent past issues — Kunday to progress this sprint alongside AutoML work.
