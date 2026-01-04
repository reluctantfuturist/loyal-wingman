---
name: plot-threads
description: Track plot threads, setups/payoffs, and narrative continuity. Use when user says "check threads", "what's unresolved", or called by query-context/writing-mode
allowed-tools:
  - Read
  - Edit
  - Grep
  - Glob
---

# Plot Threads

Track narrative threads (mysteries, questions, foreshadowing, Chekhov's guns) across a book.

## The Iron Law

```
PROPOSE, DON'T IMPOSE. Read scene, suggest thread updates, wait for user confirmation before editing.
```

## When to Use

- Called by query-context (Query mode) - before drafting
- Called by writing-mode Phase 6 (Update mode) - after drafting
- "check threads" / "what's unresolved" / "thread audit"
- Before marking final chapter complete

## Thread Storage

Threads live in the project index file:

```
10_Projects/[Book Name]/[Book Name] Index.md
```

### Table Structure

```markdown
## Plot Threads

| Thread | Type | Scope | Introduced | Status | Scenes |
|--------|------|-------|------------|--------|--------|
| Gagik's true nature | Mystery | Series | Ch1 | Developing | Ch1, Ch3, Ch4 |
| Sorochan breach | Question | Book 1 | Ch2 | Resolved | Ch2, Ch3 |
| Gagik's specimens | Foreshadowing | Series | Ch3 | Planted | Ch3 |
| Ch1 job offer | Chekhov | Book 1 | Ch1 | Planted | Ch1 |
```

### Thread Types

| Type | Description | Stale After |
|------|-------------|-------------|
| **Mystery** | Reader question, answered gradually | 4+ chapters |
| **Question** | Character question, resolved in-story | 2+ chapters |
| **Foreshadowing** | Planted for reread payoff | No warning |
| **Chekhov** | Object/detail that must pay off | End-of-book only |

### Statuses

- **Planted** — Introduced but not yet developed
- **Developing** — Actively being explored
- **Resolved** — Paid off or answered
- **Abandoned** — Intentionally dropped

### Scope

- **Book 1** (or current book) — Must resolve before book ends
- **Series** — Can remain open across books

## The Process

### Query Mode (Before Drafting)

Called by query-context to surface relevant threads.

**Phase 1: Locate Project Index**

1. Identify current project from scene path
2. Find project index: `10_Projects/[Book]/[Book] Index.md`
3. Read `## Plot Threads` section

**If no Plot Threads section exists:**
- Report: "No plot threads tracked yet. Create initial registry?"
- If user confirms, create empty table structure

**Phase 2: Identify Relevant Threads**

1. Get current chapter number from scene
2. Filter threads where Scenes column includes nearby chapters
3. Identify threads by status: Developing, Planted

**Phase 3: Check for Warnings**

Scan for issues:

**Orphaned Threads:**
- Book-scoped thread still Planted in late chapters (Ch7+)
- `⚠ ORPHANED: "[Thread]" (Type, Scope) — still Planted in Ch[X]`

**Stale Threads:** (thresholds per Thread Types table above)
- `⚠ STALE: "[Thread]" (Type) — last touched Ch[X], now Ch[Y]`

**Phase 4: Generate Report**

```markdown
## Active Plot Threads for Ch[X]

**Developing:**
- [Thread] (Type, Scope) — last touched Ch[X]

**Planted (needs development):**
- [Thread] (Type, Scope) — planted Ch[X], not yet developed

**Warnings:**
- ⚠ [Warning message]

**Recently Resolved:**
- [Thread] — resolved Ch[X]
```

### Update Mode (After Drafting)

Called by writing-mode Phase 6 after scene completion.

**Phase 1: Read Completed Scene**

1. Read the scene file completely
2. Note chapter number, characters, key events
3. Identify potential thread touchpoints

**Phase 2: Load Existing Threads**

1. Read project index `## Plot Threads` table
2. Parse into structured list

**Phase 3: Propose Updates**

Cross-reference scene against threads:

```markdown
## Plot Thread Updates for Ch[X]

**Proposed changes:**
- [Thread]: Planted → Developing (add Ch[X])
- [Thread]: add Ch[X] to scenes
- [Thread]: Developing → Resolved

**New threads detected:**
- "[Description]" — Type? Scope?

**No changes detected for:**
- [Thread] (Chekhov) — still planted

Confirm, adjust, or add more?
```

**Phase 4: Wait for User Confirmation**

**STOP and wait.** User may confirm, adjust, add, or reject proposals.

**Phase 5: Apply Updates**

After confirmation:
1. Use Edit tool to update `## Plot Threads` table
2. Report changes made

### Audit Mode (End of Book)

Triggered manually via "thread audit" or "book complete" commands.

**Phase 1: Full Thread Scan**

Read all threads from project index.

**Phase 2: Resolution Check**

Categorize all threads:

```markdown
## Book [X] Thread Resolution Check

### Resolved
✓ [Thread] — Resolved (Ch[X])

### Unresolved (Book Scope)
✗ [Thread] (Type) — Status: [Developing/Planted]
  → Needs resolution or scope change to Series

### Chekhov Violations
⚠ [Thread] — planted Ch[X], never paid off
  → Add payoff scene or remove setup in revision

### Series Threads (OK to leave open)
○ [Thread] — [Status], continues in future books

### Abandoned
⊘ [Thread] — intentionally dropped Ch[X]
```

**Phase 3: Recommendations**

For each unresolved Book-scoped thread:
- Suggest resolution approach, OR
- Suggest changing scope to Series, OR
- Suggest marking Abandoned with reason

## Red Flags - STOP

If you catch yourself thinking:
- "I'll just update the table..." → STOP. Propose first, wait for confirmation.
- "This thread is obviously resolved..." → STOP. Let user confirm.
- "I'll create a new thread without asking..." → STOP. Propose new threads, don't add.
- "The user probably wants..." → STOP. Ask, don't assume.

## Cross-References

- **Called by:** query-context (Query mode), writing-mode (Update mode)
- **Manual triggers:** "check threads", "update threads", "thread audit"
- **Storage location:** `10_Projects/[Book]/[Book] Index.md` → `## Plot Threads`
- **Design document:** `docs/plans/2026-01-03-plot-threads-design.md`

## Remember

- **Propose, don't impose** — Always wait for user confirmation before editing
- **Locate project index first** — Threads live in the book's index file
- **Type-dependent warnings** — Mysteries simmer longer than Questions
- **Scope matters** — Book-scoped threads must resolve; Series threads can stay open
- **Chekhov = end-of-book** — Only flag Chekhov items during Audit mode
- **Create table if missing** — Offer to initialize `## Plot Threads` section
