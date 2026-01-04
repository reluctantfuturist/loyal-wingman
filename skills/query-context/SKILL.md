---
name: query-context
description: Search vault for scene context before writing. Use when user asks "what do we know about X", "find context for this scene", "check continuity", or needs canon/research lookup before drafting
allowed-tools:
  - Read
  - Grep
  - Glob
---

# Query Context

## The Iron Law

```
SEARCH COMPREHENSIVELY. Never invent missing information - identify gaps for user decision.
```

## When to Use

- Before drafting any scene (called by writing-mode)
- When user asks "what do we know about X"
- To verify continuity with existing canon

## The Process

### Phase 1: Identify Search Targets

From scene requirements, list:
- Characters involved
- Locations featured
- Equipment used
- Factions relevant
- Systems/magic elements
- Themes being explored
- Timeline context needed
- Previous scenes for continuity

### Phase 2: Search Vault

**Search ALL world bible folders:**

1. **Characters** - `02_World/Characters/`
   - Current status, relationships, equipment
   - Recent events affecting character

2. **Locations** - `02_World/Locations/`
   - Physical description, special properties
   - Previous events at location

3. **Equipment** - `02_World/Equipment/`
   - Technical specifications
   - Special properties, behaviors

4. **Factions** - `02_World/Factions/`
   - Structure, key members
   - Current status, goals

5. **Systems** - `02_World/Systems/`
   - Rules and costs
   - Mechanics and limitations
   - Character abilities

6. **Themes** - `02_World/Themes/`
   - Core thematic elements
   - Moral framework

7. **Timeline** - `02_World/Timeline_Events/`
   - Relevant historical events
   - Political/social backdrop

8. **Project scenes** - `10_Projects/[Project]/Scenes/`
   - Continuity with earlier chapters
   - Foreshadowing requirements

9. **Research** - `03_Research/`
   - Cultural authenticity
   - Technical accuracy

10. **Plot Threads** - Project index `## Plot Threads`
    - Active threads for this scene
    - Stale/orphaned thread warnings

**REQUIRED SUB-SKILL:** Invoke `plot-threads` (Query mode)

### Phase 3: Compile Findings

Format results as:

```
## Context for [Scene Description]

### Available Canon

**Characters:**
- [Name]: [relevant state/equipment/relationships] (source: file)

**Location:**
- [Name]: [key details] (source: file)

**Factions:**
- [Name]: [relevant involvement] (source: file)

**Systems:**
- [System]: [applicable rules/costs] (source: file)

**Themes:**
- [Theme]: [how it applies] (source: file)

**Timeline:**
- Scene takes place: [date/period]
- Relevant backdrop: [events]

**Equipment:**
- [Item]: [specs needed for scene] (source: file)

### Gaps Identified
- [Gap 1]: No vault entry found. Need user decision.
- [Gap 2]: Contradictory information in [file1] vs [file2].

### Research Needs
- [Topic]: Needs external research (flag for research)

### Continuity Flags
- Previous scene: [summary of state to maintain]
- Future scene: [setup requirements]
```

### Phase 4: Present for Decision

**WAIT for user input on gaps before proceeding.**

**Gap Types:**

| Gap Type | Question Format |
|----------|-----------------|
| **Missing World Element** | "I need [X] for this scene but found nothing. How does it fit? What are its key characteristics?" |
| **Character Decision** | "Character faces a choice. Option A: [consequences]. Option B: [different costs]. Which aligns with your vision?" |
| **Timeline Gap** | "Need to reference events between [date] and [date]. What happened? How did it affect [character]?" |
| **Tone Calibration** | "Scene could go darker/lighter. Current draft has [dark elements] and [hope moments]. Right balance?" |
| **Cultural Detail** | "Need authentic details about [cultural element]. Specific details? Personal experience? Misconceptions to avoid?" |
| **System Application** | "Scene requires [system] to [use]. What cost to character? How does it manifest? Does this expand/break rules?" |
| **Plot Development** | "Approaching [major event]. Right timing? Preparation needed? How does it affect overall arc?" |

For each gap, ask:
```
Gap: [description]
Options:
A: [specific option with consequences]
B: [alternative with different costs]
C: Create new canon entry (invoke world-bible)

Which aligns with your vision?
```

## Red Flags - STOP

If you catch yourself thinking:
- "I'll just make something up..." → STOP. Flag as gap.
- "This seems logical..." → STOP. Check vault first.
- "I remember from earlier..." → STOP. Search and cite.
- "That folder isn't relevant..." → STOP. Search ALL folders.

## Cross-References

- **Called by:** writing-mode (Phase 3)
- **Gaps needing research:** Flag for research
- **Gaps needing new canon:** Flag for world-bible
- **Plot thread context:** REQUIRED SUB-SKILL: plot-threads

## Remember

- **Search ALL folders** - Characters, Locations, Equipment, Factions, Systems, Themes, Timeline
- **Check plot threads** - Invoke plot-threads for active thread context
- **Cite sources** - Include file paths for verification
- **Flag, don't fill** - Gaps are for user decision
- **Continuity matters** - Check previous AND future scenes
