# personal-agent

A personal AI agent that keeps your career on track, writes your product and experiment docs, and makes meetings and tasks effortless. No code, no database — just a folder of markdown files, a set of skills, and an AI that knows your context.

Your agent reads your goals, remembers your preferences, and learns from every week. It gets more useful the longer you use it.

Works with **Claude Code Desktop**, **Claude Code CLI**, **Claude Co-Work**, **Cursor**, or any AI tool that reads local files.

---

## What It Does

### 🎯 Keep your career on track
- Map every task and milestone to your G&I goals
- Log weekly achievements automatically from Jira and Slack — G&I review becomes copy-paste
- Track growth behaviours (AI judgment, strategic leverage, visible prioritisation, signal-first comms) with evidence as you go
- Run a bias audit on any decision against your motivational profile
- Get a structured morning briefing every day — calendar, Jira, and overnight Slack signals in one place

### 📄 Generate product and experiment docs
- Draft PRDs, experiment docs, and goal update comments from Jira context, Slack discussions, and your existing docs
- Multi-perspective steelmanning of any document — 3–5 critique lenses run in parallel to surface blind spots before you share
- Draft emails, Slack messages, and strategy docs in your own voice

### ⚡ Make meetings and tasks efficient
- Auto-digest Zoom meetings: extract decisions and action items, deduplicate against Jira, save structured notes
- Morning briefing posted automatically at 8:30am — focus items, overdue Jira, overnight signals
- 1:1 prep with full talking points generated from notes, tasks, and ongoing relationship docs
- Weekly and daily planning that reads from your goals, not a blank slate

---

## Quick Start

### 1. Get the folder

```bash
git clone https://github.com/priscila-wag/personal-agent.git
```

Or download the zip from the green **Code** button above. Put it somewhere permanent — this is a living workspace, not a one-time download.

### 2. Open it in an AI tool

You need something to **run the AI** and something to **browse your files**. You can use one tool for both, or pair them.

#### Claude Code Desktop (recommended)

