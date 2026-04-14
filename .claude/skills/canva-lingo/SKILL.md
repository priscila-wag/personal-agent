---
name: canva-lingo
description: "Look up Canva-specific terms, acronyms, and deprecated names — the shared glossary layer for the supergroup"
---

# Canva Lingo

Authoritative terminology lookup for Canva-specific language. Prevents agents from using
outdated, ambiguous, or inconsistent naming across the supergroup.

## Instructions

When the user invokes `/canva-lingo [term]` or asks questions like:
- "What does [X] mean?"
- "What do we call [X]?"
- "Is [X] deprecated?"
- "How should I refer to [X]?"
- "What's the right term for [X]?"

Run the following steps in sequence.

---

### Step 1: Load the glossary

Read `Context/Memory/Reference/canva-glossary.md`.

If the file doesn't exist, tell the user and offer to create it using the Bootstrap section below.

---

### Step 2: Look up the term

Search the glossary for the term. Try in this order:
1. Exact match on term or acronym
2. Match on aliases / also-known-as
3. Partial match on term name

Return a structured result:

| Field | Value |
|-------|-------|
| **Term** | The canonical name |
| **Status** | Active / Deprecated / Renamed / Ambiguous |
| **Definition** | Plain-language explanation |
| **Aliases / Also known as** | Other names, acronyms, legacy names |
| **Do not call it** | Common wrong names (if any) |
| **Notes** | Context, nuance, disambiguation |

---

### Step 3: Handle ambiguous terms

Some terms have multiple meanings at Canva (e.g. CC, DD, RC, GTM, PDP, Team).

If the term is ambiguous:
1. List all known meanings with context on when each applies
2. Ask the user which context they're working in if it affects the answer

---

### Step 4: Handle deprecated terms

If a term's status is **Deprecated** or **Renamed**:
- State clearly: "**[term]** is deprecated."
- State what replaced it (if known)
- State the preferred term going forward

Example:
> **C4W** is deprecated. It was renamed to **Canva Pro** in mid-2019 to expand beyond work use cases. Use "Canva Pro" going forward.

---

### Step 5: Handle "not found"

If no match is found:
1. Say clearly: "No entry for '[term]' in the Canva glossary."
2. Ask: "Do you know the correct usage? I can add it."
3. If the user confirms → proceed to Step 6

---

### Step 6: Add or update a term

When a user wants to add or correct a glossary entry, append to
`Context/Memory/Reference/canva-glossary.md` using this format:

```
## [Preferred Term / Acronym]
- **Status:** Active | Deprecated | Renamed | Ambiguous
- **Definition:** Plain-language explanation (1-3 sentences).
- **Aliases:** alias1, alias2 (optional)
- **Renamed from / to:** previous or new name (if applicable)
- **Do not call it:** wrong names to avoid (if applicable)
- **Notes:** nuance, edge cases, links (optional)
- **Last updated:** YYYY-MM-DD
```

After adding, remind the user:
> "Added to your local glossary. Don't forget to PR this to the canvanauts repo so the whole supergroup benefits."

---

### Step 7: Compound-on-touch (silent)

While running this skill:
- If you spot a glossary entry missing a **Status** field → add it
- If you spot a term used incorrectly elsewhere in the workspace → flag it once, don't lecture

---

## Bootstrap: Creating the glossary from scratch

If `Context/Memory/Reference/canva-glossary.md` doesn't exist:

1. Create the file with the header below
2. Seed it with any terms the user provides now
3. Note: the canonical source lives in the canvanauts repo — agents should pull updates when the file feels stale

Starting template:
```markdown
# Canva Glossary

Shared terminology reference for the supergroup.
Canonical source: canvanauts/personal-agent repo.
Last synced: YYYY-MM-DD

<!-- Entries below in alphabetical order -->
```

---

## Output format

- Return one structured table per term
- For ambiguous terms, list all meanings clearly
- Keep meta-commentary minimal — give the answer, not a description of the answer
- If multiple partial matches found, list them with a disambiguation line
