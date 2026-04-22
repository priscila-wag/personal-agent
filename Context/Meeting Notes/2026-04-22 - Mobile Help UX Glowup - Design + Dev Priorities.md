# Mobile Help UX Glowup — Design + Dev Priorities
*2026-04-22 | 30 min | [[Priscila Wagner]], [[Michelle Huang]], [[Simone]], [[Jenna]]*

## Summary
The team triaged and finalised sprint priorities for the [[Mobile Help UX]] glowup, locking in 3 bugs for [[Jenna]] to ship this sprint and scoping out two items (file preview thumbnails, endless sheet stacking) that need more design/coordination work. The biggest unlock is an MVP fix for the [[Help Center]] article navigation bug — opening articles in the phone browser as a stopgap while a proper inline solution is designed.

## Decisions
- **Error banner issue (row 28):** Out of scope — occurs in the object panel, not Help Assistant; escalate to editor team
- **HC navigation bug:** Ship MVP this sprint (open articles in phone browser); design long-term inline article loading separately — pattern also applies to Offline Canva's Classic Assistant
- **File preview thumbnails (row 33):** Removed from sprint — needs design work on thumbnail pattern and coordination with Easel components team
- **Endless sheet stacking (row 26):** No longer valid — CSAT is switching to thumbs up/down only, invalidating the scenario
- **Settings entry point:** [[Michelle Huang]] and [[Simone]] will refine [[Matthew]]'s designs, map scroll/nav bar behaviour patterns, and coordinate with AdminX for experiment setup

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Investigate UI glitch — focus event/scroll height issue (row 28) | Jenna | [[HELP-4139]] | This sprint |
| 2 | Ship MVP fix for HC navigation bug (open articles in phone browser) | Jenna | [[HELP-4139]] | This sprint |
| 3 | Complete technical spike on half-sheet drag behaviour | Jenna | [[HELP-4139]] | End of next week |
| 4 | Clone HC navigation ticket; create separate design ticket for long-term inline article solution | Pri | [[HELP-4139]] | — |
| 5 | Attach Canva AI recording to half-sheet spike ticket as reference behaviour | Pri | [[HELP-4139]] | — |
| 6 | Contact PM to identify stakeholders for settings entry point discussion | Pri | [[HELP-4139]] | — |
| 7 | Remove file preview thumbnail task from current sprint | Pri | [[HELP-4139]] | — |
| 8 | Review Matthew's settings designs; map scroll/nav bar patterns; coordinate with AdminX for experiment | Michelle & Simone | [[HELP-4139]] | — |

## Open Questions & Blockers
- **Half-sheet complexity:** Canva AI has significant sheet-specific code — Jenna needs to spike feasibility before committing to build; timeline TBC after spike
- **File upload limit:** Appears to be 1 photo via camera, multiple via gallery — needs verification before designing around it
- **Settings entry point experiment:** Timeline and resource allocation with AdminX still pending
- **Long-term HC inline article design:** Who owns this design track and when does it slot in?

## Context
- The [[half-sheet drag behavior]] affects ~3M mobile sessions — highest-priority item in the glowup backlog
- The **HC navigation bug root cause**: articles open in a web view inside the app, creating stacked navigation that breaks back button behaviour
- The long-term inline article solution also applies to offline Canva's Classic Assistant ([[logged-out HA]] scenario), so design should account for both contexts
- [[UVSG-615]] split panel is at 100% rollout — mobile polish is the next visible UX gap
- Sprint scope: UI glitch + HC nav bug MVP + half-sheet spike; file preview and sheet stacking removed
