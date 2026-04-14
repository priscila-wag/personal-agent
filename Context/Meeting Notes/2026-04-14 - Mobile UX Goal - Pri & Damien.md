# Mobile UX Goal — Pri & [[Damien Kime]]
*2026-04-14 | ~17 min | [[Damien Kime]], Pri*

## Summary
Pri and [[Damien Kime]] worked through the metric definition for [[UVSG-1343]]. The LP activation dashboard in Looker doesn't split by platform by default, so the hypothesis that desktop users activate more after help couldn't be confirmed live. Damien will extract the split from Snowflake. Goal name locked pending data confirmation: *"Improve the mobile experience to hit desktop activation parity."*

## Decisions
1. **Primary metric**: Canva product activation rate within 24 hours of help usage (share/download/publish) — not help flow activation
2. **Goal scope**: Help assistant (AI help) only — not Help Center broadly
3. **Goal name**: "Improve the mobile experience to hit desktop activation parity" — contingent on Snowflake data
4. **Contingency**: If activation data doesn't support the hypothesis, Pri will agree a different goal name with stakeholders before Jira goal is created

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Extract Canva product activation rate split by platform from Snowflake | [[Damien Kime]] | [[UVSG-1343]] | Today (Apr 14, within 1hr of meeting) |
| 2 | Notify stakeholders data confirmation is in progress; adjust goal name if Snowflake data doesn't show desktop > mobile activation | Pri | [[UVSG-1343]] | Today (Apr 14) |

## Open Questions & Blockers
- **Does desktop activate more than mobile after help usage?** — Damien pulling from Snowflake to confirm. If yes, goal name stands. If no, needs renegotiation.
- **Intent skew risk**: Desktop help queries skew toward refunds/cancellations/print issues, which may inflate or deflate activation rates. Need like-for-like comparison to confirm metric is fair.

## Context
- Mobile help rate: **0.9%** vs desktop: **2%** — a significant gap [[Damien Kime]] flagged as the core problem
- Only **15% of mobile help users** return to help — poor retention signal, independent of the activation metric
- Mobile CSAT is *higher* than desktop — [[Damien Kime]]'s hypothesis: different intents (refunds/cancellations skew desktop, not mobile), not better quality
- Looker LP activation dashboard tracks product activation (share/publish/download) within 24hrs of help — this is the right metric, but underlying data isn't platform-split by default; requires Snowflake query
- Canva Create is reducing experiment load this week, creating bandwidth for this data work
- Friday will be a write-off (Canva Career event, keynote at 2pm — [[Damien Kime]] and team attending)
