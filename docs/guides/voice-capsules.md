# Voice Capsules: Keeping Characters Consistent

Voice capsules are structured definitions of how a character thinks and speaks. The prose-editor skill uses them to check your prose for voice consistency, catching drift before it becomes a problem.

## Why Voice Capsules Matter

Every character has a distinct voice—how they think, speak, react under pressure. When you're deep in a draft, it's easy to slip:
- Your protagonist suddenly sounds like your antagonist
- Internal narration becomes generic
- A terse character delivers an exposition monologue

Voice capsules give the prose-editor concrete patterns to check against, catching these slips with specific feedback tied to your character definitions.

## Where Voice Capsules Live

Voice capsules belong in character files:

```
02_World/Characters/[Character Name].md
```

Within the character file, add a `## Voice` section.

## Voice Capsule Structure

```markdown
## Voice

### Dialogue
- **Style**: [How they speak - rhythm, complexity, emotional expression]
- **Markers**: [Signature phrases, verbal tics, recurring patterns]
- **Vocabulary**: [Word choices reflecting background, education, profession]
- **Code-switching**: [How speech changes by context or relationship]
- **Never**: [What this character would never say]

### Internal
- **Style**: [How they think - analytical, emotional, fragmented]
- **Markers**: [Recurring internal phrases or framings]
- **Never**: [Thought patterns that would break character]

### Leitmotifs
- [Thematic phrases that define the character]

### Stress Responses
- [How voice changes under pressure]
```

## Field Guide

### Style
The core pattern for how this character communicates. Be specific.

**Weak**: "Speaks casually"
**Strong**: "Terse; treats emotion as logic puzzle; rarely uses more words than necessary"

### Markers
Concrete phrases or patterns the prose-editor can look for. These aren't required in every scene—they're touchstones that reinforce character when used well.

**Examples**:
- "The math doesn't lie" (analytical character)
- Economics metaphors (character with finance background)
- Military jargon without explanation (veteran character)

### Vocabulary
Word choices that reflect who this character is. Helps catch moments where vocabulary doesn't match background.

**Examples**:
- Technical precision: calibers, model numbers, proper terminology
- Working-class speech: no fifty-cent words
- Academic: subordinate clauses, hedged statements

### Code-switching
How the character adjusts speech for different contexts. Essential for characters who move between social worlds.

**Examples**:
- "Formal Russian with elders, profane with close friends"
- "Corporate jargon at work, relaxed slang at home"
- "Careful and measured with strangers, rapid-fire with family"

### Never
The most important field for catching problems. These are explicit constraints—if the prose-editor finds a violation, it's flagged as Critical.

**Be specific about what breaks character**:
- "Exposition dumps" — character reveals too much
- "Empty reassurances" — character wouldn't offer false comfort
- "Self-pity paragraphs" — internal voice shouldn't wallow
- "Promises she can't keep" — character is too honest for this

### Leitmotifs
Recurring thematic phrases that define the character across scenes. Use sparingly but consistently.

**Examples**:
- "The wheel keeps turning." (fatalistic acceptance)
- "Control, always control." (character's core need)

### Stress Responses
How voice changes when the character is under pressure. Helps the prose-editor check action and tension scenes.

**Examples**:
- "Shorter sentences, verb stacking"
- "Falls back on childhood dialect"
- "Goes silent—actions replace words"
- "Dark humor increases"

## Example: Complete Voice Capsule

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

## How Voice-Checker Works

The prose-editor invokes the voice-checker skill to verify character voices:

1. **Identifies all speakers**: Scans the scene for the POV character and all characters with dialogue
2. **Loads capsules**: Reads voice capsules for each identified character from `02_World/Characters/`
3. **Checks POV internal narration**: Compares POV character's thoughts against Internal fields
4. **Checks ALL dialogue**: Verifies every character's speech against their respective capsules
5. **Reports violations**: Quotes exact text, references which field was violated, suggests fixes

Characters without voice capsules are skipped with a warning, not failed.

### Feedback Example

```
**VOICE: Dialogue violates "Never" pattern**
"I promise everything will be okay," Alisa said softly.
↳ Violates: Dialogue.Never = "Empty reassurances, promises she can't keep"
↳ Fix: She deflects or offers concrete action instead
```

## Scene Frontmatter

For voice capsules to work, scenes need a `pov_character` field:

```yaml
---
title: Scene Title
pov_character: Character Name
status: draft
---
```

The character name should match the filename (without `.md`) in `02_World/Characters/`.

## Tips for Effective Voice Capsules

**Start with "Never"**: The constraints are most useful for catching problems. What would absolutely break this character?

**Be concrete in Markers**: Vague markers like "speaks confidently" don't help. Specific phrases and patterns do.

**Update as you write**: Voice capsules evolve. When you discover something new about how a character speaks, add it.

**Less is more for Leitmotifs**: One or two signature phrases per character. If they're everywhere, they lose power.

**Test your capsule**: After writing it, read a scene with that character. Does the capsule capture what makes their voice distinct?

## When Voice Capsules Are Skipped

The prose-editor gracefully handles missing pieces:

- **No `pov_character` in frontmatter**: Warns you, skips voice-specific checks
- **Character file not found**: Warns you, skips voice-specific checks
- **No `## Voice` section**: Warns you, skips voice-specific checks

You'll still get AI pattern detection and other prose-editor checks—you just won't get character-specific voice feedback.

## Edge Cases

**Multiple POV switches:** If your scene shifts POV mid-scene, set `pov_character` to the primary POV. Internal narration checks will apply to that character; dialogue checks will apply to all speakers regardless of POV.

**Omniscient narration:** If no clear POV character exists, omit `pov_character`. Voice-checker will still verify all dialogue against capsules, but skip internal narration checks.

**Minor characters without capsules:** You don't need voice capsules for every character. Background characters with one or two lines can be skipped. Voice-checker will warn you but continue checking characters that do have capsules.

**Ensemble scenes:** In scenes with many speakers, voice-checker loads capsules for all identified characters. If this gets unwieldy, consider which characters truly need voice consistency enforcement.
