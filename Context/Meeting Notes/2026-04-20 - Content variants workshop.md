---
title: Content variants workshop
description: Personalization methods audit across HA and HC — 7 methods consolidated to 3 core approaches. Decisions on Control Panel as transformation layer, taxonomy as preferred model, localization scoped separately. 10 attendees."
type: meeting-note
created_date: 2026-04-20
---

# Content variants workshop
*2026-04-20 | 1h 50m | [[Yshana Wong]], [[Priscila Wagner]], [[Marlene Ensor]], [[Linette Voller]], [[Laura Derman]], [[Kunday]], [[Jacob Foley]], [[Danne Lim]], [[Arveen Azurin]], [[Alex Nucera]]*

## Summary
The workshop audited the 7 personalisation methods currently scattered across [[Help Assistant]] and [[Help Center]], surfacing critical gaps — no shared personalisation between surfaces, and Content Ops unable to make changes without engineering involvement each time. The team landed on an architecture direction: consolidate to 3 core methods, use [[Control Panel]] as the translation layer between Canva-wide user attributes and UV-specific personalisation, and shift country/locale-based content to [[taxonomy]] as the primary model. Localisation pipeline work remains scoped separately. Clear 6-month and 1-year targets were set; action items distributed across the team for May 8 multi-agent planning.

## Decisions
- **Consolidate over expand**: Stop creating new personalisation approaches — align the team on 3 core methods going forward
- **Control Panel as transformation layer**: Use Control Panel to translate Canva-wide user attributes into UV-specific personalisation, enabling consistent definitions across [[Help Assistant]] and [[Help Center]]
- **Taxonomy as preferred model**: Shift country-based and structured personalisation to taxonomy for consistency and maintainability; reduce free text limitations and prompt logic
- **Localisation scoped separately**: Translation quality and pipeline improvements stay in the [[Content Pipeline]] project, not this personalisation workstream

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Share meeting recording, transcript, and summary in GlobalMax personalization channel | [[Sally]] | [[HELP-3090]] | — |
| 2 | Create terminology one-pager: locale, country, language, regionalization, static vs dynamic personalisation | [[Laura Derman]] | [[HELP-3090]] | — |
| 3 | Incorporate personalisation requirements into multi-agent foundation/knowledge layer planning for May 8 presentation | [[Laura Derman]] + [[Jacob Foley]] | [[UVSG-615]] | May 8 |
| 4 | Share early thinking document on Help Assistant personalisation consolidation | [[Linette Voller]] | [[UVSG-615]] | — |
| 5 | Address translation solution in content pipeline project (currently blocking pipeline work) | [[Kunday]] + Pri | [[HELP-3090]] | — |
| 6 | Continue expanding taxonomy-based personalisation to reduce prompt logic and free text limitations | [[Jacob Foley]] + Pri | [[HELP-3222]] | — |
| 7 | Work with Michelle to apply OmniAgent localization layer approach to Help Assistant | [[Arveen Azurin]] | [[HELP-3090]] | — |

## Open Questions & Blockers
- **Change management at scale**: When a lock triggers content updates, how are regional content owners notified to update their variants?
- **HC translation approach**: Should HC adopt HA's on-the-fly LLM translation (higher CSAT) or keep SmartLink (version control, quality)? Currently inconsistent.
- **Overlapping personalisations**: How do LLMs handle content available on Pro but not in Japan, with usage limits — multiple conditional rules compound?
- **SEO**: All content must remain indexable even if dynamically personalised for logged-in users — front-end capability not yet built
- **Terminology alignment**: Locale vs country vs language definitions still inconsistent across teams (Laura's one-pager addresses this)
- **Multi-brand workspace consolidation**: Confidence needed that content can be properly segregated before merging Canva, Affinity, and future brands into one Contentful workspace
- **HC dynamic personalisation**: Front-end capability to show personalised content for logged-in users not yet built

## Context
- **7 personalisation methods identified**: taxonomy, availability fields, experiment variants, Control Panel variants, prompt logic, free text limitations (HA + HC), and audience variants (HC only — used for Affinity China, ~3 weeks per new attribute)
- **No shared personalisation between surfaces**: HA and HC require separate implementations for the same need (e.g., Japan-specific content) — the unified knowledge layer vision addresses this
- **6-month target**: Parity in HC personalisation capabilities (currently behind HA). **1-year target**: Content Ops writes once, personalises once, consistent output across all surfaces without per-change engineering
- **Japan BPO success signal**: 6 language experts expanding to additional locales in H2; Rosetta rollout imminent (per-locale LLM selection, prompt customisation, SmartLink glossary integration)
- **[[HC AI Mode]] / [[AI-First Help Center]] connection**: This workshop directly feeds H2 personalisation scoping — shapes what gets committed to the roadmap next cycle
