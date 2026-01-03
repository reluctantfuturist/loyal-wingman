---
name: world-bible
description: Create and maintain world bible entries with proper cross-linking. Use when user says "add a character", "create location entry", "update the world bible", or needs to document new canon for characters, locations, equipment, factions, systems, or themes
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - WebSearch
  - WebFetch
---

# World Bible

Create and maintain canonical world bible entries with heavy cross-linking, proper knowledge graph structure, and consistency verification.

## The Iron Law

```
QUERY BEFORE CREATE. Check for existing entries and conflicts. Link bidirectionally.
```

## Core Principles

**TWO-TIER LINKING STRATEGY**:
- **Story files (Scenes)**: Minimal/no wikilinks in prose - publication-ready
- **World Bible & Meta files**: Heavy cross-linking for knowledge graph

**NEVER ASSUME**: Search first, ask second, create last. The sparse vault is a feature.

**CANONICAL REFERENCE**: World bible is single source of truth for all story elements.

## When to Use

- Creating new character in `02_World/Characters/`
- Creating new location in `02_World/Locations/`
- Creating new equipment in `02_World/Equipment/`
- Creating new faction in `02_World/Factions/`
- Creating new timeline event in `02_World/Timeline_Events/`
- Creating new system in `02_World/Systems/`
- Creating new theme in `02_World/Themes/`
- Updating existing world bible entries with new canon
- Called by thinking-mode for structured worldbuilding output

## The Process

### Phase 1: Query Existing (ALWAYS FIRST)

Before creating, search for:
- Existing entity with same/similar name
- Related entities that should reference this one
- Conflicting information in vault
- Research backing in `03_Research/`

**If entity exists**: Update, don't duplicate.
**If similar exists**: Ask user before creating new one.
**If nothing found**: Ask user before inventing.

### Phase 2: Design Phase (User Collaboration)

**Stop and ask**:
```
I need to create [Entity Type: Character/Location/Equipment/etc].

From vault search I found:
- [What exists]
- [What's missing]
- [Potential conflicts]

Questions:
- [Specific design question 1]
- [Specific design question 2]

Options:
A: [Approach A with implications]
B: [Approach B with different costs]
```

**For Characters:**
- Full name (with culturally appropriate naming conventions)
- Role in story (main, supporting, background)
- Key relationships
- Timeline position (when active)

**For Locations:**
- Name and region/area
- Special properties (if any)
- Key events that happen here
- Sensory anchors (smell, sound, texture)

**For Equipment:**
- Exact specifications (model, type, etc.)
- Source (research reference if real-world)
- Story function

**For Themes:**
- Core statement (what the theme explores)
- How it manifests in story (through which characters, events, systems)
- Thematic questions (what the story asks, not answers)
- Related themes (tension, reinforcement, contrast)

### Phase 3: Create Entry (After Approval)

1. Read appropriate template from `01_Meta/Templates/`
2. Fill with gathered information
3. Use proper file naming (see File Naming Standards)
4. Include all required frontmatter fields
5. Write to correct location

| Type | Template | Location |
|------|----------|----------|
| Character | `01_Meta/Templates/_character.md` | `02_World/Characters/` |
| Location | `01_Meta/Templates/_location.md` | `02_World/Locations/` |
| Equipment | `01_Meta/Templates/_equipment.md` | `02_World/Equipment/` |
| Faction | `01_Meta/Templates/_faction.md` | `02_World/Factions/` |
| Event | `01_Meta/Templates/_event.md` | `02_World/Timeline_Events/` |
| System | `01_Meta/Templates/_system.md` | `02_World/Systems/[category]/` |
| Theme | `01_Meta/Templates/_theme.md` | `02_World/Themes/` |

### Phase 4: Cross-Reference (MANDATORY)

**Every world bible entry MUST include**:

#### Relationships Section
Link to all related characters:
```markdown
## Relationships
- [[Character Name]] - relationship type and context
- [[Other Character]] - relationship type and context
```

#### Appears In Section
Reference scenes without direct links:
```markdown
## Appears In
- Project Name, Scene Title - brief context
```

#### Related Section
Link to locations, equipment, events, systems:
```markdown
## Related
- [[Location Name]] - why relevant
- [[Equipment Name]] - why relevant
```

### Phase 5: Bidirectional Linking (CRITICAL)

**When A links to B, ensure B references A back**.

1. Identify all entities that should link TO this entry
2. Identify all entities this entry should link TO
3. Update each related file with wikilink
4. Verify all links resolve

**Verification checklist**:
- [ ] Created new link to Entity X?
- [ ] Opened Entity X and added reference back?
- [ ] Context provided in both directions?

### Phase 6: Validate Links

**REQUIRED SUB-SKILL:** Invoke `validate-links`

Validate-links will verify:
- All wikilinks resolve to actual files
- Bidirectional linking is complete
- No orphaned entries created

### Phase 7: Confirm Creation

Report:
```
Created: 02_World/[Type]/[Name].md

Outgoing links:
- [[Entity 1]] ✓
- [[Entity 2]] ✓

Incoming links added:
- [[Entity A]].md updated ✓
- [[Entity B]].md updated ✓

Validation: [status from validate-links]
```

