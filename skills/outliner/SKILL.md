---
name: outliner
description: Create or review scene outlines with flexible depth. Use when user asks "outline this scene", "what are the beats", "help me plan this chapter", or needs structure ranging from discovery mode to detailed beat sheets
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

# Outliner

## The Iron Law

```
SERVE THE WRITER'S PROCESS. Some need detailed beats, others need a compass heading. Offer structure without imposing it.
```

## When to Use

- Before drafting a new scene (called by writing-mode Phase 2)
- "outline this scene" / "plan chapter X" / "what are the beats"
- Reviewing existing outline before continuing work
- Converting brainstorming into structured scene plan

## The Process

### Phase 1: Check Existing Outline

Search for outline in:
1. Project index file (e.g., `10_Projects/[Project]/[Project] Index.md`)
2. Scene file frontmatter
3. Scene seeds (`10_Projects/Scene_Seeds/`)

**If outline exists:**
1. Read and present the planned beats
2. Identify "discovery writing zones" (areas marked flexible)
3. Note key questions to address during drafting
4. Ask: "Proceed with this outline, or adjust first?"

**If no outline exists:** Proceed to Phase 2.

### Phase 2: Determine Outline Depth

Present options based on writer preference:

**Option A: Discovery Mode** (minimal structure)
- Define only: Scene goal + how it ends
- Trust the process to find the path
- Best for: Pantsers, exploratory scenes, character-driven moments

**Option B: Compass Outline** (light structure)
- Scene goal (what POV character wants)
- Obstacle (what blocks them)
- Disaster/outcome (how scene ends, value shift)
- Emotional core (thematic purpose)
- Best for: Plantsers, scenes with clear purpose but flexible execution

**Option C: Beat Sheet** (detailed structure)
- Numbered beats with word estimates
- Key dialogue moments or revelations
- Specific emotional turns
- Discovery zones explicitly marked
- Post-scene state defined
- Best for: Complex scenes, action sequences, revelation scenes

### Phase 3: Gather Scene Elements

Based on chosen depth, gather:

**Core Elements (all outlines):**

| Element | Question | Example |
|---------|----------|---------|
| **Scene Goal** | What does the POV character want? | "Alisa wants to confront Gagik about the security breach" |
| **Obstacle** | What blocks them? | "Gagik's calm deflection, her own conflicted feelings" |
| **Value Shift** | How does the scene end vs. start? | "Trust → Damaged trust (negative)" |
| **Emotional Core** | What is this scene ABOUT? | "Love warped by trauma is still love" |

**Extended Elements (compass + beat sheet):**

| Element | Question |
|---------|----------|
| **Opening State** | Where is the character physically/emotionally? |
| **Closing State** | Where do they end up? |
| **Must-Have Moments** | What absolutely needs to happen? |
| **Foreshadowing** | What seeds future events? |

**Beat Sheet Elements (detailed only):**

| Element | Question |
|---------|----------|
| **Numbered Beats** | What are the 4-8 major moments? |
| **Word Estimates** | Roughly how long is each beat? |
| **Discovery Zones** | Which beats are flexible/exploratory? |
| **Key Questions** | What needs to be figured out during drafting? |
| **Revelation Calibration** | What does character learn vs. reader infer? |

### Phase 4: Structure Using Craft Frameworks

Apply relevant framework based on scene type:

**For most scenes - Swain's Scene & Sequel:**
- Scene: Goal → Conflict → Disaster
- Sequel: Reaction → Dilemma → Decision

**For turning points - Story Grid Five Commandments:**
- Inciting Incident → Turning Point → Crisis → Climax → Resolution

**For action sequences:**
- Clear spatial orientation
- Cause → Effect chains
- Physical/emotional costs visible

**For dialogue scenes:**
- Subtext layer (what's NOT said)
- Power dynamics shifting
- Each character has an agenda

### Phase 5: Document Outline

**Save location options:**
1. **Project Index** - For complex scenes, keeps all planning together
2. **Scene Frontmatter** - For simpler scenes, keeps outline with draft
3. **Scene Seeds** - If not ready to draft yet

**Outline Format:**

```markdown
## [Scene Title] Outline

**Scene Goal:** [What POV character wants]
**Obstacle:** [What blocks them]
**Value Shift:** [Start state] → [End state]
**Emotional Core:** [What this scene is ABOUT]

### Beats
1. **[Beat Name]** (~Xw): [Description]
2. **[Beat Name]** (~Xw): [Description]
   - *Discovery zone: [what's flexible]*
3. **[Beat Name]** (~Xw): [Description]

### Key Questions
- [Question to address during drafting]

### Post-Scene State
- Physical: [condition]
- Mental: [state]
- Relationships: [status changes]

### Discovery Zones
- [Area left intentionally flexible]
```

### Phase 6: Confirm and Handoff

If called by writing-mode:
- Summarize outline for user confirmation
- Note discovery zones
- Hand back to writing-mode for query-context phase

If standalone:
- Save outline to appropriate location
- Offer: "Ready to start drafting? Use `/writing` to begin."

## Scene Type Templates

### Action Scene Outline
```
Goal: Survive/defeat [threat]
Obstacle: [Physical danger, limited resources]
Beats: Setup → Engagement → Complication → Resolution
Must track: Ammunition, injuries, spatial clarity
Value shift: Safety → Danger (or reverse)
```

### Confrontation Scene Outline
```
Goal: Get [truth/commitment/acknowledgment]
Obstacle: [Other character's resistance/secrets]
Beats: Approach → Initial exchange → Escalation → Revelation → Aftermath
Must track: Power dynamics, what's revealed vs. concealed
Value shift: Trust/ignorance → [new state]
```

### Quiet/Reflection Scene Outline
```
Goal: Process [recent events]
Obstacle: [Internal resistance, intrusive thoughts]
Beats: Routine anchor → Memory/reflection → Realization → Decision
Must track: Sensory grounding, character voice
Value shift: Confusion → Clarity (or reverse)
```

## Red Flags - STOP

If you catch yourself thinking:
- "Let me plan every detail..." → STOP. Preserve discovery zones.
- "This doesn't need an outline..." → STOP. Even discovery mode defines goal + ending.
- "I'll figure out the ending later..." → STOP. Scene needs destination.
- "Let me start drafting..." → STOP. That's writing-mode, not outliner.

## Cross-References

- **Called by:** writing-mode (Phase 2)
- **Standalone use:** "outline chapter X"
- **For brainstorming:** thinking-mode (then invoke outliner to structure)
- **For context:** query-context (after outline, before drafting)
- **Project index:** `10_Projects/[Project]/[Project] Index.md`

## Remember

- **Serve the writer's process** - Not everyone needs detailed beats
- **Scene goal is non-negotiable** - Even discovery mode needs a destination
- **Discovery zones are sacred** - Mark what's flexible, respect it
- **Value shift matters** - Scene should change something
- **Save the outline** - Don't lose planning work
