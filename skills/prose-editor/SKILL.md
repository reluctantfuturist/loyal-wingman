---
name: prose-editor
description: Use when polishing prose for voice consistency and de-AI-ification - reads project Style Guide for project-specific patterns
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

# Prose Editor

## The Iron Law

```
QUOTE BEFORE FIXING. Read project Style Guide for patterns. Show text, explain failure, propose fix.
```

## When to Use

- "polish this" / "edit chapter" / "de-AI-ify"
- "check voice" / "voice consistency"
- After completing a draft
- Before marking scene as final
- Called by writing-mode Phase 5

## The Process

### Phase 1: Load Project Standards

**Read these files first:**
1. `01_Meta/Style_Guide/Style Guide.md` - Core patterns and voice bible (if exists)
2. `01_Meta/Style_Guide/` - Any additional style documentation
3. Project-specific config in `CLAUDE.md` or `PROJECT_CONFIG.md`

**Extract from Style Guide:**
- Language and diction patterns
- Character voice profiles (especially POV character for this scene)
- Craft and continuity rules
- Genre-specific guidance
- Pitfalls and anti-patterns
- QA checklist items

### Phase 2: AI Pattern Detection

Scan for universal AI tells:

**Transition Bloat:**
- "Moreover," "Furthermore," "Additionally," "However,"
- "In conclusion," "It's worth noting that"
- "Interestingly," "Notably," "Importantly"

**AI Cliches:**
- "In today's..." / "Let's dive into..."
- "It's important to note" / "It's worth mentioning"
- Rhetorical questions with immediate answers
- Forced parallel structures

**Hedging:**
- "somewhat," "rather," "quite," "fairly"
- Vague quantifiers: "various," "numerous," "significant"
- "It could be argued that..."

**Corporate Speak:**
- "utilize" → use
- "leverage" → use
- "implement" → do/make
- "facilitate" → help

**Overpolish:**
- Every sentence same length/structure
- Grammatically perfect but rhythmically dead
- Missing rough edges that feel human

### Phase 3: Voice Consistency Check

Using patterns loaded from project Style Guide:

**Against Character Voice (if defined):**
- [ ] POV character voice markers present
- [ ] Character-specific patterns used appropriately
- [ ] Dialogue style matches character profile
- [ ] "Never Do" items avoided (if specified)

**Against Prose Style (project-specific):**
- [ ] Prose texture matches project guidelines
- [ ] Verb/adjective balance appropriate
- [ ] Sensory detail at expected level

**Against Craft Rules (if defined):**
- [ ] Opening hooks present
- [ ] Pacing appropriate
- [ ] Setting established effectively
- [ ] Genre conventions respected

**Against Anti-Patterns:**
- Check for patterns flagged in Style Guide
- Verify voice doesn't drift toward identified problems

### Phase 4: Generate Feedback

For each issue:

```
[SEVERITY]: [CATEGORY]
"[exact quote from text]"
Problem: [why this doesn't work - reference Style Guide if applicable]
Fix: [specific replacement text]
```

**Severity Levels:**
- **CRITICAL**: Voice drift, character breaks, AI tells
- **HIGH**: Generic prose, pattern repetition, Style Guide violations
- **MEDIUM**: Polish opportunities, rhythm issues
- **LOW**: Minor improvements

### Phase 5: Present Teaching Feedback

Group by severity:

```
## Prose Edit Feedback: [Scene Name]

### CRITICAL (must fix)
[issues with Style Guide references]

### HIGH (strongly recommend)
[issues]

### MEDIUM (worth fixing)
[issues]

### LOW (optional)
[issues]

### What's Working
- [strengths to preserve]

### QA Checklist (from project Style Guide)
- [ ] [Project-specific checklist items]

**Ready to apply these edits?**
```

**WAIT for user approval.**

### Phase 6: User Applies Edits

**The user applies edits, not you.** Your role is to:
1. Present clear, copy-paste-ready replacement text
2. Wait for user to make changes
3. When user signals done: re-read for flow (edits sometimes create new issues)
4. Report any new issues introduced by edits

**Only use Edit tool if user explicitly asks:** "make these changes for me" or "apply the edits"

## Red Flags - STOP

If you catch yourself thinking:
- "This is fine actually..." → Re-read. Something triggered the scan.
- "The author probably meant..." → Quote exact text. Don't interpret.
- "I'll just make small tweaks..." → Present feedback first. Always.
- "This needs complete rewrite..." → Focus on fixable issues.
- "I know the patterns..." → Read Style Guide. Every time.

## Cross-References

- **For full scene workflow:** Used by writing-mode
- **For style reference:** Read `01_Meta/Style_Guide/`
- **For character specifics:** Read `02_World/Characters/[POV].md`

## Remember

- **Read Style Guide first** - Don't rely on memory
- **Quote before fixing** - Never edit without showing problem
- **Teach, don't just fix** - User should understand WHY
- **User applies edits** - Suggest, don't apply (unless explicitly asked)
- **Preserve rough edges** - Overpolish kills voice
- **Reference sections** - Cite Style Guide in feedback when applicable
