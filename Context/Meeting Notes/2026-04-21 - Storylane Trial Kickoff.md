# Storylane Trial Kickoff <> Canva
*2026-04-21 | 60 min | [[Jackson]] (Storylane), [[Tahlia]], [[Vinod]], [[Sahil]], [[Treble]], [[Sally Bagshaw]], [[Priscila Wagner]]*

## Summary
Kick-off session for the 14-day Storylane trial, focused on configuring the workspace and creating the first two interactive training demos. The team aligned on a support-tone, tooltip-with-backdrop-spotlight design style (not the default hotspot circles), and confirmed the two success metrics that will determine if Storylane earns a full adoption: user desirability (traffic/engagement impact when demos are embedded in articles) and throughput (content creation speed vs current screenshot workflow). Treble (Manila) owns workspace creation; demos persist post-trial if Canva upgrades.

## Decisions
- **Demo style:** Tooltips with backdrop spotlight animations — not default hotspot circles ([[Jackson]] + team)
- **AI tone:** Set to "Support" not "Marketing" — training context requires different register
- **No intro cards:** Remove title/intro cards from all demos — no value in HC context
- **CTAs:** "Rewatch" (loops to step 1) and "Keep Learning" (continues to next module) — replace sales CTAs
- **Autoplay:** 5-second autoplay between steps enabled so users can watch passively
- **Multi-chapter structure:** Related workflows organised as chapters within single demo projects with progress tracking + strikethrough completion markers

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Send Canva font files to Jackson via existing email thread | [[Treble]] | [[HELP-3090]] | — |
| 2 | Send call recording, recap email, resources + create Slack channel for Q&A | [[Jackson]] | — | — |
| 3 | Upload Canva font files to workspace once received | [[Jackson]] | — | — |
| 4 | Build training demos for HC articles during 14-day trial | Team | [[HELP-3090]] | End of trial |
| 5 | Embed demos in HC articles; measure traffic and engagement impact (user desirability test) | Pri / [[Tahlia]] | [[HELP-3090]] | — |
| 6 | Schedule follow-up working session end of this week or early next week | [[Jackson]] | — | CW17 end |
| 7 | Confirm with Jackson until when demos created during trial are accessible | Pri | [[HELP-3090]] | Tomorrow |

## Open Questions & Blockers
- **Rounded corners:** Product team evaluating whether spotlight animations can have rounded corners to match Canva's design language — not confirmed
- **Video-to-demo converter:** Feature launching May 2025 — can upload existing screen recordings with auto click detection + tooltip generation (potential throughput accelerator)
- **Video clip insertion:** Desktop app video recording didn't capture properly during session — Storylane product team investigating
- **How many articles to focus on?** Pri proposed 3–5 articles max to validate user desirability; Treble can work on more for throughput validation in parallel (see Slack thread #tmp-poc-storylane)

## Context
- [[Storylane]] POC relates to [[HELP-3090]] (Content pipeline) and [[Content Automation]] work — the goal is visual content at scale without manual screenshot overhead
- Trial is 14 days; all demos persist if team upgrades after trial
- [[Treble]] (Manila-based) owns workspace; [[Kunday]] looped in on translation pipeline implications
- Embedding method: Storylane demos embed in CMS like YouTube/Vimeo players — Jenna (front-end dev) already testing with public examples
- Localisation workflow: translate existing demos via "Translate and duplicate", then recapture workflows in localised Canva environments
