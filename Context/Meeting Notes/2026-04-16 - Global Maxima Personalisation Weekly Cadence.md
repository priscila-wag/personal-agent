---
title: Global Maxima Personalisation Weekly Cadence 2026-04-16
description: "Pri's help-assisted personalisation goal removed from GM stream; Rosetta, HA glossary, and role personalisation approved for full rollout; Policy Agent at 50% targeting 100% next week."
type: meeting-note
created_date: 2026-04-16
---

# Global Maxima: Personalisation Weekly Cadence
*2026-04-16 | ~30 min | [[Yshana Wong]], [[Lucas]], [[Allison Wahl]], [[Jacob Foley]], [[Callum McKay]], [[Arveen Azurin]], [[Nee]], [[Priscila Wagner]], [[Danne Lim]], [[Linette Voller]]*

## Summary
Pri's help-assisted personalisation goal has been officially descoped from the Global Maxima stream and will move to goal alignment tracking only, now focused exclusively on increasing logged-in sessions — confirmed by Pri and [[Danne Lim]] as the right call given the goals no longer overlap. Multiple personalisation experiments are clearing for full rollout: Rosetta specialist translator, HA glossary, and role personalisation all show positive directional signals (including reduced Zendesk tickets) despite mostly non-significant primary metrics. [[Policy Agent]] is at 50% Omniagent rollout targeting 100% next week post-Canva Create, with the escalation feature cleared for staging.

## Decisions
- **Pri's goal removed from Global Maxima stream** — [[UVSG-614]] focuses on login sessions, not personalisation delivery; tracked via goal alignment only from now on. [[Danne Lim]] and Pri agreed the overlap no longer exists; H2 personalisation work will be the right home for future alignment.
- **Rosetta specialist translator approved for full rollout** — eval results positive on 1–4 scale across locales; rolling out to all owned languages for email and chat.
- **HA glossary experiment approved for full rollout** — mostly non-significant but reduced Zendesk ticket creation and invisible-good-translation hypothesis validated. Rolling to all owned languages.
- **Role personalisation proceeding to full rollout** — DS guidance supports rollout despite lack of statistical significance; success metrics trending right for team-leaning intents; guardrails safe. (Note: incorrect pilot split inadvertently concluded experiment — [[Nee]] seeking permission for full rollout.)
- **Policy Agent escalation feature cleared design LTGM** — moving to staging for Trust and Safety sign-off before HA rollout.
- **Omniagent Policy Agent targeting 100% rollout** — as early as next week post-Canva Create; HA escalation is next in queue after Omniagent completes.

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Add deck for Global Maxima highlights by tomorrow for team input | [[Yshana Wong]] | [[HELP-3090]] | 2026-04-17 |
| 2 | Announce Pri's goal removal from GM stream at next week's call | [[Yshana Wong]] | [[HELP-3090]] | 2026-04-23 |
| 3 | Track additional personalizations above 118 target in governance system | [[Yshana Wong]] | [[HELP-3090]] | — |
| 4 | Map out additional HubMemory M2 work to flag deadline risks early | [[Lucas]] | [[HELP-3090]] | — |
| 5 | Add "Do you need help content?" step to experiment rollout checklist | [[Lucas]] | [[HELP-3090]] | — |
| 6 | Get Rosetta LTGM approvals and roll out to all languages for email/chat | [[Arveen Azurin]] | [[HELP-3090]] | — |
| 7 | Work with Daniel to store specialist translated prompts in Lang Views for editing | [[Arveen Azurin]] | [[HELP-3090]] | — |
| 8 | Complete translation glossary quality review in Lang Views before full rollout | [[Nee]] | [[HELP-3090]] | — |
| 9 | Select next locales for glossary expansion | [[Nee]] | [[HELP-3090]] | — |
| 10 | Complete end-to-end refunds tool testing and enable full shadowing next week | [[Callum McKay]] | [[HELP-3090]] | — |
| 11 | Roll out [[HA]] escalation feature to staging for Trust and Safety approval | [[Jacob Foley]] | [[HELP-4319]] | — |

> **Note for Pri:** No direct action items from this meeting. Two items worth tracking as context:
> - Item 5 (Lucas's help content checklist step) directly affects HC content team workflow — worth following up with Lucas post-Create.
> - Item 11 (HA escalation to staging) is a near-term dependency for [[logged-out HA]] work under [[HELP-4319]].

## Open Questions & Blockers
- **HubMemory M2 deadline at risk (May 30)** — unexpected work (live chat history, support service delays) may push beyond target; prod review tomorrow with [[Allison Wahl]] and [[Lucas]] to discuss scope reduction or deadline extension.
- **Crisis line integration** — LLMs hallucinate crisis hotline numbers; need API with external service or internal database; Trust and Safety to weigh in on preferred approach. [[Jacob Foley]] investigating.
- **Auto-escalation for minors** — no current mechanism to escalate minors without user consent; legal ([[Andi]]) reviewing strict requirements. Potential new feature if legal says mandatory.
- **Feature flag personalisation feasibility** — Linette flagged post-Create exploration to scope feature-flag-based personalisation as potential H2 work; pilot team interested. No owner yet.
- **Control panel build vs buy** — design doc for UI requirements in progress; decision expected mid-cycle.
- **Role personalisation experiment**: incorrect pilot split inadvertently concluded experiment; [[Nee]] seeking full rollout permission.

## Context
- **[[Canva Create]] context**: the Canva AI 2.0 personalisation was deployed via a brute-force quick fix — feature flag + locale check + admin permissions. This reignited interest in feature-flag-based HC personalisation at scale.
- **[[UVSG-614]] update**: Pri confirmed the first "Try In My Design" login experiment ran with only 15 articles and delivered +0.14% login sessions — directionally strong. Doubling down on this approach for H1.
- **H2 personalisation setup**: [[Linette Voller]] flagged a cross-team content variants workshop next week led by [[Sally]] — directly relevant to Pri's H2 personalisation planning (noted in [[GOALS.md]] opportunity for Apr 20 workshop). No action required but prep for H2 scope position is valuable.
- **Personalisation taxonomy**: Jacob described using Contentful "experiences" as long-lasting taxonomy markers — content and users both tagged when new features roll out. This is the emerging standard for feature-flag HC personalisation.
- **Rosetta + voice/tone milestone**: with Rosetta's launch ingesting Canva style guides in-language, a large portion of voice/tone personalisations will arrive as a side-effect — helping Arveen's team hit 118+ personalisations by April.
