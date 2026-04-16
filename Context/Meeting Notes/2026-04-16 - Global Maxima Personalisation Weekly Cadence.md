---
title: Global Maxima Personalisation Weekly Cadence — 2026-04-16
description: "Pri's help-assisted personalisation goal descoped from Global Maxima stream; all H1 personalisation milestones removed, focus shifts to logged-in session increases only."
type: meeting-note
created_date: 2026-04-16
---

# Global Maxima Personalisation Weekly Cadence
*2026-04-16 | ~30 min | [[Yshana Wong]], [[Lucas]], [[Allison Wahl]], [[Jacob Foley]], [[Callum McKay]], [[Arveen Azurin]], [[Nee]], [[Linette Voller]], [[Danne Lim]], [[Sally]] (next week), Priscila Wagner*

## Summary
Pri's help-assisted personalisation goal is formally removed from the Global Maxima stream — all H1 personalisation milestones descoped, with [[UVSG-614]] now focused exclusively on increasing logged-in HC sessions. The first login incentive experiment (Try In My Design) already shows +0.14% increase across just 15 articles, validating the direction. The rest of the stream is tracking well: Rosetta specialist translations approved for full rollout, glossary experiment wrapping up, role personalisation moving to full rollout.

## Decisions
- **Pri's goal removed from GM stream** — help-assisted personalisation moves to goal-alignment-only tracking. No overlap with current GM personalisation delivery work; [[UVSG-614]] focus is login sessions, not personalisation variants. [[Yshana Wong]] to announce at next week's GM call.
- **Rosetta specialist translator: full rollout approved** — evals show consistently better translation quality (1–4 scale) across locales; rolling out to all languages for email and chat. ([[Arveen Azurin]])
- **Help Assistant glossary experiment: full rollout approved** — mostly non-significant results, but reduced Zendesk tickets and invisible-good-translation hypothesis supports rollout to all owned languages. ([[Nee]])
- **Role personalisation: full rollout approved** — success metrics trending positively for team-leaning intents; DS guidance and safe guardrails support rollout despite lack of statistical significance. ([[Nee]])
- **Policy Agent escalation feature: Design LTGM done** — moving to staging for Trust and Safety sign-off before prod rollout. ([[Jacob Foley]])
- **Omniagent Policy Agent scaling to 100%** — currently at 50%; targeting 100% as early as next week post-Canva Create. ([[Jacob Foley]])

## Action Items

No action items for Pri from this meeting.

*Other team action items (for reference):*

| Owner | Task | Due |
|-------|------|-----|
| [[Yshana Wong]] | Add deck for GM highlights by tomorrow for team input | 2026-04-17 |
| [[Yshana Wong]] | Announce Pri's goal removal from GM stream at next week's call | 2026-04-23 |
| [[Yshana Wong]] | Track additional personalizations above 118 target in governance system | — |
| [[Lucas]] | Map out additional HubMemory M2 work to flag deadline risks early | — |
| [[Lucas]] + Pilot team | Add "Do you need help content?" step to experiment rollout checklist | — |
| [[Arveen Azurin]] | Get Rosetta LTGM approvals and roll out to all languages for email/chat | — |
| [[Arveen Azurin]] | Work with Daniel to store specialist translated prompts in Lang Views | — |
| [[Nee]] | Complete translation glossary quality review in Lang Views before full rollout | — |
| [[Nee]] | Select next locales for glossary expansion | — |
| [[Callum McKay]] | Complete end-to-end refunds tool testing; enable full shadowing next week | 2026-04-23 |
| [[Jacob Foley]] | Roll out Help Assistant escalation to staging for Trust and Safety approval | — |
| [[Jacob Foley]] | Monitor escalation ticket volumes during HA rollout | — |
| [[Jacob Foley]] | Explore crisis line API options with Trust and Safety | — |

## Open Questions & Blockers
- **HubMemory M2 deadline at risk (May 30)** — unexpected work (live chat history, support service delays) may push delivery; prod review scheduled to discuss scope reduction or extension. [[Allison Wahl]] perspective: May 30 was set before full goal discovery — extending to deliver more value may be right.
- **Role personalisation experiment data issue** — incorrect pilot split correction inadvertently concluded the experiment; seeking permission for full rollout as a workaround.
- **Crisis line integration** — LLMs hallucinate hotline numbers; needs API integration with an external always-updated database or an internal one. Trust and Safety to advise.
- **Auto-escalation for minors** — no current pattern to auto-escalate without user consent when a minor self-identifies; legal reviewing strict requirements.
- **Feature flag personalisation feasibility** — [[Linette Voller]] flagged worth scoping for H2; pilot team interested. Size unknown.

## Context
- Pri attended to formally confirm the goal descoping, then will drop off after next week's announcement. No further obligations to this cadence.
- H2 personalisation (user attribute-based variants, content variants by feature flag) is where Pri's team will re-engage with GM stream. [[UVSG-614]] login session focus is the H1 unlock for this.
- The personalisation workshop next week (led by [[Sally]]) is about content variant handling in Contentful — relevant to [[HCF]] and [[Content Automation]] work. Consider sending a rep given H2 alignment implications.
- [[Linette Voller]] running a post-Create retro on HC/HA content alignment gaps — HA didn't have all necessary content before Create. [[HCF]] process issue worth monitoring.
- Lucas's proposal to add a help-content check to the Pilot experiment rollout checklist is a low-effort systemic fix for recurring content-experiment misalignment. Worth supporting.
