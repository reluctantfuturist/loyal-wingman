---
name: research
description: Find, validate, and archive research with proper sourcing. Use when user asks "research X for me", "what's accurate about Y", "I need facts on Z", or when scene needs real-world grounding for cultural/technical/historical accuracy
model: haiku
allowed-tools:
  - WebSearch
  - WebFetch
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - Bash
---

# Research

Find, validate, and archive research that grounds fiction in authentic culture, accurate technical specifications, and verifiable context.

## The Iron Law

```
SOURCE EVERYTHING. No research note without URL/date. Save to 03_Research/ with proper metadata.
```

## Core Mission

**Fight the Wikipedia-tourist trap**: Move beyond surface-level details to lived experience, technical precision, and period-specific accuracy.

**Serve the story**: Research should deepen atmosphere, illuminate setting, and ground fiction in concrete reality.

## When to Use

- When scene needs real-world accuracy (called by writing-mode)
- When user asks for research on topic
- When query-context identifies research gaps
- When creating entity that needs real-world grounding
- Called by thinking-mode for research needs
- Cultural authenticity questions
- Technical specifications needed
- Historical accuracy required

## Research Categories

Organized by `03_Research/` subdirectories:

### Culture/
- Language patterns, slang, colloquialisms
- Social customs and daily life
- Subcultural groups and communities
- Food, drink, and domestic rituals
- Generational and class distinctions

### History/
- Political climate and events
- Economic conditions
- Social movements
- Cultural shifts
- Period-specific context

### Technology/
- Period-appropriate tech
- Infrastructure state
- Communication methods
- Transportation
- Tools and equipment

### Geography/
- Location characteristics
- Routes and distances
- Landmarks and notable places
- Environmental details
- How geography affects story

### Equipment/
- Technical specifications
- Operational characteristics
- Availability and access
- Maintenance and limitations
- Costs and consequences of use

## The Process

### Phase 1: Define Research Need

Clarify:
- What specific information is needed?
- What time period? (check project settings for relevant era)
- What category? (Culture, History, Geography, Equipment, Technology)
- What depth? (Quick fact vs. deep dive)

**Ask first**:
```
This scene needs [specific detail].

I'll research:
- [Search query 1]
- [Search query 2]

Should I focus on anything specific?
Is there personal knowledge I should incorporate first?
```

### Phase 2: Check Existing Research

Search `03_Research/` for:
- Existing notes on this topic
- Related research that might contain answer
- Previously validated sources

**If found:** Present existing research, ask if more needed.

### Phase 3: Source Evaluation

**Priority hierarchy**:

**Tier 1 - Lived Experience** (ALWAYS ASK USER FIRST):
- Writer's personal knowledge
- Direct cultural experience
- Family/friend accounts
- Local perspective

**Tier 2 - Primary Sources**:
- Period news archives
- Government data from era
- Contemporary photography/video
- Academic ethnography
- Technical manuals

**Tier 3 - Specialized Secondary**:
- Subject-matter expert analysis
- Technical specifications from manufacturers
- Historical scholarship with citations
- Investigative journalism from period

**Tier 4 - General Secondary** (USE WITH CAUTION):
- Contemporary journalism
- Documentary sources
- Reputable cultural analysis
- Cross-verified encyclopedia entries

**AVOID**:
- Single-source claims
- Tourist guides and superficial blogs
- Stereotypical generalizations
- Sources from wrong time period

### Phase 4: External Research

Use WebSearch and WebFetch to find:
- Primary sources preferred
- Academic/professional sources over blogs
- Period-appropriate sources for historical topics

**For each source, capture:**
- URL
- Access date
- Key facts extracted
- Reliability assessment

**Search Strategy:**
- Period-specific date ranges
- Regional sources for authenticity
- Technical forums for equipment specs
- Academic sources for historical analysis

**Multi-source verification**: Never rely on single source for critical details.

### Phase 5: Validate Information

Cross-reference claims:
- Does this match user's lived experience? (ASK)
- Do multiple sources agree?
- Is this period-appropriate?
- Does this align with established canon in vault?
- Are there contradictions with existing research files?

**Red flags**:
- Too perfect/convenient details
- Matches stereotypes exactly
- Single-source exotic claims
- Contradicts multiple other sources
- Feels "too Hollywood"

**Flag uncertain information clearly.**

### Phase 6: Document Findings

Create research note in appropriate location:

```
03_Research/
├── Culture/        # Social, linguistic, cultural context
├── Equipment/      # Weapons, tools, gear
├── Geography/      # Locations, maps, routes
├── History/        # Events, periods, politics
└── Technology/     # Technical systems
```

**Filename pattern**: `[Topic] - [Specific Focus].md`
- Use spaces for readability
- Be specific: not "City.md" but "City District - Neighborhood History.md"

**Use template from** `01_Meta/Templates/_research.md`

