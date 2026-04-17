# Product Review - Fortnightly
*2026-04-17 | ~70 min | [[Carl]], [[Matthew Baranauskas]], [[Dom]], [[Michelle Huang]], [[Kerry Zhang]], [[Andi Schuster]], [[Sally Bagshaw]], [[Simone Attanasio]], [[Lucas]], [[Pri]]*

## Summary
Three major initiatives landed: Help Memory Milestone 2 ([[UVSG-633]]) to address 6,000 duplicate tickets/disconnected chats monthly by building on prior help sessions; a Unified Knowledge Base POC to combine [[HC AI mode]], Design School, and marketing content for richer AI answers ([[HELP-3820]], [[HELP-4370]]); and the Canva AI + [[HA]] "No Dead Ends" milestone ([[UVSG-1350]]) to eliminate routing dead ends via intent-based handoffs and a shared component library. All three got green lights with user testing and a three-variant screen recording experiment as next validation steps.

## Decisions
- **Help Memory prioritisation locked**: open chat reconnection first → email ticket follow-ups → HA-to-HA session continuity → handover summaries to specialists (stretch). Ordered by urgency and complexity — [[Dom]] / [[Andi Schuster]]
- **User testing required before finalising HA session management model**: run unbiased prototypes comparing "continue old thread" vs "inbox model" — don't hypothesise, speak to users. [[Andi Schuster]] call; [[Dom]] to run
- **Unified Knowledge Base POC approved**: select top 10 design intents, map against Design School + YouTube content, build a prototype RAG layer, test with users before any content infrastructure decisions — [[Dom]]
- **No Dead Ends milestone this cycle**: automatic intent-based handoff from HA → Canva AI (and back); shared component library (input fields, loaders, styling); soft-start replaces splash screen; content push-over UX — [[Michelle Huang]] / [[Matthew Baranauskas]]
- **Screen recording experiment**: target Chrome/Edge on Windows desktop initially; three-variant test (fake door / native instructions / built-in recording) to validate value before further investment — [[Kerry Zhang]] / [[Lucas]]

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Schedule user interviews to test "continue thread" vs "inbox" models for HA session management | [[Dom]] | [[UVSG-1332]] | — |
| 2 | Build prototype RAG combining HC + Design School + YouTube; map top 10 design intents; validate with users | [[Dom]] | [[HELP-4370]] 🔗 | — |
| 3 | Complete design review with [[Canva AI]] team and internal stakeholders for unified interface; plan engineering work | [[Michelle Huang]] / [[Matthew Baranauskas]] | [[UVSG-1350]] 🔗 | — |
| 4 | Validate with [[Lucas]] on front-end capacity for screen recording experiment; consider mobile-first given iOS simplicity | [[Kerry Zhang]] | [[HELP-4139]] | — |
| 5 | Consult [[Jesse]] on Full Story integration as alternative/supplement to browser-based screen recording | [[Kerry Zhang]] | [[HELP-4139]] | — |
| 6 | Follow up with [[Chelsea Nordstrom]] on Canva AI credit exhaustion → learning content handoff concept | [[Dom]] | [[UVSG-615]] | — |
| 7 | Review MarTech/Product Platform H2 goal on Canvas CMS overhaul for content infrastructure alignment | [[Sally Bagshaw]] | [[HELP-3820]] | — |
| 8 | Re-explain to [[Andi Schuster]] why continuing ephemeral conversations (inbox model) wasn't viable for chat history due to flow progress storage complexity | [[Jacob]] | [[UVSG-1332]] ⚠️ | — |

## Open Questions & Blockers
- **Two-chat problem unresolved**: users can still open [[Canva AI]] and [[HA]] side-by-side; long-term solution needed — both [[Andi Schuster]] and [[Matthew Baranauskas]] agree it shouldn't stay this way, but out of scope this cycle
- **Content governance gap**: how to ensure Design School/marketing content in the unified knowledge base stays current and doesn't erode trust — [[Michelle Huang]] and [[Andi Schuster]] flagged; UX approach (let user pick relevance rather than forcing one right answer) suggested as mitigation
- **Mobile help entry points**: top-right `?` button on home/settings vs. buried menu navigation on mobile — [[Matthew Baranauskas]] flagged; needs platform buy-in for global header on home/settings
- **Chat history technical feasibility**: [[Jacob]] to re-explain why the inbox model (continue old session) wasn't viable due to how flow progress is stored — [[Andi Schuster]] unconvinced; needs a clearer technical explanation before architecture is locked

## Context
- Canva Create aftermath: [[Carl]]'s team was pushing content updates until 3am for Canva AI Pass messaging that blew up on social media — plan is to scrap remaining pipeline milestones and reevaluate what improvements matter most for engineers and content ops
- Help Memory architecture: memory service will store help journey data separately from product event data; available via API even if not surfaced on front-end — other teams can call it regardless
- Screen recording browser constraints: Safari unsupported; Chrome on Mac requires browser restart on first use; tab-switching in Windows ends recording — mitigate with browser targeting and expectation setting; [[Simone Attanasio]] confirmed iOS is actually simpler (native parameter available), making mobile-first viable
- Unified Knowledge Base: Marketing's [[Canvas CMS]] was purpose-built for their needs and won't migrate to Contentful without proof of value — POC must come first; [[Sally Bagshaw]] flagged an H2 MarTech goal on CMS overhaul that may provide infrastructure alignment
- [[UVSG-1350]] (No Dead Ends) was only created 2026-04-16 — very fresh milestone; design review and engineering planning are the immediate next steps
