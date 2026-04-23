---
title: HCF Standup — pre-long-weekend, Pat's last day
description: "Pre-long-weekend standup: no deploys before Tuesday, Pat on 3-week leave (back May 18), AutoML migration saves 40min pipeline, Contentful delta fetch proposed, Storylane mobile visuals due EOD."
type: meeting-note
created_date: 2026-04-23
---

# HCF Standup
*2026-04-23 | 30 min | Priscila, Tahlia, Yang Mi, Sophie Benjamin, Methun, Leo Kuang, David Nahodil, Carl Pritchett, Treble*

## Summary
Pre-long-weekend standup with standing directive: no deployments before Tuesday. [[Pat]] last day before 3-week leave (returns May 18). Multiple handoffs in flight — article backfill script, LLM readability doc, Storylane mobile visuals. Key tech highlight: AutoML migration will save 40 minutes in the translation pipeline; Contentful delta-fetch approach proposed to fix speed limit performance issues.

## Decisions
- **No deploys before Tuesday** — public holiday Monday; team mostly out
- **AutoML migration confirmed** — 99% of jobs finish under 60 seconds vs Smartling's current approach; saves ~40 min pipeline time. [[Sachini]] starts implementation Tuesday.
- **Contentful delta-fetch approach proposed** — instead of downloading everything from Contentful each run (causing speed limit hits), switch to delta-fetching. [[Kunday]] working on stakeholder alignment.
- **Affinity article backfill** — continue testing and rebase from master; trigger from Helpy directly once stable

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Reschedule end walkthrough to next Tuesday (FE engineers sick) | [[Tahlia]] | UVSG-615 | Mon/Tue |
| 2 | Run another round of tests on article backfill script from Affinity, rebase, publisher staging, tag Leo | [[Kunday]] | HELP-3090 | Today |
| 3 | Push current pipeline ticket to staging, complete test cases, prepare for release | [[Leo Kuang]] | HELP-3090 | Today |
| 4 | Discuss Slack notification change with Sashini on Tuesday; apply if approved | [[Leo Kuang]] | HELP-3090 | Tue |
| 5 | Take over 404 pages Affinity CM runner page card, review linked PR | [[Leo Kuang]] | HELP-4087 | Today |
| 6 | Find and link relevant PR for 404 pages Affinity CM runner page | [[Kunday]] | HELP-4087 | Today |
| 7 | Complete training with Mitch on category management, close task EOD | [[Pat]] | HELP-3820 | Today |
| 8 | Finish LLM readability doc draft and share with [[Lynette]] EOD | [[Pat]] | HELP-3222 | Today |
| 9 | Find Storylane support docs or responsible contact re: variant setup for Mitch | [[Kunday]] | HELP-3820 | After lunch |
| 10 | Merge multiple small observability metrics PRs into one PR | [[Kunday]] | HELP-3090 | Today |
| 11 | Complete mobile visuals for Storylane articles EOD | Treble | HELP-3820 | Today |
| 12 | Share handover documentation before leave | [[Pat]] | — | Today |
| 13 | Start Smartling job implementation for AutoML migration | Sachini | HELP-3090 | Tue |
| 14 | Write and share goal progress update deck with team | [[Tahlia]] | UVSG-615 | — |

## Open Questions & Blockers
- **Contentful performance** — during recent release, Canva Create, HC, and Affinity all hit Contentful speed limits simultaneously. Delta-fetch proposal needs stakeholder alignment before implementation.
- **Storylane variant setup** — Pat needs instructions for Mitch on how to set up variant content types; Kunday to source docs/contact this afternoon
- **404 pages Affinity CM runner** — Leo to review the linked PR for the correct approach (Kunday to find/link first)
- **Sachini on leave** — returns Tuesday; AutoML migration waits until then

## Context
- [[Pat]] on 3-week leave starting today; returns May 18
- [[Kunday]] out Monday, returns Tuesday. [[Leo Kuang]] also out Monday.
- Japan language team resolved translation issues independently — Leo reported they'll handle updates going forward
- Treble completed 3 Storylane articles + translations into Spanish and Portuguese in 2 days
- Long weekend: Anzac Day Monday (public holiday) — most Sydney team out
