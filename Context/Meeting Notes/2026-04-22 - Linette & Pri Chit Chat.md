---
title: Linette & Pri Chit Chat — Help Center Rebranding Pre-Brief
description: "Pre-brief between Pri and Linette ahead of N:1 with Andi. HC label hiding agreed (1-2 weeks), ToC sidebar move, offline help H2 priority flagged."
type: meeting-note
created_date: 2026-04-22
---

# Linette & Pri Chit Chat
*2026-04-22 | 30 min | [[Priscila Wagner]], [[Linette Voller]]*

## Summary
Leadership ([[Andi]], Mark, Mel) is pushing to remove or rebrand the "Help Center" label immediately, and Pri and Linette aligned on approach ahead of the N:1 with Andi. The root cause of the request is unclear — it appears driven by internal perception rather than user research. Pri will temporarily hide the HC label on the homepage only (1–2 week cap), get clarity from Andi on what prompted the ask, and flag navigability risks if the label disappears permanently without a proper strategy.

## Decisions
- **Temporarily hide "Help Center" label on homepage** to manage leadership pressure — not on breadcrumbs or other pages. Hard cap: revert or commit to a plan within 1–2 weeks.
- **Table of contents moves to left sidebar** (from article center), following Claude/ChatGPT patterns. Currently blocking content, causing accidental mobile taps, and breaking screen readers/AI parsing because writers are avoiding headings.
- **Offline help (markdown library)** prioritized as H2 initiative — top 20 intents per doc type, no images, basic browse/search. Start simple before adding embedded AI.

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Meet with [[Andi]] to understand background conversation with Mel and Mark that prompted urgent label removal | Pri | [[HELP-3090]] | ASAP |
| 2 | Review Fullstory sessions to build data case on [[Help Center]] homepage usage patterns and navigation behavior | Pri | [[HELP-3090]] | This week |
| 3 | Create Jira epic for prototype week (May 4th) — article page redesigns with designer + content designer | Pri | [[HELP-3090]] | This week |
| 4 | Push offline help + article experience (ToC sidebar) as H2 priorities | [[Linette]] | [[HELP-3090]] | H2 planning |

## Open Questions & Blockers
- **Root cause unclear**: What specific conversation between Mel, Mark, and Andi prompted the urgent label removal? Needed before committing to a direction.
- **Naming strategy unresolved**: Align "Help Center" name with "Help Assistant" terminology, or differentiate them? Options on the table: "Get Help", "Help", generic navigation item — "Home" conflicts with Canva Home.
- **No analytics on HC homepage nav**: No tracking events exist to measure how many users use the HC label to return home. Makes impact measurement impossible pre-experiment.
- **SEO and localization risk**: "Help Center" has real Google discoverability value. Name changes have "massive SEO impacts" — needs proper evaluation before any external rename.
- **Partial rebrand risk**: Hiding the label without a new strategy creates confusion, not clarity — like removing the "Rolls Royce" badge before the new car arrives.

## Context
- [[Help Center]] gets ~5 million monthly sessions. Majority of users arrive via Google, land on individual articles, and use the HC label to reset searches or browse categories — not to navigate from the homepage.
- Leadership's mental model is HC = static 2020 article library. Reality: search, AI assistant, design school, shortcuts, contact flows, billing info.
- [[Mark]]'s recurring question ("why do we even have Help Center? It should all be in-product") ignores offline use cases and non-product queries like billing — a pattern Pri has flagged before.
- User research: screening participants consistently conflate [[Help Center]] and [[Help Assistant]], making research difficult. This confusion is a real product problem distinct from the label debate.
- This meeting was a pre-brief before [[N:1 HCF + Andi]] at 14:30 AEST same day.
