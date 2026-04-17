---
title: Product Review - Fortnightly
description: "Three H1 initiatives: Help Memory M2 (6k duplicate tickets/month), Unified KB POC (HC + Design School + marketing), No Dead Ends Canva AI + HA integration. Decision to user-test session management models before building."
type: meeting-note
created_date: 2026-04-17
---

# Product Review - Fortnightly
*2026-04-17 | ~70 min | [[Carl]], [[Dom]], [[Matthew Baranauskas]], [[Michelle Huang]], [[Kerry Zhang]], [[Andi Schuster]], [[Sally Bagshaw]], [[Simone Attanasio]], Pri*

## Summary
Three interconnected initiatives presented this cycle: [[Help Memory]] Milestone 2 to close 6,000 monthly duplicate tickets and disconnected chats via session continuity; a Unified Knowledge Base POC to combine Help Center, Design School, and marketing content into a single AI answer layer; and the "No Dead Ends" milestone for [[UVSG-615]] launching this cycle, creating seamless intent-based handoffs between [[Help Assistant]] and Canva AI. All three advance the same direction: a connected, context-aware [[AI-First Help Center]]. Key decision: user-test "continue thread" vs inbox models before locking Help Memory session UX.

## Decisions
- **Help Memory priorities locked:** (1) reconnect open chats → (2) email ticket follow-up detection → (3) HA-to-HA session continuity; stretch goal = handover summaries to specialists — [[Dom]]
- **User testing required:** Run unbiased prototypes comparing "continue old thread" vs "inbox model" for Help Assistant session management before finalising approach — [[Andi Schuster]] call, [[Dom]] agreed
- **Unified Knowledge Base:** Proceed with POC — select top 10 design intents, map against Design School + marketing content, build prototype RAG layer, test with users — [[Dom]]
- **No Dead Ends milestone:** Launch this cycle with automatic intent-based handoff between Help Assistant and Canva AI — [[Michelle Huang]] / [[Matthew Baranauskas]]
- **Screen recording:** Start with Chrome/Edge on Windows desktop only; run three-variant experiment (fake door, native OS instructions, built-in recording) to validate value before broader investment — [[Kerry Zhang]]
- **Mobile optimization:** Screens from the unified HA/Canva AI design to be handed off to mobile optimization goal team for further refinement — [[Matthew Baranauskas]]

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Schedule user interviews to test "continue thread" vs "inbox model" for HA session management | [[Dom]] | [[UVSG-615]] | — |
| 2 | Build prototype RAG combining Help Center + Design School + YouTube content; map top 10 design intents; validate with users | [[Dom]] | [[HELP-3820]] | — |
| 3 | Complete design review with Canva AI team and internal stakeholders for unified HA/Canva AI interface; plan engineering work | [[Michelle Huang]] / [[Matthew Baranauskas]] | [[UVSG-615]] | This cycle |
| 4 | Validate front-end capacity with [[Lucas]] for screen recording experiment; consider mobile-first approach given iOS simplicity | [[Kerry Zhang]] | [[HELP-4139]] | — |
| 5 | Consult [[Jesse]] on Full Story integration (5% sample) as alternative or complement to browser-based screen recording | [[Kerry Zhang]] | [[HELP-4139]] | — |
| 6 | Follow up with [[Chelsea Nordstrom]] on Canva AI credit exhaustion → learning content handoff concept | [[Dom]] | [[HELP-3820]] | — |
| 7 | Review MarTech/Product Platform H2 goal on Canvas CMS overhaul for content infrastructure alignment | [[Sally Bagshaw]] | [[HELP-3820]] | — |

## Open Questions & Blockers
- **Two-chat problem unresolved:** Users can still open Canva AI and Help Assistant side-by-side. Long-term the right answer is a single panel — not in scope this cycle. Needs a future vision artifact to make the problem tangible before it can be properly debated.
- **Help Memory technical feasibility:** [[Jacob]] to re-explain why continuing ephemeral conversations (inbox model) wasn't viable due to flow progress storage complexity — [[Andi Schuster]] pushed for a clearer answer.
- **Content governance:** How to ensure Design School/marketing content in the unified knowledge base stays current. Outdated content creates trust issues; UX may need to present options rather than one "best" answer.
- **Help entry point on mobile:** Whether mobile home/settings should use a top-right question mark for easier access vs buried menu — mentioned but not resolved.

## Context
- **Canva Create aftermath:** Team pushed content updates until 3am due to unclear Canva AI Pass messaging blowing up on social media. [[Carl]] flagging this as a pipeline timing problem — Canva AI should get help content out months earlier, not days. Connects to [[Content Automation]] goal.
- **Help Memory architecture:** Memory service stores help journey data separately from product event data; available via API for other teams even if not exposed in the front-end. Non-zero cross-team value even before front-end ships.
- **Screen recording browser constraints:** Safari unsupported; Chrome on Mac requires browser restart on first use; Windows tab-switching can end recordings. iOS via native parameter is actually simpler — [[Simone Attanasio]] flagged this as easier to implement than desktop.
- **Unified interface components:** Moving to shared component library between [[Help Assistant]] and Canva AI (input fields, loaders, soft-start UX) to make handoffs feel seamless. HA has a separate type system from Canva AI 2.0 — this design work retires that debt.
- **Canva AI credit exhaustion → learning handoff:** When users exhaust AI credits, there's a natural moment to hand off to Help/Design School learning content. [[Chelsea Nordstrom]] flagged as adjacent but distinct from the Unified KB work — may be two separate exploration threads.
