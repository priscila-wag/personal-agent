---
title: C&C Tech Check — AI prototyping tools and Flying Fox launch
description: "Creative Tech unveiled GenAI templates, Connect API, and Flying Fox (Claude Code-based prototyping tool with collaboration). AI Discovery Week in 2 weeks with hackathon."
type: meeting-note
created_date: 2026-04-23
---

# C&C Tech Check (Craft & Connect: AI Development)
*2026-04-23 | ~15 min | Priscila Wagner + Creative Tech team*

## Summary
Creative Tech presented a comprehensive suite of prototyping resources ready for [[AI Discovery Week]] in two weeks: GenAI-powered templates, Connect API for real Canva data, and the new [[Flying Fox app]] — a custom Electron tool built on [[Claude Code]] that automates Git, enables collaboration, and one-click deploys prototypes. Best practices shared for Cursor context management, rules, and plan mode. Skills are plain-text Markdown files Claude auto-discovers — good pattern for custom workflow automation.

## Decisions
- **Flying Fox pilot launch** — Blake to coordinate with interested users before AI Discovery Week
- **Cursor best practice established** — start new agent tab per feature; use rules for consistency; plan mode for complex features
- **AI Discovery Week structure confirmed** — Days 1-3 workshops/sessions, Days 4-5 hackathon with three pillars: Canva team (internal workflows), Canva product (new features), Canva community (social impact)

## Action Items
| # | Task | Owner | Epic | Due |
|---|------|-------|------|-----|
| 1 | Try Cursor 101 using ERU (formerly Kanji) and lo-fi templates; set brain to Claude model | All attendees incl. Pri | — | Today |
| 2 | Launch Flying Fox app pilot; coordinate with interested users | Blake | — | Before AI Discovery Week |
| 3 | Register hackathon ideas in #hackathon Slack channel | All | — | ASAP |
| 4 | Push Canva Create 2026 layout to Easel prototype | CT team | — | Before AI Discovery Week |
| 5 | Watch for AI Discovery Week Hub comms next week | All | — | Next week |

## Open Questions & Blockers
- **Flying Fox pilot scope** — who gets early access before AI Discovery Week? Not specified.
- **Cursor vs Claude Code** — functionally equivalent when using Claude model in Cursor; Flying Fox (Claude Code-based) adds collaboration and auto-Git. No need to switch if happy with Cursor + Claude.

## Context
- **Flying Fox app** — 8 weeks to build; Electron wrapping Claude Code; auto-creates user-prefixed branches, snapshots every prompt (rollback available), live preview with hot reload, commenting system synced to code, one-click deploy. Roadmap: drag-and-drop design, deeper Easel integration, infinite canvas.
- **Skills** — plain text .md files with name, description, instructions. Claude auto-searches and determines relevance. Can be project-scoped or global. Good model for automating repetitive PM workflows.
- **Context window tip** — after 10-20 rounds in Cursor, context can include 20K+ lines of code. Start new agent tab per feature for accuracy + speed.
- **Plan mode** — creates internal checklist, splits large requests into tasks, runs agents simultaneously. Best practice: describe entire feature set upfront (use mic or separate chat to brainstorm), then feed into plan mode.
- **Connect API** — authenticates users to display real Canva documents, templates, homepage projects, and brand kit data in prototypes. No setup required.
- AI Discovery Week Hub launching early next week with full details and calendar invites
