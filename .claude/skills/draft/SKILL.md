---
name: draft
description: "Universal drafting router — detects what type of draft is needed, uses the correct template, and posts output to #prw-personal-agents. Handles goal updates, PRDs, meeting minutes, emails, Slack messages, and strategy docs."
---

# Draft

Detect the type of content needed, apply the right template, draft it in Pri's voice, and post to #prw-personal-agents. One entry point for all drafting.

**Channel ID:** `C0AM6E2D4R2`

---

## Step 1 — Detect draft type

Read the request and classify into one of these types:

| Type | Signals |
|------|---------|
| `goal_update` | UVSG-XXX mentioned; "goal", "progress update", "goal alignment", "GA", "monthly update", "monthly comment" |
| `prd` | "PRD", "product requirements", "initiative brief", "kickoff doc", "feature spec", "product brief" |
| `meeting_minutes` | "meeting notes", "minutes", "recap", "notes from [meeting]", "what was discussed", "write up the meeting" |
| `email` | "email", "reply to [person]", "write to [person]", "message to [email]" |
| `slack_message` | "slack", "post in #[channel]", "message in", "send to [person] on Slack" |
| `strategy_doc` | "strategy", "memo", "write up", "one-pager", "narrative", "doc about" |

If the type is ambiguous, ask one question: *"What type of content is this — goal update, PRD, meeting notes, email, Slack message, or something else?"*

---

## Step 2 — Route to the correct sub-skill

Read the corresponding skill file and execute it fully:

| Type | Skill file |
|------|-----------|
| `goal_update` | `.claude/skills/draft-goal-update/SKILL.md` |
| `prd` | `.claude/skills/draft-prd/SKILL.md` |
| `meeting_minutes` | `.claude/skills/draft-meeting-minutes/SKILL.md` |
| `email` | Execute inline — see Email instructions below |
| `slack_message` | Execute inline — see Slack instructions below |
| `strategy_doc` | Execute inline — see Strategy Doc instructions below |

Pass the full original request as context when executing the sub-skill.

---

## Inline: Email

**Gather context:**
- Check `Context/Memory/Reference/writing-styles/` for voice guide
- Check `Context/121s/` if the recipient has a relationship doc
- Check `Context/Meeting Notes/` for relevant recent context

**Draft rules:**
- Lead with the point, not a greeting
- 2–3 sentences per paragraph max
- Specific and direct — no filler phrases ("I hope this finds you well", "just wanted to", "as per my last email")
- Close with a clear ask or next step
- Sign off: Pri (not "Best regards, Priscila Rachelle Wagner")

**Post to #prw-personal-agents:**
```
*✉️ Email draft — to [recipient] re: [subject]*

[Full email text in a code block]

Subject line: [suggested subject]
```

---

## Inline: Slack message

**Gather context:**
- If posting in a known channel, check recent messages for tone and thread context
- Check `Context/121s/` if directed at a specific person

**Draft rules:**
- No subject line — lead straight into the message
- Conversational but not sloppy
- Use bullet points only if listing 3+ distinct items
- Avoid excessive emoji — use 1 if it fits, not as decoration
- Keep it to what fits on a phone screen

**Post to #prw-personal-agents:**
```
*💬 Slack draft — [channel or @person]*

[Full message text]
```

---

## Inline: Strategy doc / one-pager

**Gather context:**
- Read `GOALS.md` for strategic context
- Check `Context/Document Hub/` for related docs
- Check `Context/Memory/Reference/frameworks/` for relevant frameworks (JTBD, 7 Powers, etc.)

**Structure:**
```markdown
# [Title]
*[Date] | [Author: Pri Wagner]*

## TL;DR
[2–3 sentences. What is this, why does it matter, what does it recommend.]

## Background
[Context — what's the situation, what led to this?]

## The Opportunity / Problem
[What we're solving and why now.]

## Proposed Approach
[What we're recommending. Be specific.]

## Why This, Not That
[Key tradeoffs or alternatives considered and rejected.]

## Success Looks Like
[Concrete outcomes — metric + timeframe where possible.]

## Open Questions
[What still needs to be resolved before moving forward.]

## Next Steps
| Action | Owner | By when |
|--------|-------|---------|
```

**Save to:** `Context/Document Hub/[title].md`

**Post to #prw-personal-agents:**
```
*📄 Strategy doc draft — [title]*
Saved to: Context/Document Hub/[filename]

[TL;DR text]

Review, fill open questions, and share when ready.
```

---

## Voice rules (apply to all types)

Read `Context/Memory/pri-brain.md` before drafting. Apply these always:
- Lead with outcome, not effort or process
- Specific over vague — name the thing
- Short sentences — no padding
- Confident, not hedging
- No generic AI phrasing ("it's worth noting", "in conclusion", "this is important because")
- Internal Canva docs: casual but precise. External: professional but not stiff.

---

## Output rule

All draft types post to `#prw-personal-agents` (C0AM6E2D4R2). Never output only to the console when running automated — always post to Slack.
