# Langfuse HC AI Mode Set Up
*2026-04-21 | 25 min | [[Dean Soste]], [[Pat Santos]], [[Tahlia]], [[Priscila Wagner]]*

## Summary
[[Dean Soste]] walked the HC team through Langfuse tracing and LLM-as-judge methodology for automating quality monitoring across the HC's AI surfaces (help assistant, search bar, AI summaries, AI mode). The key shift: move from reactive bug discovery (potentially weeks after a regression) to proactive alerting within days. The approach — manual annotation first, then LLM judges calibrated to human scoring — gives the HC team genuine ownership over prompt quality on their surfaces without depending on platform teams to catch issues.

## Decisions
- **Prompt ownership:** HC team owns and can modify prompts specific to their surfaces in Langfuse — including `Magic Answers Help Center Content-Based Unrestricted` versions ([[Dean Soste]])
- **Annotation-first:** Team will manually score traces before automating with LLM judges — calibration must match human judgment before automation
- **Surface-specific prompts:** Each AI surface (search bar, help assistant, article summaries, AI mode) requires tailored prompts with feature localisation components — current shared prompts causing tone mismatches

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Create inventory of 5–10 quality concerns across 4 surfaces (help assistant, search bar, AI summaries, AI mode) — tone, escalation paths, context appropriateness | Pri, [[Tahlia]], [[Pat Santos]] | [[UVSG-615]] | — |
| 2 | Set up annotation queue with custom scores targeting identified quality concerns | [[Dean Soste]] | [[UVSG-615]] | — |
| 3 | Compile list of problematic trace examples — start with "contact support" intent and AI summary tone issues | Pri, [[Tahlia]] | [[UVSG-615]] | — |
| 4 | Schedule follow-up session: walk through annotation queue, demonstrate how to assign scores + add traces | [[Dean Soste]] | [[UVSG-615]] | — |
| 5 | After annotation complete: build LLM-as-judge to auto-monitor and score production traces | [[Dean Soste]] | [[UVSG-615]] | — |

## Open Questions & Blockers
- **Code-based content drafting:** Pri proposed reading code at experimentation phase to auto-generate content drafts using AI — Dean flagged challenges: thousands of feature flags create multiple code paths, agentic systems generate non-deterministic outputs. Not resolved.
- **Contact support intent:** When users express intent to contact support, assistant suggests reaching out but provides no actual mechanism — open UX gap that needs escalation path designed
- **Sahil's browser agent verification:** Exists but is reactive (not PR-based) — potential future integration with annotation pipeline

## Context
- **Current AI surfaces owned by HC team:** Help assistant (in HC), Magic Answers (search bar), AI summaries (article tops) — 204,000+ observations for content-based unrestricted prompt alone
- **Problems surfaced:** (1) Canva Create launch included features (memory, scheduled tasks) disclosed days before launch — forced rushed content across teams; (2) Search bar tone mismatch — assistant uses conversational language where users can't respond; (3) AI summaries inherited in-product prompts causing "I can see you are not on a website right now" responses in HC context
- **Model:** GPT-4 (2025 version) for content generation; parameters visible in traces
- This work directly supports [[HC AI mode]] quality evaluation framework — a key output of [[UVSG-615]] and [[AI-First Help Center]]
- Langfuse tracing capability is the foundation for the eval framework Pri needs to demonstrate as part of the UVSG-615 milestone
