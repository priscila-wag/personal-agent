# Align on goal progress: Integrated Help Assistant and Help Center
*2026-04-21 | 30 min | [[Tahlia Giann]], [[Simone Attanasio]], [[Matthew Baranauskas]], [[Priscila Wagner]]*

## Summary
[[Tahlia Giann]] walked through the full milestone status for [[UVSG-615]] ahead of Goal Alignment. The AI mode MVP (search → AI-first chat) is on track for a May 15 experiment. Key trade-off confirmed: "Ask about this page" moved to H2 due to 3-week backend dependency on Hype Engineering. The goal name changed from "Personalized Help Center" because back-end capacity prevented personalisation — all remaining milestones are front-end and tied to increasing logged-in sessions.

## Decisions
- **AI mode MVP over "Ask about this page"** — Ask about this page deferred to H2; AI mode MVP is the H1 delivery target (May 15 experiment). [[Tahlia Giann]] + [[Simone Attanasio]]
- **Goal renamed** from "Personalized Help Center" — back-end capacity blocked personalisation; front-end milestones kept as they support logged-in session growth
- **Help Assistant FAB to be removed from search pages** once AI mode experiment validates — dual chat creates competing interests
- **GA prep automation** — use Canva's task scheduler with Jira integration + template to auto-generate presentations; reduces manual effort for future GA cycles. Pri proposed to Eva; to be implemented

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Get second LGTM for deep links milestone (M2) — 1 of 2 received | [[Tahlia Giann]] | [[UVSG-615]] | Before May 15 |
| 2 | Finalise "Ask about this page" designs + get LGTM ready for H2 handoff | [[Tahlia Giann]] / Priya | [[UVSG-615]] | — |
| 3 | Explore UI improvements for article hierarchy issues (KTLO) — Canva AI 2.0 articles have ~20 anchors at top, broken mobile hierarchy | [[Tahlia Giann]] | [[UVSG-615]] | — |
| 4 | Propose GA prep automation to Eva — Canva task scheduler + Jira integration + template for auto-generating presentations | Pri | [[UVSG-615]] | — |
| 5 | Increase visibility of shipped milestones — tag to rollout channel or equivalent | Pri / [[Simone Attanasio]] | [[UVSG-615]] | — |

## Open Questions & Blockers
- **Dual chat resolution** — depends on a component not yet available; no timeline. Blocks solving the competing Help Assistant FAB + AI mode chat experience
- **"Ask about this page"** — 3-week backend dependency on Hype Engineering confirmed by Sergey; deferred to H2. Priya + Tahlia to finalise designs in the meantime
- **Vision for Help Center (full screen chat, visuals/assets)** — concepts only; depends on Canva AI + HA integration patterns and AI mode experiment results
- **AI mode MVP is NOT powered by Help Assistant yet** — no conversational memory, no context carry-through between questions. Foundational step only; full HA integration is next cycle

## Context
- [[UVSG-615]] goal milestone summary as of 2026-04-21:
  - ✅ Split screen view — launched 100% desktop
  - ✅ Four-level IA — launched, +1% month-on-month uplift
  - ✅ Try My Design Phase 2 — in rollout, 8% CTR, 75% new user adoption, 7.5% uplift
  - ✅ User research for AI mode — completed and synthesised
  - 🔨 Launch MVP user-driven search vs AI mode — experiment May 15
  - 🔨 Implement triggering deep links — LGTM 1/2 received
  - 🔍 Solving dual chat — blocked on missing component
  - 🔍 Vision for Help Center — concepts only
  - 🔍 KTLO article refresh — exploring
  - ➡️ Ask about this page — moved to H2
- Try My Design Phase 2 shipped by [[Jenna]] within last few days of this meeting
