# Voice Capsule Integration Design

**Date**: 2026-01-03
**Status**: Implemented
**GitHub Issue**: #1

## Overview

Create a new `voice-checker` atomic skill that checks dialogue and internal narration against character voice capsules for ALL speaking characters in a scene. Integrate with prose-editor as a sub-skill.

## Problem

Currently, prose-editor checks for AI patterns and generic voice drift, but doesn't systematically verify prose against character-specific voice definitions. Voice information exists in character files and Style Guides, but isn't actively used during prose editing.

## Solution

New atomic skill `voice-checker` that:
1. Identifies all characters with dialogue in a scene
2. Loads voice capsules for each character
3. Checks POV character's internal narration + dialogue
4. Checks all other characters' dialogue
5. Returns structured report by severity

Prose-editor invokes voice-checker as a sub-skill in Phase 3.

---

## Voice Capsule Structure

Voice capsules live in character files at `02_World/Characters/[Name].md` within a `## Voice` section:

```markdown
## Voice

### Dialogue
- **Style**: [core speech pattern]
- **Markers**: [signature phrases, verbal tics]
- **Vocabulary**: [characteristic word choices, jargon, register]
- **Code-switching**: [context variations by relationship/formality]
- **Never**: [off-limits patterns]

### Internal
- **Style**: [thinking pattern]
- **Markers**: [recurring internal phrases]
- **Never**: [off-limits internal voice]

### Leitmotifs
- [thematic phrases that define character]

### Stress Responses
- [how voice changes under pressure]
```

### Field Definitions

| Field | Purpose | Example |
|-------|---------|---------|
| **Style** | Core pattern for this voice channel | "Terse; emotion as logic puzzle" |
| **Markers** | Concrete phrases/patterns to look for | "The math doesn't lie", economics metaphors |
| **Vocabulary** | Word choices reflecting background | Technical precision, chess references |
| **Code-switching** | Context-dependent register shifts | "Formal with elders, profane with Gagik" |
| **Never** | Explicit constraints (violations are Critical) | "Exposition dumps", "empty reassurances" |
| **Leitmotifs** | Recurring thematic phrases | "The wheel keeps turning" |
| **Stress Responses** | Voice changes under pressure | "Shorter sentences, verb stacking" |

### Design Rationale

- **Character file as source of truth**: Scales with cast size, self-contained per character
- **Structured fields**: Enable LLM to check specific aspects systematically
- **"Never" fields**: Provide clear constraints for Critical-level feedback
- **Separate Internal/Dialogue**: Different rules for POV narration vs speech

---

## Prose-Editor Integration

### Phase 1: Load Project Standards (Enhanced)

Add after existing Style Guide loading:

```markdown
**Load POV voice capsule:**
1. Read `pov_character` from scene frontmatter
2. If set: Load `02_World/Characters/[pov_character].md`
3. Extract `## Voice` section
4. If missing: Warn user, continue with Style Guide only
```

**Failure handling:**
- No `pov_character` in frontmatter → Warn, skip voice-specific checks
- Character file not found → Warn, skip voice-specific checks
- No `## Voice` section in file → Warn, skip voice-specific checks

### Phase 3: Voice Consistency Check (Enhanced)

Replace current voice checking with capsule-aware version:

```markdown
### Phase 3: Voice Consistency Check

**Using loaded voice capsule, check:**

**Internal narration (POV character):**
- Does thinking style match `Internal.Style`?
- Are `Internal.Markers` present where appropriate?
- Any violations of `Internal.Never`? → CRITICAL

**Dialogue (POV character's speech):**
- Does speech match `Dialogue.Style`?
- Are `Dialogue.Markers` used authentically (not forced)?
- Does vocabulary align with `Dialogue.Vocabulary`?
- Is code-switching appropriate for context/relationship?
- Any violations of `Dialogue.Never`? → CRITICAL

**Stress scenes:**
- If high-tension: Do `Stress Responses` patterns appear?

**Leitmotifs:**
- Are signature phrases used in earned moments?
- Are they overused (appearing too frequently)?
```

### Phase 4/5: Feedback Format (Enhanced)

Voice issues reported with capsule references:

```markdown
**VOICE: [Category] - [Issue Type]**
"[exact quote from text]"
↳ Violates: [Capsule.Field] = "[constraint]"
↳ [Explanation of why this breaks character voice]
↳ Fix: [Specific suggestion aligned with character]
```

**Severity mapping:**
| Severity | Trigger |
|----------|---------|
| CRITICAL | Any "Never" field violation |
| HIGH | Style mismatch, wrong register, code-switching error |
| MEDIUM | Missed opportunities, marker overuse |
| LOW | Minor authenticity notes |

---

## Example: Alisa Chernova Voice Capsule

```markdown
## Voice

### Dialogue
- **Style**: Terse; emotion as logic puzzle
- **Markers**: "The math doesn't lie", economics metaphors, chess references
- **Vocabulary**: Technical precision (calibers, models), clinical descriptions
- **Code-switching**: Formal Russian with elders, profane with Gagik, careful with civilians
- **Never**: Exposition dumps, empty reassurances, promises she can't keep

### Internal
- **Style**: Analytical, darkly wry
- **Markers**: Cost-benefit framing, clinical observation of horror, dissociation as survival
- **Never**: Self-pity paragraphs, grand declarations of destiny

### Leitmotifs
- "Control, always control."
- "The wheel keeps turning."

### Stress Responses
- Siberian profanity (father's influence)
- Shorter sentences, verb stacking
- Sarcasm before engagement, silence during
```

---

## Files Modified

| File | Changes |
|------|---------|
| `skills/voice-checker/SKILL.md` | **NEW**: Atomic skill for checking all characters against voice capsules |
| `skills/prose-editor/SKILL.md` | Invoke voice-checker as sub-skill in Phase 3 |
| `skills/world-bible/SKILL.md` | Updated Voice section template for character creation |
| `docs/guides/voice-capsules.md` | **NEW**: Writer-facing documentation |

---

## Writer Documentation

Create `docs/voice-capsules.md` covering:

1. What voice capsules are and why they matter
2. Voice section structure with field explanations
3. Examples of good voice capsules
4. How prose-editor uses them
5. Tips for writing effective "Never" constraints

---

## Project-Specific Recommendations

For projects adopting this feature:

### Character Files
- Add `## Voice` section to POV characters
- Structure per template above
- Consolidate from existing speech/voice documentation

### Scene Frontmatter
- Add `pov_character` field to all scenes:
  ```yaml
  pov_character: Character Name
  ```

### Style Guide
- Update to reference character files for voice details
- Keep summary tables for quick reference

### Templates
- Update `_character.md` template to include Voice section

---

## Out of Scope

- Checking non-POV character dialogue (future enhancement)
- Automated voice capsule generation from existing prose
- Voice drift tracking across multiple scenes

---

## Implementation Order

1. ✅ Create voice-checker atomic skill
2. ✅ Update prose-editor to invoke voice-checker as sub-skill
3. ✅ Update world-bible skill with expanded Voice section template
4. ✅ Create writer documentation (`docs/guides/voice-capsules.md`)
5. ✅ Close GitHub issue #1
