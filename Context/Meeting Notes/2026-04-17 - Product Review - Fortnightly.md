---
title: Product Review - Fortnightly 2026-04-17
description: "Help Memory Milestone 2 prioritised; Unified KB POC greenlit; No Dead Ends (Canva AI + HA) launching this cycle; screen recording experiment scoped. 7 action items across Dom, Michelle/Matthew, Kerry, Sally."
type: meeting-note
created_date: 2026-04-17
---

# Product Review - Fortnightly
*2026-04-17 | ~70 min | [[Carl]], [[Matthew Baranauskas]], [[Dom]], [[Michelle]], [[Andi]], [[Kerry]], [[Sally]], [[Simone]], Pri, [[Lucas]] (left early)*

## Summary
Three initiatives moved forward at the fortnightly product review. [[Dom]] presented Help Memory Milestone 2 (targeting 6,000 monthly duplicate tickets/disconnected chats) and a Unified Knowledge Base POC to combine Help Center, Design School, and marketing content into a modular RAG layer for richer AI answers. [[Michelle]] and [[Matthew Baranauskas]] presented the "No Dead Ends" milestone under [[UVSG-615]] — seamless intent-based handoff between [[HC AI mode]] and Canva AI, launching this cycle. Key shift: user testing locked in before finalising Help Memory session model; unified KB approved as a "tool, not a merge" POC; No Dead Ends progressing to design review with Canva AI team.

## Decisions
- Help Memory priority order locked: (1) reconnect users to open specialist chats, (2) email ticket follow-ups, (3) Help Assistant session continuity; stretch goal is handover summaries to specialists — [[Dom]] / [[Andi]]
- User testing required before finalising Help Memory session model: build unbiased prototypes comparing "continue thread" vs "inbox model" — [[Andi]] called this explicitly
- Unified KB: Proceed with POC — select top 10 design intents, map against Design School/marketing content, build prototype RAG layer, validate with users — [[Dom]] / [[Andi]]
- Canva AI + HA: Launch "No Dead Ends" milestone this cycle with automatic intent-based handoff between Help Assistant and Canva AI — [[Michelle]] / [[Matthew Baranauskas]]
- Screen recording experiment: Target Chrome/Edge on Windows desktop first; run 3-variant experiment (fake door, native instructions, built-in recording) before broader investment — [[Kerry]]
- Two-chat problem: Acknowledged as a long-term architectural issue (two AI chats shouldn't coexist), but not scoped for this cycle — long-term vision is a unified panel — [[Matthew Baranauskas]] / [[Andi]]

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Schedule user interviews to test "continue thread" vs "inbox" session models for Help Assistant | [[Dom]] | [[UVSG-615]] | — |
| 2 | Build prototype RAG combining Help Center + Design School + YouTube content; map top 10 design intents; validate with users | [[Dom]] | [[HELP-3820]] | — |
| 3 | Complete design review with Canva AI team and internal stakeholders for unified interface; plan engineering work | [[Michelle]] / [[Matthew Baranauskas]] | [[UVSG-615]] | — |
| 4 | Validate with [[Lucas]] on front-end capacity for screen recording experiment; consider mobile-first approach due to iOS simplicity | [[Kerry]] | [[HELP-4139]] | — |
| 5 | Consult [[Jesse]] on Full Story integration as alternative/supplement to browser-based screen recording (5% sample already exists) | [[Kerry]] | [[HELP-4139]] | — |
| 6 | Follow up with [[Chelsea Nordstrom]] on Canva AI credit exhaustion → learning content handoff concept | [[Dom]] | [[UVSG-615]] | — |
| 7 | Review MarTech/Product Platform H2 goal on Canvas CMS overhaul for content infrastructure alignment | [[Sally]] | [[HELP-3090]] | — |

## Open Questions & Blockers
- **Two-chat problem**: Users can still open Canva AI and Help Assistant side-by-side — long-term vision needed for a single unified panel; live human chat + AI chat is the only valid side-by-side exception
- **Help Memory technical feasibility**: [[Jacob]] to re-explain why continuing ephemeral conversations (email inbox model) wasn't viable for chat history — flow progress storage complexity was cited but not fully explained
- **Unified KB content governance**: How to ensure Design School/marketing content stays current and doesn't erode trust — [[Andi]]'s framing: solve through UX (relevancy scoring + user choice), not content perfection
- **Screen recording cross-page**: Engineering not yet confirmed browser-based recording can follow users across Canva pages without breaking

## Context
- Canva Create aftermath: Team pushed content updates until 3am due to unclear Canva AI Pass messaging on social media; [[Carl]] noted help content should be finalised months before a launch, not days — pipeline timing issue
- Unified KB framing (important): "Tool, not merge" — a RAG layer that maps Design School/marketing content against top intents, callable by Help Center, Help Assistant, or Canva AI as a modular sub-agent
- Shared component library underway: input fields, loaders, and styling being unified between [[HC AI mode]] and Canva AI so handoffs feel seamless — foundational to No Dead Ends
- Mobile help entry points: [[Matthew Baranauskas]] proposing question mark icon in global header on home/settings — currently impossible to access help from [[Mobile Help UX]] mobile settings without navigating away
- [[Sally]] flagged: MarTech/Product Platform have an H2 goal to overhaul Canvas CMS into a proper content infrastructure — could be a significant enabler for [[AI-First Help Center]] Unified KB POC
- Mobile screen recording simpler than expected: iOS has a native parameter — [[Simone]] confirmed
