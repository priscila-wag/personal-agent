# HC leads planning
*2026-04-20 | 48 min | [[Patricia S]] · [[Priscila Wagner]] · [[Linette]] · [[Tahlia]] · [[Kunday]] · Chris Pritchett*

## Summary
H1 progress review that ended with two locked scope changes: "Ask About This Page" [[UVSG-615]] HA integration is officially out of H1 (bumped to H2, blocked by technical dependencies), and the translation pipeline is cutting ModernMT in favour of AutoML to reclaim 50–60 min per release. The meeting seeded the H2 PRD — [[HC AI mode]] + visual/format expansion — with Pri as owner.

## Decisions
- **H1 scope change:** "Ask About This Page" Help Assistant integration removed from H1 deliverables; AI Mode experiment takes priority as higher-impact milestone — [[Tahlia]] to confirm blockers with [[HYPE]] before communicating to Andy
- **Translation pivot:** AutoML replaces ModernMT short-term; unified staging/production deployment removes round-trip to Smartling for non-Chinese content
- **SmartLink evaluation:** Han (localization) is more open than Marie to eliminating SmartLink translation memory for non-Chinese content; decision pending quality comparison data
- **H2 PRD ownership:** [[Priscila Wagner]] will draft H2 PRD covering [[HC AI mode]] HA integration and expansion to visual content formats (Storylane, YouTube, Trymydesign)
- **Content guidelines automation:** Idea of enforcing content guidelines via a Contentful tool/AI skill added to H2 ideas backlog — [[HELP-3820]]

## Action Items

| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Schedule meeting with HYPE (Guy, Roman, Drew) to confirm HA integration technical blockers; document for Andy before communicating H1 miss | [[Tahlia]] | [[UVSG-615]] | ASAP |
| 2 | Draft H2 PRD for [[HC AI mode]] — HA integration + visual/format expansion (Storylane, YouTube, Trymydesign, app surfacing) | [[Priscila Wagner]] | [[UVSG-615]] | — |
| 3 | Switch translation pipeline to AutoML this week with Suchini's support; create rollback flag to ModernMT | [[Kunday]] | [[HELP-3090]] | This week |
| 4 | Meet with Han (localization) to assess eliminating SmartLink translation memory for non-Chinese content; get quality comparison data | [[Kunday]] | [[HELP-3090]] | — |
| 5 | Loop [[Priscila Wagner]] into Kunday–localization discussions to navigate stakeholder concerns with Han and Marie | [[Kunday]] | [[HELP-3090]] | Ongoing |
| 6 | Complete handover of category management to Content Ops before May leave | [[Patricia S]] | [[HELP-3090]] | Before May |
| 7 | Share draft article restructuring and content guidelines with [[Linette]] and team before leaving | [[Patricia S]] | [[HELP-3222]] | Before May |
| 8 | Add "Automate content guidelines enforcement via Contentful" to Jira H2 ideas board | [[Priscila Wagner]] | [[HELP-3820]] | — |
| 9 | Chat with [[Linette]]/Marlene to scope content guidelines automation requirements for Content Ops | [[Priscila Wagner]] | [[HELP-3820]] | — |
| 10 | Revisit and readjust H1 content pipeline milestones — account for team burnout, new starter in May, Affinity firefighting | [[Kunday]] | [[HELP-3090]] | ~1 week |
| 11 | Reconnect with [[Priscila Wagner]] after short-term translation fixes resolve to discuss longer-term infrastructure direction | [[Kunday]] | — | ~1 week |

## Open Questions & Blockers
- What is HA satisfaction rate for non-English content vs. Help Center? — needed to validate AutoML quality before cutting SmartLink
- Can Japanese content writers edit directly in Contentful after initial machine translation, skipping the full SmartLink MTPE workflow?
- What are leadership expectations for publishing speed improvement? (current ~2 hours → potential ~30 min)
- Should HC surface Canva App Store apps contextually when relevant to a user's job-to-be-done?
- H1 engineering milestones need rejigging — team burned out from Affinity launch, new starter onboarding in May further constrains capacity; [[Kunday]] explicitly flagged capacity cannot deliver original [[Content Automation]] goals without support

## Context
- **SmartLink failures at Affinity launch:** 20 articles missing translations despite connector completing — required 2am manual job rerun; root cause: rate limiting at 60 req/sec shared across all uses, causing throttling during large releases
- **Pipeline waste identified:** Content → ModernMT → Smartling upload → download → Contentful. No human review occurs, making the round-trip pointless for non-Chinese content; eliminating this step reclaims 30–45 min
- **Contentful Sync opportunity:** Switching to delta-based Contentful Sync with S3 backup saves another ~40 min from deploy; combined with AutoML = ~30-min deploys feasible
- **Design School integration delivered:** ~1,000 tickets/month decrease, ~500 users/month increase — solid compounding return from prior work
- **[[UVSG-615]] current status:** Split panel at 100% rollout since Apr 7; AI chat near-complete; May 15 HA integration milestone is now at risk pending HYPE dependency confirmation
