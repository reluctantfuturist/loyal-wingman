---
name: character-map
description: Show character relationships and detect orphans for a project - uses query-context and validate-links skills
allowed-tools:
  - Read
  - Grep
  - Glob
---

# /character-map

Display character appearances, relationships, and identify orphaned characters.

## Usage

```
/character-map                     # Default project (first found)
/character-map [ProjectName]       # Specific project
/character-map --orphans           # Focus on orphan detection
```

## Process

### Step 1: Query Project Context

**REQUIRED SUB-SKILL:** Invoke `query-context` with:
- Target: All scene files in `10_Projects/[Project]/Scenes/`
- Focus: Extract character references from frontmatter and prose

Query-context will search:
- Scene frontmatter for `pov_character`, `related_characters`
- `02_World/Characters/` for all character entries
- Character relationship sections

### Step 2: Build Character Map

From query-context results:

```
## [Project Name] - Character Map

### POV Characters
- **[Character Name]** - Ch 1, 2, 3 (POV all)

### Major Characters (3+ appearances)
- **[Character Name]** - Ch 1, 2, 3
  - Relationship: [relationship to protagonist]
- **[Character Name]** - Ch 1, 3
  - Relationship: [relationship type]

### Supporting Characters (1-2 appearances)
- **[Name]** - Ch [X]
  - Role: [brief description]

### Mentioned Only
- **[Name]** - Referenced in Ch [X]
```

### Step 3: Map Relationships

From character files' relationship sections:

```
### Relationship Web

[Protagonist]
├── [Character A] (relationship type)
├── [Character B] (relationship type)
└── [Character C] (relationship type)

Key Dynamics:
- [Character 1] ↔ [Character 2]: [dynamic description]
- [Character 1] ↔ [Character 3]: [dynamic description]
```

### Step 4: Validate Links

**REQUIRED SUB-SKILL:** Invoke `validate-links` to check:
- All character wikilinks in scenes resolve
- Character files link back to scenes they appear in
- Bidirectional linking between related characters

### Step 5: Identify Issues

```
### Potential Issues

**Missing World Bible Entry:**
- ⚠️ [Name] appears in Ch [X] but no entry in 02_World/Characters/
  → Use world-bible skill to create

**Orphaned Characters:**
- ⚠️ [Name] has world bible entry but doesn't appear in this project

**Link Issues:** (from validate-links)
- ⚠️ [issues reported by validate-links]

**Faction Mentions Without Detail:**
- ⚠️ [Faction] mentioned in Ch [X], no entry in 02_World/Factions/
  → Use world-bible skill to create
```

### Step 6: Recommendations

```
### Recommendations

**Create entries for:** (use world-bible skill)
- [Name] - appears prominently, needs world bible entry

**Update entries for:**
- [Name] - relationship changed, update character file

**Fix links:** (use validate-links skill)
- [Link issues]
```

## Skill Invocations

| Step | Required Sub-Skill |
|------|-------------------|
| Query context | `query-context` |
| Validate links | `validate-links` |
| Create missing entries | `world-bible` (if user approves) |
