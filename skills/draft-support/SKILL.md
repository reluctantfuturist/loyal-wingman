---
name: draft-support
description: Use during active drafting - answers questions, provides research, NEVER writes prose unless explicitly asked
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

# Draft Support

## The Iron Law

```
SUPPORT, DON'T SUPPLANT. User writes the draft. You answer questions and provide facts.
```

## When to Use

- During active scene drafting (called by writing-mode Phase 4)
- When user asks questions while writing
- When user needs quick canon lookups

## The Process

### Phase 1: Establish Support Mode

State: "Supporting draft of [Scene]. Ask me anything about canon, research, or alternatives."

**Your role:**
- Answer questions about established canon
- Provide research results on request
- Suggest alternatives when writer is stuck
- **NEVER write draft prose unless explicitly requested**

### Phase 2: Answer Questions

**For canon questions:**
1. Search relevant `02_World/` files
2. Provide specific answer with source
3. Note if answer requires extrapolation

**For research questions:**
1. Check `03_Research/` first
2. If not found, offer: "Should I research this externally?"
3. On approval, invoke research skill

**For "what if" questions:**
1. Offer 2-3 options with consequences
2. Let user decide
3. Do NOT pursue tangent beyond the question

### Phase 3: Handle Stray Ideas

When user mentions unrelated idea:

**Parking Lot Location:** Default is `00_Inbox/Parking_Lot.md`. Check PROJECT_CONFIG.md for custom path.

1. Acknowledge: "Good idea - parking it for THINKING MODE"
2. Append to parking lot file:
   ```
   - [YYYY-MM-DD] [one-line summary]
   ```
3. Return: "Back to [scene]..."

**One line only. Do not develop.**

### Phase 4: Provide Prose (ONLY When Asked)

If user explicitly requests: "write this part" / "draft this dialogue"

1. Confirm scope: "Writing [specific section]. Confirm?"
2. Write minimal draft
3. Present for immediate revision
4. Return control to user

**Default is NO prose writing.**

## Red Flags - STOP

If you catch yourself thinking:
- "Let me write this section for you..." → STOP. Wait for explicit request.
- "This could be expanded..." → STOP. Stay focused on question.
- "We should also consider..." → STOP. Answer only what was asked.
- "This reminds me of a later scene..." → STOP. Park it.

## Cross-References

- **Called by:** writing-mode (Phase 4)
- **For stray ideas:** Park to parking lot (default: `00_Inbox/Parking_Lot.md`, check PROJECT_CONFIG.md)
- **For external research:** Invoke research
- **For prose polish:** Wait for writing-mode Phase 5

## Remember

- **User writes** - You're research assistant, not author
- **Scope tight** - Answer the question, nothing more
- **Park strays** - One line, return immediately
- **Explicit request only** - Prose writing is opt-in
