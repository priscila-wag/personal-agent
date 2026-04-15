---
title: Mobile Help UX goal metric alignment — Pri & Damien
description: "Data alignment on mobile help UX goal metric: activation split by platform. Damien to pull Snowflake data; Pri holding stakeholder LGTM until confirmed."
type: meeting-note
created_date: 2026-04-14
---

# Priscila Wagner's Personal Meeting Room
*2026-04-14 | ~17 min | [[Priscila Wagner]], [[Damien Kime]]*

## Summary
Quick alignment with [[Damien Kime]] to lock the primary metric for the [[Mobile Help UX]] goal before seeking stakeholder LGTM. Canva product activation rate within 24 hours of help usage (share/download/publish) is the right metric — but the Looker dashboard doesn't split it by platform, so [[Damien Kime]] is pulling the data from Snowflake. Pri is holding the goal creation in Jira until the data confirms that desktop activation is in fact higher than mobile.

## Decisions
- **Primary metric: Canva product activation rate within 24 hours of help usage** — not help flow activation (share/download/publish/present) — Pri
- **Goal name confirmed:** "Improve the mobile experience to hit desktop activation parity" — Pri
- **Scope: [[AI-First Help Center|help assistant only]]** (AI help), not help center broadly — confirmed with [[Damien Kime]]
- **If data doesn't support hypothesis**, Pri will agree on a different goal name with stakeholders before filing in Jira

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Extract Canva product activation data split by platform from Snowflake | [[Damien Kime]] | [[HELP-4139]] | 2026-04-14 |
| 2 | Notify stakeholders data confirmation is in progress; adjust goal name if activation hypothesis isn't supported | Pri | [[HELP-4139]] | 2026-04-14 |

## Open Questions & Blockers
- **Platform split not available in Looker by default** — Looker's LP activation rate dashboard uses aggregated data; Snowflake query required for platform breakdown
- **Intent skew risk** — desktop help sessions may be disproportionately refund/cancellation related, which could inflate desktop activation rates artificially; Damien flagged this as a known risk and will flag if the data tells the wrong story
- **Stakeholder LGTM pending** — goal cannot be created in Jira until activation data confirms hypothesis; Pri is waiting on Damien's Snowflake output

## Context
- Mobile help rate is ~0.9% vs desktop ~2% — a large gap even before activation is measured
- Only 15% of mobile help users return to help — a strong signal that the mobile help experience is broken, not just underused
- Mobile users can't reopen the help assistant after closing it — a known severe UX issue driving the goal
- Canva Create is reducing experiment load, creating bandwidth for this work
- Friday (2026-04-18) is effectively a write-off due to Canva Career event at 2pm — [[Damien Kime]] and team attending