## File Naming Standards

**USE SPACES for readability** (standard pattern):
```
02_World/Characters/First Last.md
02_World/Locations/Location Name.md
02_World/Equipment/Item Name.md
02_World/Factions/Faction Name.md
02_World/Systems/Category/System Name.md
```

**Before creating**: Check existing naming patterns in target directory.

## Entity Type Standards

### Character Sheets

**Required sections**:
- Basic Info (name, aliases, age, background)
- Physical Description (grounded, specific)
- Psychological Profile (voice, motivations, patterns)
- Background (history, formative events)
- Abilities/Skills (with limitations)
- Equipment (link to equipment entries)
- Relationships (all character links)
- Character Arc (if major character)
- Appears In (scene references)
- Related (locations, events, systems)

**Voice capsule required for POV characters**:
```markdown
### Voice
- Internal: [thinking style]
- Dialogue: [speech patterns]
- Patterns: "[recurring phrases or thoughts]"
- Never: [off-limits behaviors/phrases]
```

### Location Entries

**Required sections**:
- Location Type (category)
- Physical Description (concrete details, sensory anchors)
- Special Properties (if any)
- Historical Context
- Current State
- Notable Residents/Occupants
- Related Events
- Appears In
- Related (characters, factions, equipment)

### Equipment Entries

**Required sections**:
- Technical Specifications
- Physical Properties
- Operational Characteristics
- Special Properties (if any)
- Cost of Use (limitations, maintenance)
- History (provenance)
- Current Owner
- Appears In
- Related

### Faction Entries

**Required sections**:
- Faction Type
- Structure
- Goals and Methods
- Territory/Sphere of Influence
- Resources
- Key Members (link to characters)
- Relationships (allies, enemies)
- Historical Context
- Current State
- Appears In
- Related

### System Entries

**Required sections**:
- Overview (what this system governs)
- Core Rules
- Cost Structure (if applicable)
- Manifestation (how it appears in story)
- Limitations
- Examples (from scenes)
- Related Systems
- Characters Who Use This
- Appears In

## Frontmatter Standards

**All world bible entries**:
```yaml
---
type: character|location|equipment|faction|system|theme|event
status: canon|draft|deprecated
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [relevant, tags, here]
---
```

## Link Format Standards

**Readable names**: `[[Character Name]]` NOT `[[char.name]]`

**Exact filename matching**: Links must resolve to actual vault files.

**Context required**: Don't just link - explain WHY linked.

Bad:
```markdown
## Related
- [[Location Name]]
```

Good:
```markdown
## Related
- [[Location Name]] - Primary base of operations, appears in Chapters 1-3
```

## Research Integration

**Always cross-reference** `03_Research/`:
- Cultural details → `03_Research/Culture/`
- Historical context → `03_Research/History/`
- Technical specs → `03_Research/Equipment/` or `Technology/`
- Geographic info → `03_Research/Geography/`

**Cite research files** when making canonical claims.

## Update Protocol

**When scene introduces new canon**:
1. Read scene thoroughly
2. Identify new canonical facts
3. Check which world bible entries need updates
4. Update entries with new information
5. Add scene reference to "Appears In" sections
6. Create new entries if needed (with user approval)
7. Verify cross-references are bidirectional

## Red Flags - STOP

If you catch yourself thinking:
- "I'll create this quickly..." → STOP. Query first.
- "Links can be added later..." → STOP. Link now.
- "This is similar enough..." → STOP. Check for duplicates.
- "I'll use a different template..." → STOP. Use standard templates.

**Emergency Stops - ALWAYS confirm with user before creating:**
- Major world element (new faction, new rule/system)
- Change to established character trait
- Significant backstory addition
- New faction or group
- New system rule
- Major timeline event

These require explicit user approval, not just confirmation that you're about to create them.

## Quality Checklist

Before finalizing any world bible entry:

- [ ] Searched for existing/similar entries?
- [ ] Used proper template?
- [ ] All required sections present?
- [ ] Frontmatter complete and accurate?
- [ ] File named according to standards?
- [ ] All wikilinks resolve to real files?
- [ ] Bidirectional linking verified?
- [ ] Context provided for all links?
- [ ] "Appears In" section complete?
- [ ] Cross-referenced with research files?
- [ ] Costs/limitations clearly stated?
- [ ] Voice consistent with project style?

## Cross-References

- **Called by:** thinking-mode
- **After creation:** REQUIRED SUB-SKILL: validate-links
- **For research backing:** research skill
- **Templates:** `01_Meta/Templates/`

## Remember

- **Query first** - Duplicates cause confusion
- **Use templates** - Consistency matters
- **Link immediately** - Orphan entries break navigation
- **Validate links** - Use validate-links skill
- **Sparse vault is a feature** - Empty spaces = opportunities for user input
- **Knowledge graph matters** - Rich connections in world bible, clean scene files
- **Canon is sacred** - World bible is single source of truth
- **When in doubt, ask** - User vision trumps AI creativity always
