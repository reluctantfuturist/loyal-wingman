# Plot Threads Skill Design & Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Create a plot-threads skill that tracks narrative threads across a book, integrating with query-context and writing-mode.

**Architecture:** New atomic skill (`plot-threads`) with three modes (Query, Update, Audit). Integrates as sub-skill of query-context (before drafting) and writing-mode (after drafting). Stores threads in project index markdown table.

**Tech Stack:** Markdown skills, Edit tool for table manipulation

**Date**: 2026-01-03
**Status**: Approved
**GitHub Issue**: #2

## Overview

Create a new `plot-threads` skill for tracking narrative threads (mysteries, questions, foreshadowing, Chekhov's guns) across a book. The skill integrates at two points in the writing workflow:

1. **Before drafting** (via query-context): surfaces active threads relevant to current scene
2. **After drafting** (via writing-mode): proposes thread updates based on scene content

---

## Storage Location

Threads live in a `## Plot Threads` section within the project index file:

```
10_Projects/[Book Name]/[Book Name] Index.md
```

This keeps threads alongside chapter beat sheets, preventing drift between narrative planning and thread tracking.

---

## Table Structure

```markdown
## Plot Threads

| Thread | Type | Scope | Introduced | Status | Scenes |
|--------|------|-------|------------|--------|--------|
| Gagik's true nature | Mystery | Series | Ch1 | Developing | Ch1, Ch3, Ch4 |
| Sorochan breach | Question | Book 1 | Ch2 | Resolved | Ch2, Ch3 |
| Mom's deterioration | Mystery | Book 1 | Ch2 | Planted | Ch2 |
| Gagik's specimens | Foreshadowing | Series | Ch3 | Planted | Ch3 |
| Ch1 job offer | Chekhov | Book 1 | Ch1 | Planted | Ch1 |
```

### Columns

| Column | Description |
|--------|-------------|
| **Thread** | Short descriptive name |
| **Type** | Mystery, Question, Foreshadowing, or Chekhov |
| **Scope** | Book 1 (must resolve) or Series (can stay open) |
| **Introduced** | Chapter where first planted |
| **Status** | Planted, Developing, Resolved, or Abandoned |
| **Scenes** | Comma-separated list of chapters touching this thread |

### Thread Types

| Type | Description | Example |
|------|-------------|---------|
| **Mystery** | Reader question, answered gradually | "What is Gagik?" |
| **Question** | Character question, resolved in-story | "How did Sorochan know?" |
| **Foreshadowing** | Planted for reread payoff | "Gagik's specimens" |
| **Chekhov** | Specific object/detail that must pay off | "Ammunition count", "job offer" |

### Statuses

| Status | Description |
|--------|-------------|
| **Planted** | Introduced but not yet developed |
| **Developing** | Actively being explored across scenes |
| **Resolved** | Paid off or answered |
| **Abandoned** | Intentionally dropped (for tracking) |

---

## Workflow Integration

### query-context Integration

When query-context runs (writing-mode Phase 3), it invokes plot-threads to surface relevant threads:

```markdown
## Active Plot Threads for Ch4

**Developing:**
- Gagik's true nature (Mystery, Series) — last touched Ch3

**Planted (needs development):**
- Mom's deterioration (Mystery, Book 1) — planted Ch2, not yet developed

**Warnings:**
- ⚠ "Sorochan breach" resolved in Ch3 — verify no loose ends
```

This gives the writer context before drafting: which threads to advance, which are overdue.

### writing-mode Integration

After scene completion (Phase 6), writing-mode invokes plot-threads to update the registry:

1. Skill reads the completed scene
2. Cross-references against existing threads
3. Proposes updates:

```markdown
## Plot Thread Updates for Ch4

**Proposed changes:**
- Mom's deterioration: Planted → Developing (add Ch4)
- Gagik's true nature: add Ch4 to scenes

**New thread detected:**
- "Rift behavior change" — Type? Scope?

**No changes detected for:**
- Ch1 job offer (Chekhov) — still planted

Confirm, adjust, or add more?
```

4. User confirms or adjusts
5. Skill updates the project index table

---

## Warnings

### 1. Orphaned Threads (during query-context)

Triggered when a Book 1-scoped thread is still Planted late in the book:

```
⚠ ORPHANED: "Ch1 job offer" (Chekhov, Book 1) — still Planted in Ch8
   Consider: develop or mark Abandoned
```

### 2. Stale Threads (during query-context)

Type-dependent thresholds:

| Type | Stale After |
|------|-------------|
| Mystery | 4+ chapters without mention |
| Question | 2+ chapters without mention |
| Foreshadowing | No warning (slow burn by design) |
| Chekhov | No warning (end-of-book check only) |

```
⚠ STALE: "Mom's deterioration" (Mystery) — last touched Ch2, now Ch7
   Consider: revisit or mark Abandoned
```

### 3. Chekhov Violations (end-of-book check)

When final chapter is marked complete:

```
⚠ CHEKHOV UNRESOLVED: "Ch1 job offer" — planted Ch1, never paid off
   Consider: add payoff scene or remove setup in revision
```

### 4. Resolution Check (end-of-book)

Lists all Book 1-scoped threads not marked Resolved:

```markdown
## Book 1 Thread Resolution Check

✓ Sorochan breach — Resolved (Ch3)
✗ Mom's deterioration — Developing (needs resolution)
✗ Ch1 job offer — Planted (Chekhov violation)
○ Gagik's true nature — Series scope (okay to leave open)
```

---

## Skill Structure

### File Location

```
skills/plot-threads/SKILL.md
```

### Frontmatter

```yaml
---
name: plot-threads
description: Track plot threads, setups/payoffs, and narrative continuity. Use when user says "check threads", "what's unresolved", or called by query-context/writing-mode
allowed-tools:
  - Read
  - Edit
  - Grep
  - Glob
---
```

### Invocation Modes

| Mode | Triggered By | Action |
|------|--------------|--------|
| **Query** | query-context, "check threads" | Surface active threads, show warnings |
| **Update** | writing-mode Phase 6, "update threads" | Propose changes based on scene |
| **Audit** | "thread audit", final chapter complete | Full resolution check, Chekhov violations |

### Cross-References

- **Called by:** query-context (Query mode), writing-mode (Update mode)
- **Manual triggers:** "check threads", "update threads", "thread audit"
- **Reads from:** Project index `## Plot Threads` section
- **Writes to:** Same section via Edit tool

---

## Files Modified

| File | Changes |
|------|---------|
| `skills/plot-threads/SKILL.md` | **NEW**: Plot thread tracking skill |
| `skills/query-context/SKILL.md` | Add plot-threads invocation (Query mode) |
| `skills/writing-mode/SKILL.md` | Add Phase 6: Plot Thread Update |
| `README.md` | Add plot-threads to skill lists |
| `.claude-plugin/plugin.json` | Version bump to 0.2.0 |

---

## Implementation Order

1. Create `skills/plot-threads/SKILL.md`
2. Update `skills/query-context/SKILL.md` to invoke plot-threads
3. Update `skills/writing-mode/SKILL.md` to add Phase 6
4. Update `README.md` with new skill
5. Bump version in `.claude-plugin/plugin.json`
6. Close GitHub issue #2

---

## Out of Scope

- Automatic thread detection from prose (skill proposes, user confirms)
- Cross-book thread tracking dashboard
- Thread visualization/graph view
- Integration with Obsidian plugins

---

# Implementation Tasks

## Task 1: Create plot-threads Skill

**Files:**
- Create: `skills/plot-threads/SKILL.md`

**Step 1: Create skill directory**

```bash
mkdir -p skills/plot-threads
```

**Step 2: Write the skill file**

Create `skills/plot-threads/SKILL.md` with complete skill content following the pattern of voice-checker:
- Frontmatter (name, description, allowed-tools)
- Iron Law
- When to Use
- The Process (Query Mode, Update Mode, Audit Mode phases)
- Warning Thresholds table
- Report Templates
- Red Flags - STOP
- Cross-References
- Remember

**Step 3: Verify skill structure**

```bash
head -50 skills/plot-threads/SKILL.md
```

Expected: Frontmatter and Iron Law visible

**Step 4: Commit**

```bash
git add skills/plot-threads/SKILL.md
git commit -m "feat: add plot-threads skill for narrative thread tracking"
```

---

## Task 2: Update query-context to Invoke plot-threads

**Files:**
- Modify: `skills/query-context/SKILL.md`

**Step 1: Add plot-threads to Phase 2 searches**

After line 78 (after "Research" search), add a new section:

```markdown
10. **Plot Threads** - Project index `## Plot Threads`
    - Active threads for this scene
    - Stale/orphaned thread warnings

**REQUIRED SUB-SKILL:** Invoke `plot-threads` (Query mode)
```

**Step 2: Update Cross-References section**

Add plot-threads to the Cross-References:

```markdown
- **Plot thread context:** REQUIRED SUB-SKILL: plot-threads
```

**Step 3: Verify changes**

```bash
grep -n "plot-threads" skills/query-context/SKILL.md
```

Expected: Multiple matches showing integration

**Step 4: Commit**

```bash
git add skills/query-context/SKILL.md
git commit -m "feat: integrate plot-threads into query-context"
```

---

## Task 3: Update writing-mode to Add Phase 6

**Files:**
- Modify: `skills/writing-mode/SKILL.md`

**Step 1: Renumber existing phases**

Current Phase 6 (Technical Review) becomes Phase 7, Phase 7 (Exit) becomes Phase 8.

**Step 2: Insert new Phase 6: Plot Thread Update**

After Phase 5 (Polish Prose), add:

```markdown
### Phase 6: Plot Thread Update

**REQUIRED SUB-SKILL:** Invoke `plot-threads` (Update mode)

The plot-threads skill will:
1. Read completed scene
2. Cross-reference against existing threads in project index
3. Propose status changes (Planted → Developing → Resolved)
4. Suggest new threads detected in scene
5. Wait for user confirmation
6. Update project index `## Plot Threads` table

**On completion:** Proceed to Technical Review
```

**Step 3: Update Subskill Invocation Summary table**

Add new row for Phase 6 and renumber subsequent phases.

**Step 4: Update Cross-References**

Add:
```markdown
- **Plot thread updates:** REQUIRED SUB-SKILL: plot-threads
```

**Step 5: Verify changes**

```bash
grep -n "Phase" skills/writing-mode/SKILL.md | head -20
```

Expected: Phases 1-8 in correct order

**Step 6: Commit**

```bash
git add skills/writing-mode/SKILL.md
git commit -m "feat: add plot-threads phase to writing-mode workflow"
```

---

## Task 4: Update README

**Files:**
- Modify: `README.md`

**Step 1: Add plot-threads to Support Skills list**

In the "### Support Skills" section, add:

```markdown
- **plot-threads** - Track narrative threads, setups/payoffs, Chekhov's guns
```

**Step 2: Update Skills Reference table**

Add new row:

```markdown
| plot-threads | query-context, writing-mode, Manual | Track narrative threads |
```

**Step 3: Verify changes**

```bash
grep -n "plot-threads" README.md
```

Expected: Two matches (Support Skills and Skills Reference)

**Step 4: Commit**

```bash
git add README.md
git commit -m "docs: add plot-threads to README skill lists"
```

---

## Task 5: Bump Version

**Files:**
- Modify: `.claude-plugin/plugin.json`

**Step 1: Update version**

Change `"version": "0.1.0"` to `"version": "0.2.0"`

**Step 2: Verify change**

```bash
cat .claude-plugin/plugin.json | grep version
```

Expected: `"version": "0.2.0"`

**Step 3: Commit**

```bash
git add .claude-plugin/plugin.json
git commit -m "chore: bump version to 0.2.0"
```

---

## Task 6: Create Pull Request

**Step 1: Push branch**

```bash
git push -u origin feature/plot-threads
```

**Step 2: Create PR**

```bash
gh pr create --title "Add plot-threads skill for narrative thread tracking" --body "$(cat <<'EOF'
## Summary

- **New skill: `plot-threads`** — Track narrative threads (mysteries, questions, foreshadowing, Chekhov's guns) across a book
- **query-context integration** — Surfaces active threads before drafting
- **writing-mode integration** — Proposes thread updates after scene completion
- **Warning system** — Orphaned threads, stale threads, Chekhov violations, end-of-book resolution check

## New Files

- `skills/plot-threads/SKILL.md` — The new skill

## Modified Files

- `skills/query-context/SKILL.md` — Invokes plot-threads (Query mode)
- `skills/writing-mode/SKILL.md` — Adds Phase 6: Plot Thread Update
- `README.md` — Adds plot-threads to skill lists
- `.claude-plugin/plugin.json` — Version bump to 0.2.0

## Test plan

- [ ] Invoke plot-threads manually with "check threads"
- [ ] Verify query-context surfaces active threads
- [ ] Verify writing-mode prompts for thread updates after scene
- [ ] Test warning generation for stale/orphaned threads

Closes #2

🤖 Generated with [Claude Code](https://claude.com/claude-code)
EOF
)"
```

**Step 3: Verify PR created**

```bash
gh pr view
```

Expected: PR details displayed
