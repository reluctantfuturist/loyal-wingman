---
name: writing-mode
description: Use when producing prose for current chapter/scene - enforces focus, dispatches atomic subskills, captures strays to parking lot
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - TodoWrite
---

# Writing Mode

## The Iron Law

```
STAY IN THE CURRENT SCENE. Dispatch subskills for each phase. Capture strays, don't chase them.
```

## When to Use

- "writing mode" / "let's write" / "work on chapter X"
- Starting or continuing a scene draft
- Any prose production work

## The Process

### Phase 1: Establish Focus

1. Identify current scene: project, chapter, scene number
2. State: "WRITING MODE: Working on [Project] Chapter [X]"
3. Create TodoWrite with scene phases

### Phase 2: Review/Create Outline

**REQUIRED SUB-SKILL:** Invoke `outliner`

The outliner skill will:
1. Check for existing outline in project index or scene file
2. If exists: present beats, note discovery zones, confirm ready
3. If not: offer outline depth options (discovery/compass/beat sheet)
4. Gather scene elements (goal, obstacle, value shift, emotional core)
5. Save outline to project index or scene frontmatter

**On outliner completion:**
- Review outline summary
- Note discovery zones to respect during drafting
- Proceed to query-context phase

### Phase 3: Query Context

**REQUIRED SUB-SKILL:** Invoke `query-context`

The query-context skill will:
1. Search ALL world bible folders (Characters, Locations, Equipment, Factions, Systems, Themes, Timeline)
2. Check project scenes for continuity
3. Search research archive
4. Identify gaps needing user decision
5. Flag research needs

**On query-context completion:**
- Review gaps with user
- For research needs: REQUIRED SUB-SKILL: `research`
- For new canon needs: Flag for thinking-mode (not during writing-mode)
- Proceed only when blocking issues resolved

### Phase 4: Support User Drafting

**REQUIRED SUB-SKILL:** Invoke `draft-support`

The draft-support skill will:
1. Answer questions about established canon
2. Provide research results on request
3. Capture stray ideas to parking lot
4. **NEVER write draft prose unless explicitly requested**

**Parking Lot Location:** `00_Inbox/Parking_Lot.md`

### Phase 5: Polish Prose

When user signals draft complete:

**REQUIRED SUB-SKILL:** Invoke `prose-editor`

The prose-editor skill will:
1. Read project Style Guide for project-specific patterns
2. Scan for AI patterns and voice drift
3. Present teaching feedback with quotes
4. Wait for approval before edits

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

### Phase 7: Technical Review

After prose polish approved, use the **Task tool** to dispatch a technical review agent:

```
Task tool parameters:
  subagent_type: Explore
  description: Technical accuracy review
  prompt: |
    Review [scene file path] for technical accuracy against the vault:

    1. Equipment specs match 02_World/Equipment/ and 03_Research/
    2. Technical details accurate (verify against research files)
    3. Action clarity (who moves where, spatial relationships)
    4. Timeline consistency with 02_World/Timeline_Events/
    5. Geographic accuracy against 03_Research/Geography/
    6. Continuity with previous/future scenes

    For each issue found:
    - Quote exact text from scene
    - Cite source file with correct information
    - Propose specific fix

    Return a structured report grouped by severity.
```

**Present agent findings to user for approval before any fixes.**

### Phase 8: Exit

Trigger exit when:
- User says "done" / "pause" / "stop writing"
- Scene marked complete
- User requests "thinking-mode"

On exit: "Exiting WRITING MODE. [X] items in parking lot."

## Subskill Invocation Summary

| Phase | Required Sub-Skill |
|-------|-------------------|
| 2. Review/Create Outline | `outliner` |
| 3. Query Context | `query-context` |
| 3. Research (if gaps) | `research` |
| 4. Drafting Support | `draft-support` |
| 5. Polish | `prose-editor` |
| 6. Plot Thread Update | `plot-threads` |
| 7. Technical Review | Task tool (Explore agent) |

## Red Flags - STOP

If you catch yourself thinking:
- "This reminds me of a future book..." → STOP. Park it via draft-support.
- "We should also update the world bible..." → STOP. Flag for thinking-mode.
- "Let me explore this theme..." → STOP. That's thinking-mode.
- "What if in the future..." → STOP. Park it via draft-support.
- "I can skip the query phase..." → STOP. Always invoke query-context.

## Cross-References

- **Outline phase:** REQUIRED SUB-SKILL: outliner
- **Query phase:** REQUIRED SUB-SKILL: query-context
- **Research needs:** REQUIRED SUB-SKILL: research
- **Drafting support:** REQUIRED SUB-SKILL: draft-support
- **Polish phase:** REQUIRED SUB-SKILL: prose-editor
- **Plot thread updates:** REQUIRED SUB-SKILL: plot-threads
- **For open-ended brainstorming:** Switch to thinking-mode
- **For new canon:** Flag for thinking-mode (world-bible)

## Remember

- **Check for outline first** - Read existing beats or offer to create
- **Invoke subskills** - Each phase has a required skill
- **User writes the draft** - Support, don't supplant
- **Park strays immediately** - Via draft-support
- **Three-stage review** - Prose (prose-editor), threads (plot-threads), technical
- **Discovery zones are sacred** - Don't over-plan what's marked flexible
