---
name: voice-checker
description: Check dialogue and narration against character voice capsules. Use when user asks "check voice", "voice consistency", or when prose-editor needs voice verification for a scene
allowed-tools:
  - Read
  - Grep
  - Glob
---

# Voice Checker

Check prose against character voice capsules for all speaking characters in a scene.

## The Iron Law

```
EVERY CHARACTER HAS A VOICE. Load capsules for all speakers. Check POV internal + all dialogue.
```

## When to Use

- Called by prose-editor (Phase 3)
- Called by writing-mode for voice spot-check
- "check voice" / "voice consistency" / "does this sound like [character]?"
- Before marking scene as final
- When dialogue feels off

## The Process

### Phase 1: Identify Characters in Scene

1. Read scene file completely
2. Identify POV character from frontmatter (`pov_character` field) or narration style
3. Scan for all characters with dialogue (look for dialogue tags, speech patterns)
4. Build character list: `[POV, Speaker1, Speaker2, ...]`

**If no `pov_character` in frontmatter:**
- Infer from third-person limited narration
- Or ask user: "Who is the POV character for this scene?"

### Phase 2: Load Voice Capsules

For each character identified:

1. Search `02_World/Characters/` for matching file
2. Load the `## Voice` section if present
3. Track which characters have capsules vs missing

**Report loading status:**
```
Voice capsules loaded:
✓ [Character A] - full capsule
✓ [Character B] - full capsule
⚠ [Character C] - no Voice section (will skip)
✗ [Character D] - no character file found
```

**Continue with available capsules.** Missing capsules = skipped, not failed.

### Phase 3: Check POV Character

**Internal Narration** (only POV character has this):
- Does thinking style match `Internal.Style`?
- Are `Internal.Markers` present naturally? (not forced)
- Any violations of `Internal.Never`? → CRITICAL

**POV Character Dialogue:**
- Apply same dialogue checks as other characters (see Phase 4)

### Phase 4: Check All Dialogue

For each character with a loaded voice capsule:

**Style Check:**
- Does speech pattern match `Dialogue.Style`?
- Is vocabulary consistent with `Dialogue.Vocabulary`?

**Marker Check:**
- Are `Dialogue.Markers` used authentically?
- Not required in every scene, but should feel natural when present

**Code-Switching Check:**
- Who is the character speaking TO?
- Does register match `Dialogue.Code-switching` for that relationship?

**Never Check:**
- Any violations of `Dialogue.Never`? → CRITICAL
- These are explicit author constraints — violations always flagged

**Stress Response Check (if applicable):**
- Is this a high-tension scene?
- Do `Stress Responses` patterns appear appropriately?

### Phase 5: Check Leitmotifs

For POV character:
- Are `Leitmotifs` used in earned moments?
- Overuse check: same leitmotif multiple times in scene = flag as MEDIUM

### Phase 6: Generate Report

```markdown
## Voice Check: [Scene Name]

### Characters Checked
- **[POV Character]** (POV) - internal + dialogue
- **[Character B]** - dialogue only
- **[Character C]** - skipped (no voice capsule)

### CRITICAL Issues

**[Character Name]: Dialogue violates "Never" pattern**
"[exact quote]"
↳ Violates: Dialogue.Never = "[constraint]"
↳ [Explanation]
↳ Fix: [Suggestion aligned with character voice]

### HIGH Issues

**[Character Name]: Code-switching mismatch**
"[exact quote]"
↳ Context: Speaking to [relationship]
↳ Expected: [per Code-switching field]
↳ Fix: [Adjust register]

### MEDIUM Issues

**[Character Name]: Leitmotif overused**
"[phrase]" appears 3 times in scene
↳ Consider: Use once for impact, vary phrasing otherwise

### What's Working
- [Character A]'s economics metaphors feel natural
- [Character B]'s terse responses match profile
- Stress responses authentic in combat scene

### Missing Voice Capsules
The following characters have dialogue but no voice capsule:
- [Character C] - consider adding to `02_World/Characters/`
- [Character D] - mentioned but no file exists
```

## Voice Capsule Structure

Expected structure in `02_World/Characters/[Name].md`:

```markdown
## Voice

### Dialogue
- **Style**: [core speech pattern]
- **Markers**: [signature phrases, verbal tics]
- **Vocabulary**: [characteristic word choices]
- **Code-switching**: [context variations by relationship]
- **Never**: [off-limits patterns]

### Internal
- **Style**: [thinking pattern]
- **Markers**: [recurring internal phrases]
- **Never**: [off-limits internal voice]

### Leitmotifs
- [thematic phrases]

### Stress Responses
- [voice changes under pressure]
```

## Severity Mapping

| Severity | Trigger |
|----------|---------|
| CRITICAL | Any `Never` field violation |
| HIGH | Style mismatch, wrong register, vocabulary break |
| MEDIUM | Missed opportunities, marker overuse, leitmotif repetition |
| LOW | Minor authenticity notes |

## Red Flags - STOP

If you catch yourself thinking:
- "This character doesn't have a capsule, I'll guess..." → STOP. Skip or ask user.
- "Close enough to the style..." → STOP. Quote and compare specifically.
- "The Never rule doesn't apply here..." → STOP. Never rules always apply.
- "I'll check just the main character..." → STOP. Check all speakers.

## Cross-References

- **Called by:** prose-editor, writing-mode
- **Voice capsule source:** `02_World/Characters/[Name].md` → `## Voice`
- **For creating capsules:** See world-bible skill
- **Documentation:** `docs/guides/voice-capsules.md`

## Remember

- **Check ALL speakers** - Not just POV character
- **Load before checking** - Report which capsules found/missing
- **Never = Critical** - These are explicit author constraints
- **Missing capsule = skip** - Don't guess, don't fail
- **Quote exactly** - Reference specific capsule fields
- **Context matters** - Code-switching depends on who's speaking to whom