**Required frontmatter:**
```yaml
---
type: research
category: culture|history|technology|geography|equipment
topic: [specific topic]
status: verified|preliminary|needs-validation
created: YYYY-MM-DD
updated: YYYY-MM-DD
period: [relevant time period]
sources:
  - url: [URL]
    accessed: [YYYY-MM-DD]
    reliability: [high|medium|low]
reliability: high|medium|low
tags: [relevant, tags, here]
related_world_entries:
  - "[[Entity Name]]"
---
```

**Structure**:
```markdown
# [Topic]

## Summary
[3-5 sentence overview of what this research covers]

## Key Details
[Bullet points of specific facts, specs, or cultural notes]
- Detail 1 with [source citation]
- Detail 2 with [source citation]

## Context
[Why this matters for the story]
[How this grounds the world]

## Story Applications
[How this can be used in scenes]
[Character connections]
[Atmospheric opportunities]

## Sources
1. [Full URL or citation]
   - Retrieved: YYYY-MM-DD
   - Reliability: high|medium|low
   - Notes: [why this source matters]

## Open Questions
[What still needs research]
[Contradictions found]

## Related Research
- [[Other Research File 1]]
- [[Other Research File 2]]
```

### Phase 7: Integration

**After creating research file**:

1. **Update relevant world bible entries**:
   - Add research-backed details to character/location/equipment files
   - Link to research file for citations
   - Note any contradictions with existing canon

2. **Cross-reference in vault**:
   - Link from world bible entries to research files
   - Link related research files to each other

3. **Validate links**:
   - REQUIRED SUB-SKILL: `validate-links`

### Phase 8: Report Completion

```
## Research Complete: [Topic]

**Saved to:** 03_Research/[Category]/[Filename].md

**Key findings:**
- [Fact 1] (source: [URL])
- [Fact 2] (source: [URL])

**Linked to world entries:**
- [[Entity 1]]
- [[Entity 2]]

**Confidence:** [High|Medium|Low]
**Gaps remaining:** [any]
```

## Research Priorities

### Cultural Authenticity (HIGHEST PRIORITY)
**What matters**: How people actually spoke, daily rituals, subcultural markers, class distinctions, generational divides

**Story impact**: Prevents "tourist" feeling. Grounds characters in lived experience.

### Technical Specifications (CRITICAL FOR ACTION)
**What matters**: Exact models, operational characteristics, reliability issues, maintenance requirements

**Story impact**: Action scenes feel real. Choices have weight. Costs are concrete.

### Historical Context (ESSENTIAL FOR ATMOSPHERE)
**What matters**: Political climate, economic conditions, recent events, cultural mood, media landscape

**Story impact**: Setting becomes a character. Background adds tension. Period feels specific.

### Geographic Grounding (IMPORTANT FOR SETTING)
**What matters**: Location characteristics, landmarks, routes, environmental details

**Story impact**: Movement makes sense. Characters inhabit real space. Atmosphere deepens.

## Quality Checklist

Before finalizing research file:

- [ ] Multiple sources consulted?
- [ ] Period-appropriate?
- [ ] User's lived experience considered?
- [ ] Sources documented with URLs/dates?
- [ ] Reliability assessment included?
- [ ] Contradictions noted (not hidden)?
- [ ] Story applications identified?
- [ ] Proper frontmatter complete?
- [ ] Filed in correct category?
- [ ] Cross-referenced with related files?
- [ ] World bible entries updated?
- [ ] Stereotypes avoided?
- [ ] Technical specs verified?

## Red Flags - STOP

If you catch yourself thinking:
- "This seems right..." → STOP. Cite a source.
- "I'll add sources later..." → STOP. Source now.
- "Everyone knows this..." → STOP. Verify anyway.
- "Close enough for fiction..." → STOP. Accuracy matters.

## When to Stop Researching

**You've done enough when**:
- Core question answered with verifiable details
- Multiple sources agree (or contradictions noted)
- Story applications clear
- User's lived experience incorporated
- Research file created and integrated

**Don't fall into**:
- Infinite rabbit holes
- Perfectionism paralysis
- Research as procrastination
- Over-documentation of tangential details

**Move forward**: Research enables writing. Don't let it replace writing.

## Cross-References

- **Called by:** writing-mode, thinking-mode, draft-support
- **After documenting:** REQUIRED SUB-SKILL: validate-links
- **For cultural topics:** Check `03_Research/Culture/` first
- **Research template:** `01_Meta/Templates/_research.md`

## Remember

- **Source everything** - No URL = no research note
- **Period-appropriate** - Check date relevance for project era
- **Save to vault** - Research in chat is lost
- **Link bidirectionally** - Research supports world entries
- **Research serves story** - Don't research for research's sake
- **Authenticity over exoticism** - Real details, not Hollywood versions
- **Lived experience > Google** - Always ask user first about cultural details
- **Contradictions are data** - Note them, don't resolve them artificially
- **Period specificity matters** - The exact era shapes everything
- **Archive for reuse** - Good research pays dividends across multiple scenes
