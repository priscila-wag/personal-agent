---
name: draft-experiment-doc
description: "Draft an experiment doc following Canva's Confluence live doc structure. Confirms which sections are ready for input, pulls context from Jira/PRDs/Slack, then produces a structured doc with filled sections and clear [To complete] markers. Use this skill whenever Pri mentions drafting, writing, or creating an experiment doc, experiment brief, or experiment page — even if she just says 'start an experiment doc for X' or 'set up the experiment doc'."
---

# Draft Experiment Doc

Draft a structured experiment document following Canva's Confluence live doc format. The document has four areas — **Background**, **UX**, **Development**, and **Post experiment** — with different readiness requirements for each. The goal is to create a working doc that's immediately useful: filled sections are complete enough to share, empty sections are clearly marked so nothing gets forgotten.

**Output:** Saved to `Context/Document Hub/[Experiment Name] Experiment Doc.md` and posted to #prw-personal-agents (`C0AM6E2D4R2`)

---

## Step 1 — Establish the experiment name

Extract the experiment name from the request. If not provided, ask before continuing — the name anchors everything else.

**Naming convention:** Canva experiment docs are prefixed with `X ` (e.g., `X Removing Help Centre link from Home Page`). If the name already starts with `X `, preserve it. If not, add `X ` prefix.

---

## Step 2 — Readiness check

Before gathering context, confirm which sections the user has information ready for. Present this checklist clearly:

```
Which sections do you have info ready for? (I'll pull what I can from Jira/PRDs/Slack — just flag what you have on hand)

🧪 Background
  ☐ Background context — why is this experiment being run?
  ☐ Experiment goal — what outcome are we aiming for?
  ☐ Hypothesis — "We believe that [X] will result in [Y] for [Z users]"

🎨 UX
  ☐ User stories (optional)
  ☐ User flow (optional — Figma or Confluence link?)
  ☐ User Testing / Research — any usability work, or reasoning for skipping?

⚙️ Development
  ☐ Experiment setup — variants (control vs treatment), targeting, flag name?
  ☐ Tracking — primary metric, guardrail metrics, events, dashboard?
```

> QA and Post experiment are not needed at doc creation — I'll mark them clearly for later.

For each section the user flags as ready, ask them to paste the content inline. For sections they haven't flagged, you'll still try to pull what's available from context — just note what was inferred vs. what the user provided.

---

## Step 3 — Gather context (run in parallel)

**A. Jira**
Search for a matching ticket using experiment name keywords:
```
searchJiraIssuesUsingJql: project IN (HELP, UVSG) AND summary ~ "[experiment keywords]" ORDER BY updated DESC
```
Extract: ticket key, description, status, assignee, linked metrics or milestones.

**B. Context/Document Hub/**
Scan for any existing PRD, strategy doc, or prior experiment doc referencing this initiative. If found, reference it in the Background section.

**C. Slack**
```
slack_search_public_and_private: [experiment keywords] after:[30-days-ago]
```
Extract: decisions made, scope discussions, open questions, metric targets mentioned.

---

## Step 4 — Draft the document

Use the template below. Apply these rules:

- **User-provided content** → fill in directly, no marker needed
- **Inferred from context (Jira/Slack/PRD)** → fill in with a note: *(from Jira)* or *(from Slack)*
- **Missing / not provided** → use `[To complete]` — never leave a required section blank without a marker
- **Optional sections with nothing available** → use `[To complete — or mark as not applicable]`

### Document template

```markdown
---
title: [Experiment Name] — Experiment Doc
description: "[~150 chars describing the experiment and its goal — used for future retrieval]"
type: experiment-doc
created_date: [YYYY-MM-DD]
jira_ticket: [key or TBD]
status: Planning
---

# [X] [Experiment Name]

| | |
|---|---|
| Driver | [Pri Wagner — unless specified otherwise] |
| Jira ticket | [key or TBD] |
| Created | [today's date] |
| Status | Planning |

---

## 🧪 Background

### Background
[Why is this experiment being run? What user problem, business signal, or strategic bet is it responding to?]

### Experiment goal
[What outcome are we trying to achieve? Tie to team or company goals where possible.]

### Hypothesis
*"We believe that [doing X] will result in [outcome Y] for [user segment Z]."*

---

## 🎨 UX

### User stories *(optional)*
[To complete — or: not applicable]

### User flow *(optional)*
[To complete — or: [Figma/Confluence link]]

### User Testing / Research
[Link to research, usability testing notes — or: "No user testing planned. Rationale: [___]"]

---

## ⚙️ Development

### Experiment setup

**Variants:**
| Variant | Description |
|---------|-------------|
| Control | [what users see today] |
| Treatment | [what users see in the experiment] |

**Targeting:**
- Audience: [who sees this experiment]
- Rollout: [% or gating logic, e.g. 50/50 split]
- Flag name: [To complete]

### Tracking

**Primary metric:** [metric name + success threshold, e.g. "Help article views — target: -10% (fewer users needing help)"]
**Guardrail metrics:** [what must not regress, e.g. "CSAT, task completion rate"]
**Events to track:** [list key events]
**Dashboard:** [link — or: To complete]

### QA
> ⚠️ *Not required at doc creation — complete before launch.*

[To complete]

---

## 📊 Post experiment

> ⚠️ *Not required at doc creation — fill after the experiment concludes.*

### Experiment results
[To complete]
```

---

## Step 5 — Save the document

Save the completed draft as:
`Context/Document Hub/[Experiment Name] Experiment Doc.md`

---

## Step 6 — Post to #prw-personal-agents

Call `slack_send_message` with channel `C0AM6E2D4R2`:

```
*🧪 Experiment doc drafted — [Experiment Name]*
Saved to: Context/Document Hub/[filename]
Jira ticket: [key or TBD]

*Sections filled:* [list sections with real content]
*Needs input before sharing:* [list sections marked [To complete] that are required]
*Fill later:* QA (before launch), Experiment results (post-experiment)
```

---

## Edge cases

- **No Jira ticket found:** Draft without it. Note at the top: *"No Jira ticket linked — add before sharing."*
- **No UX info at all:** Mark the entire UX section `[To complete — UX section to be filled by design]` and flag it in the Slack summary.
- **PRD exists in Context/Document Hub/:** Reference it at the top of the Background section: *"Related PRD: [filename]"*
- **User has everything ready:** Skip the readiness check and draft directly — the checklist is only needed when there's uncertainty about what's available.
- **Experiment name already has X prefix:** Preserve it as-is.
