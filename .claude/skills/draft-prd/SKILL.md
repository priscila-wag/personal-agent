---
name: draft-prd
description: "Draft a PRD using Canva's AI PRD template. Pulls context from Jira epic, GOALS.md, Slack, and existing docs. Saves to Context/Document Hub/ and posts to #prw-personal-agents."
---

# Draft PRD

Draft a product requirements document following Canva's AI PRD template. Populate every required section from available context — leave optional sections clearly marked as [To complete].

**Template source:** `Context/Memory/Reference/templates/prd-template.md`
**Output:** Saved to `Context/Document Hub/[Initiative Name] PRD.md` + posted to #prw-personal-agents
**Channel ID:** `C0AM6E2D4R2`

---

## Instructions

### Step 1 — Establish scope

Extract from the request:
- **Initiative name** — what is being built?
- **Jira epic** — is there an existing epic key? (HELP-XXXX or UVSG-XXX)
- **Stage** — pre-kickoff (Opportunity Space only) or post-kickoff (full doc)?

If initiative name is missing, ask before proceeding.

---

### Step 2 — Gather context (parallel)

**A. Jira**
If an epic key is provided:
- `getJiraIssue` — extract description, milestones, status, assignee
- `searchJiraIssuesUsingJql`: `"Epic Link" = [key] ORDER BY priority ASC` — extract child tickets for scope and key features

If no epic key:
- `searchJiraIssuesUsingJql`: `project = HELP AND summary ~ "[initiative keywords]" ORDER BY updated DESC`

**B. GOALS.md**
Read `GOALS.md` — identify which goal this initiative serves. Extract success metrics and strategic context.

**C. Context/Document Hub/**
Scan for any existing PRD, strategy doc, or decision record referencing this initiative.

**D. Slack** (if available)
```
slack_search_public_and_private: [initiative keywords] in:#hcf-team OR in:#hcf-leads after:[30-days-ago]
```
Extract: decisions made, scope discussions, open questions.

---

### Step 3 — Draft the PRD

Follow the Canva AI PRD template structure exactly. Mark required sections clearly.

---

#### Header

```markdown
# [Cycle] - [Initiative Name]
To follow this project: #[channel if known]

| | |
|---|---|
| Driver | [Pri Wagner — unless specified otherwise] |
| Approver | [Andi Schuster — unless specified otherwise] |
| Contributors | [from Jira assignees / Slack context] |
| Informed | [from Slack / meeting context] |
| Jira epic | [key or TBD] |
| Status | [Kicking off / Shaping / Building / Rollout] |

### Change log
| Date | Change |
|------|--------|
| [today] | Initial draft |
```

---

#### 1. Opportunity Space

**🚀 Problem**
[Why this matters for the business. Tie to Canva strategy. Pull from Jira description or GOALS.md.]

**Who: Target Users** ✅
[Who are you building for? Be specific — logged-out users, Pro users, Enterprise admins, etc.]

**Problem Statement** ✅
- Customer problem: [what friction or gap exists for users]
- Business problem: [what it costs Canva to leave this unsolved]

**Why & Why Now: Strategic fit** ✅
- Strategic fit: [which Canva company goal or UV goal does this serve]
- Why now: [what's changed — new capability, data signal, competitive move]
- Non-goals: [what this explicitly does NOT address]

**Success** ✅
- Working Hypothesis: *"We believe that [doing X] will result in [outcome Y] for [user segment Z]"*
- Primary metric: [metric + threshold]
- Guardrail metrics: [what must not regress]

**🔍 Evidence**

Supporting Data ✅
[Pull from Jira description, GOALS.md metrics, any data mentioned in Slack. If none available: [Data needed — check with Damien]]

Competitive Research *(encouraged)*
[To complete]

Opportunity Sizing *(encouraged)*
[MAU reach, ARR impact — if known]

**⚠️ Dependencies, Risk & Mitigations**

Risks ✅
| Risk | Probability | Severity | Mitigation |
|------|-------------|----------|------------|
| [risk] | [H/M/L] | [H/M/L] | [action] |

Dependencies ✅
| Dependency | Type | Status |
|------------|------|--------|
| [dependency] | [Stakeholder/Technical/Calendar] | [action] |

---

#### 2. Solution Space *(complete after kickoff)*

**📝 Solution Definition**

Proposed Solution ✅
[What is the scope? Key features? Complexity?]

Rejected Options *(encouraged)*
[To complete]

Scope ✅
- In scope: [list]
- Out of scope: [list]

Key Features ✅
- Table stakes: [must-have baseline]
- Differentiators: [what sets this apart]

Product Vision *(encouraged)*
[To complete]

**🎨 Design/Prototype**

Interactive Prototype ✅
[Prototype link — To complete]

Design Explorations ✅
[Figma links — To complete]

Feasibility Review ✅
[To complete — schedule early]

Future Considerations ✅
[What's deferred to a future cycle]

**🧪 Eval Strategy** *(for AI-powered features)*

AI Task Definition
- Primary tasks: [what the AI needs to do]
- Inputs available: [data/context the AI has access to]
- Constraints: [hard rules]

Evaluation Levels
- Level 1 (basic checks): [To complete]
- Level 2 (human/model eval): [To complete]
- Level 3 (A/B): [To complete]

**🗺 Delivery**

Milestones ✅
| Milestone | Description | Target date |
|-----------|-------------|-------------|
| [M1] | [description] | [date] |

Critical Decisions ✅
[To complete]

Experiment & Rollout Plan ✅
- Primary metric + threshold: [metric]
- Guardrail metrics: [what can't break]
- Ramp gates: [To complete]
- Fallback: [To complete]

**📖 Definitions**
| Term | Definition |
|------|------------|

**🔗 References**
- [links to vision, strategy, decision docs, designs]

---

### Step 4 — Save to Context/Document Hub/

Save the full draft as:
`Context/Document Hub/[Initiative Name] PRD.md`

---

### Step 5 — Post to #prw-personal-agents

Call `slack_send_message` with channel `C0AM6E2D4R2`:

```
*📄 PRD draft ready — [Initiative Name]*
Saved to: Context/Document Hub/[filename]
Jira epic: [key or TBD]

*Sections completed:* [list required sections that have real content]
*Needs your input:* [list sections marked [To complete] or [Data needed]]

Review the file and fill in the gaps before sharing.
```

---

## Edge cases

- **No Jira epic**: draft from GOALS.md + request context only. Flag clearly: *"No epic found — create one and link after review."*
- **Pre-kickoff only**: draft Opportunity Space only. Note: *"Solution Space left blank — complete after kickoff."*
- **AI feature**: always include Eval Strategy section, even partially filled.
- **Existing doc found**: note it at the top — *"Existing doc found at [path] — this draft builds on it."*