1. Download [Claude Code Desktop](https://claude.ai/download) (macOS / Windows)
2. Open the app → **Code** tab → **Local** → **Select folder** → choose `personal-agent`
3. Start chatting. Skills are auto-discovered from `.claude/skills/`

#### Claude Code CLI

```bash
npm install -g @anthropic-ai/claude-code
cd personal-agent && claude
```

#### Claude Co-Work

Open [Claude Co-Work](https://claude.ai) and select this folder. Skills are auto-discovered.

#### Cursor

Open this folder as a project. Use the AI chat panel (`Cmd+L`) — it picks up `CLAUDE.md` as context automatically.

#### Obsidian (companion, not AI)

[Obsidian](https://obsidian.md) is great for browsing and editing your markdown files — kanban boards, linked notes, graph view. It doesn't run AI, but pairs well with any of the tools above.

---

### 3. Run `/onboard`

This is the fastest way to get set up. `/onboard` walks you through two things:

1. **Goals interview** — populates `GOALS.md` with your role, vision, quarterly priorities, and current projects
2. **Agent config** — creates `Context/agent-config.md` with your Slack ID, timezone, personal channel, and default document settings

Everything the agent does is grounded in these two files. Fill them in once; all skills read from them automatically.

---

### 4. Start using it

**Daily:**
- `/today` — daily plan from your weekly scratchpad, calendar, Jira, and overnight signals
- `/morning-briefing` — posts a compact brief to your Slack channel at 8:30am (runs automatically)
- Drop items into `BACKLOG.md` → `/backlog` to triage into structured tasks

**Weekly:**
- `/plan-week` — full week plan on Monday: priorities, meeting triage, daily pre-plans
- `/weekly-wrap` — Friday review: progress, shareable update, learnings compounded into memory

**Career & G&I:**
- `/achievements` — pull the week's progress from Jira and Slack, map to goals, log to your achievements file
- `/bias [topic]` — audit a decision against your motivational profile blind spots
- `/draft-goal-update [UVSG-XXX]` — draft the monthly goal comment from Jira + Slack context

**Meetings & 1:1s:**
- `/meeting-digest` — Zoom transcript → decisions, action items, structured notes (also runs hourly, 9am–5pm)
- `/121 [person]` — talking points from notes, tasks, and your ongoing relationship doc (also runs inside `/today`)
- `/draft-meeting-minutes` — structured minutes from transcript or description

**Product & experiment docs:**
- `/draft-prd [initiative]` — PRD from Jira epic, GOALS.md, and Slack context
- `/draft-experiment-doc [name]` — experiment doc following Canva's Confluence structure
- `/draft-goal-update` — monthly progress comment for a UVSG goal ticket
- `/draft [topic]` — email, Slack message, or strategy doc in your voice
- `/steelman-advice [doc]` — multi-perspective critique: blind spots, reframes, concrete improvements

**On demand:**
- `/slack-unactioned` — triage unread Slack into Tonight (urgent) vs Tomorrow (can wait)
- `/unblock [task]` — diagnose a stalled task and find the smallest next action
- `/canva-lingo` — look up Canva-specific terms, acronyms, and deprecated names
- `/update-graph` — refresh the interactive idea graph connecting your ideas, Slack discussions, and Jira projects

---

## Folder Structure

```
personal-agent/
├── GOALS.md                      # Your goals, vision, and quarterly priorities
├── BACKLOG.md                    # Raw capture inbox — dump ideas here
├── AGENTS.md                     # Agent instructions (how the AI behaves)
├── CLAUDE.md                     # Points to AGENTS.md (auto-loaded by Claude)
├── Weekly Kanban.md              # Sprint board — visual kanban with [[wiki-links]]
│
├── Tasks/                        # Active task files
│   ├── Backlog/                  # Initiative/track files — strategic context
│   └── Done/                     # Completed tasks (archived here)
│
├── Context/                      # Persistent personal context
│   ├── agent-config.md           # Your settings: Slack ID, timezone, defaults (created by /onboard)
│   ├── G&I Goals H1 2026.md      # Current review cycle: goals, milestones, growth behaviours
│   ├── Memory/                   # Preferences, decisions, and compounded learnings
│   │   ├── pri-brain.md          # Deep map of how you think, communicate, and decide
│   │   ├── bias.md               # Motivational profile — drives /bias and communication rules
│   │   ├── learnings.md          # Distilled weekly insights — compounds over time
│   │   └── Reference/            # Writing-style guides, strategic frameworks, company context
│   ├── 121s/                     # Ongoing 1:1 relationship docs (maintained by /121)
│   ├── Document Hub/             # PRDs, strategy docs, experiment docs, decision records
│   ├── Meeting Notes/            # Meeting digests and summaries
│   └── Progress Updates/         # Weekly wraps, goal reviews, achievements log
│
├── Notes/                        # Daily notes and thinking
├── Bookmarks/                    # Reading list and saved links
│
└── .claude/skills/               # Slash commands (auto-discovered)
    ├── onboard/                  # /onboard — first-time setup + agent-config
    ├── today/                    # /today — daily planning
    ├── plan-week/                # /plan-week — weekly planning
    ├── backlog/                  # /backlog — triage inbox
    ├── weekly-wrap/              # /weekly-wrap — weekly review + learnings
    ├── morning-briefing/         # /morning-briefing — daily Slack brief (auto at 8:30am)
    ├── achievements/             # /achievements — G&I log from Jira + Slack
    ├── 121/                      # /121 — 1:1 meeting prep
    ├── meeting-digest/           # /meeting-digest — Zoom → notes + action items
    ├── draft-meeting-minutes/    # /draft-meeting-minutes — structured minutes
    ├── draft/                    # /draft — universal drafting router
    ├── draft-prd/                # /draft-prd — PRD from Jira + Slack context
    ├── draft-experiment-doc/     # /draft-experiment-doc — Canva experiment doc structure
    ├── draft-goal-update/        # /draft-goal-update — monthly goal comment
    ├── steelman-advice/          # /steelman-advice — multi-perspective document critique
    ├── slack-unactioned/         # /slack-unactioned — triage unread messages
    ├── unblock/                  # /unblock — diagnose stalled tasks
    ├── bias/                     # /bias — motivational bias audit
    ├── update-graph/             # /update-graph — interactive idea graph
    └── canva-lingo/              # /canva-lingo — company terminology reference
```

---

## How It Works

Three layers work together:

**1. Config** (`GOALS.md`, `Context/agent-config.md`, `Context/G&I Goals *.md`)
The agent reads these to understand who you are, what you're working toward, and how to find your tools. Without this, every session is a capable stranger. With it, every session picks up where the last one left off.

**2. Tasks** (`Tasks/`, `BACKLOG.md`, `Weekly Kanban.md`)
Structured markdown with YAML frontmatter — priority, status, goal reference. The Kanban board gives a visual sprint view. The planning loop (below) keeps these files current automatically.

**3. Skills** (`.claude/skills/`)
Reusable workflows triggered by slash commands. They combine file reading, reasoning, and tool calls into repeatable processes that adapt to your goals and context.

### The Planning Loop

```
Monday:  /plan-week  → creates Tasks/Week-YYYY-WNN.md with all 5 days pre-planned
Daily:   /today      → reads weekly plan, preps every meeting, updates the scratchpad
Friday:  /weekly-wrap → reviews progress, produces a shareable update, compounds learnings
```

### The Compounding Loop

```
/weekly-wrap → distills insights into Context/Memory/learnings.md
                   ↓
         future sessions reference past learnings
                   ↓
         better advice → more learnings → repeat
```

Your agent after 4 weeks is meaningfully better than on day one. After 8–10 weeks of `/achievements`, your G&I self-review is copy-paste.

---

## Using This With Your Team

All skills are generic — no personal data is hardcoded. Each user sets up two files once:

- **`Context/agent-config.md`** — Slack ID, timezone, channel, default document names
- **`Context/G&I Goals [cycle].md`** — current review cycle goals, milestone hierarchy, growth behaviours

To give a teammate access: share the `.claude/skills/` folder. They run `/onboard` and fill in their own config. All skills work from their context, not yours.

---

## How This Relates to Co-Work

If you're using Claude Co-Work, this workspace is complementary — not a replacement.

| Co-Work alone | Co-Work + this workspace |
|---|---|
| Each session starts blank | Sessions inherit your goals, memory, and learnings |
| Skills are generic recipes | Skills reference your goals, config, and G&I cycle |
| No memory across sessions | `Context/Memory/` persists everything |
| You repeat yourself every time | `GOALS.md` is read automatically |

Co-Work provides the hands (connectors, sub-agents, Chrome, local files). This workspace provides the brain (goals, memory, learnings, skills that know you). They stack.

---

## Automated Agents

Some skills run on a schedule without being triggered manually.

### Morning Briefing (daily, 8:30am)

`/morning-briefing` posts your daily brief to Slack every morning via macOS launchd. It pulls calendar, Jira, and overnight Slack signals, picks 3 focus items, and posts a compact message to your personal channel.

### Meeting Digest (hourly, 9am–5pm)

`/meeting-digest` runs every hour and checks for new Zoom meetings. When it finds one not yet processed: extracts decisions and action items, saves structured notes to `Context/Meeting Notes/`. Fully idempotent — safe to run multiple times.

**Setup files:**
- `~/.claude/scripts/meeting-digest.sh` — shell wrapper
- `~/Library/LaunchAgents/com.pri.meeting-digest.plist` — launchd schedule
- `~/.claude/logs/meeting-digest.log` — run log

```bash
# Load
launchctl load ~/Library/LaunchAgents/com.pri.meeting-digest.plist

# Trigger manually
launchctl start com.pri.meeting-digest

# Unload
launchctl unload ~/Library/LaunchAgents/com.pri.meeting-digest.plist
```

---

## Add Your Own Skills

Create `.claude/skills/<name>/SKILL.md`:

```markdown
---
name: my-skill
description: "What this skill does and when to use it"
---

# My Skill

## Instructions

[Steps for the agent to follow]
```

Run it with `/my-skill`. Skills can read any file in the workspace, call connected tools (Jira, Slack, Zoom, Calendar), and write output back to your files.

**Ideas:** `/status-update` · `/retro` · `/goal-alignment` · `/brainstorm [topic]` · `/promo-doc`

---

## License

CC BY-NC-SA 4.0
