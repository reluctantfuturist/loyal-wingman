---
name: feedback-processor
description: Process alpha reader feedback into actionable revision priorities. Use when user says "process this feedback", "what do my readers think", "triage beta comments", or has new reader notes to analyze
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
---

# Feedback Processor Skill

Process alpha reader feedback systematically: extract issues from various formats, prioritize by severity and frequency, track patterns across readers, and maintain structured feedback table for revision planning.

## Core Mission

**Pattern recognition over single-reader reactions**: Don't chase one-off suggestions. Wait for recurring issues across 3+ readers before flagging for revision.

**Brutal honesty filter**: Distinguish actionable critique from vague praise or random suggestions. Only concrete, specific feedback gets tracked.

**Status-driven workflow**: Every feedback item has a lifecycle. Track from intake → pattern analysis → triage → action → resolution.

## Skill Workflow

### 1. Intake New Feedback

**Triggered by**:
- User says "process feedback from [reader name]" or "new feedback in [file/folder]"
- User provides file path to feedback document or screenshot

**Input formats supported**:
- Markdown files with structured responses
- Screenshot images (WhatsApp, email, Discord, etc.)
- Plain text files
- Audio transcriptions (if provided as text)

**Process**:

1. **Read source material**:
   ```
   Reading feedback from: [file path]
   Format detected: [markdown/screenshot/text]
   Reader: [name]
   Date: [extracted or ask user]
   ```

2. **Extract feedback items**:
   - Parse structured responses (if using template format)
   - OCR/read screenshots for informal feedback
   - Identify distinct feedback points
   - Separate actionable critique from praise/noise

3. **Categorize each item** into:
   - **Character** (voice, motivation, consistency, development)
   - **Plot/Pacing** (hook, momentum, structure, clarity)
   - **World-building** (setting, systems, authenticity, info-dumping)
   - **Prose/Craft** (writing quality, dialogue, description)
   - **Technical** (accuracy, research, period details)
   - **Engagement** (interest level, drop-off points, confusion)
   - **Non-actionable** (vague praise, random suggestions)

4. **Extract priority signals**:
   - **Critical**: Reader confused, considered stopping, broke immersion
   - **High**: Multiple mentions, strong reaction, engagement issue
   - **Medium**: Single mention, clear concern, specific suggestion
   - **Low**: Minor observation, preference, nice-to-have
   - **Non-actionable**: Vague, random, or contradicts story intent

5. **Log to tracker**:
   - Add items to feedback table
   - Include reader name, date, category, priority
   - Set status: `new` for first occurrence
   - Cross-reference if similar issue exists from other readers

### 2. Pattern Analysis

**Run after collecting 2+ readers** (ideally 3-5 before flagging patterns):

1. **Scan tracker table** for duplicate/similar issues across readers
2. **Identify patterns**:
   - **Strong pattern**: 3+ readers mention same issue → Flag for action
   - **Emerging pattern**: 2 readers mention → Watch closely
   - **Single occurrence**: 1 reader → Track but don't act yet
   - **Contradictory feedback**: Readers disagree → Note conflict, user decides

3. **Update priority**:
   - Elevate priority if multiple readers cite same issue
   - Downgrade if only single occurrence after 5+ readers
   - Mark as `pattern-confirmed` when 3+ readers agree

4. **Flag for triage**:
   - Items with `pattern-confirmed` status → Ready for revision planning
   - Critical single-reader issues → Ask user if immediate action needed
   - Contradictory feedback → Present conflict to user for decision

### 3. Prioritization Framework

**Larry Correia's Unforgivable Sin Principle**: "The only unforgivable sin is being boring."

**Priority hierarchy**:

**P0 - CRITICAL (Fix immediately, even with single reader)**:
- Reader stopped reading / considered stopping
- Complete confusion about plot/character/world
- Immersion-breaking errors (anachronism, continuity break)
- Engagement failure (boring, couldn't care what happens)

**P1 - HIGH (Pattern confirmed, 3+ readers)**:
- Character feels flat/inconsistent (multiple readers)
- Pacing drags in specific section (multiple readers)
- Info-dump overwhelms (multiple readers)
- Key plot element unclear (multiple readers)

**P2 - MEDIUM (Pattern emerging, 2 readers OR single high-impact)**:
- Secondary character underdeveloped (2 readers)
- Specific scene feels slow (2 readers)
- World-building element confusing (2 readers)
- Single reader has strong specific concern with examples

**P3 - LOW (Single reader, minor issue)**:
- Preference differences
- Minor clarity improvements
- Nice-to-have additions
- Style preferences

**P4 - NON-ACTIONABLE (Track but don't act)**:
- Vague praise ("It's great!")
- Random plot suggestions unconnected to identified issues
- Contradicts core story intent
- Reader wants different genre/story

**Triage questions**:
1. **Does this make the story MORE INTERESTING?** (Correia test)
2. **Is this pattern or single occurrence?** (Wait for patterns)
3. **Does this serve the character/story?** (Story-first filter)
4. **Is this specific and actionable?** (Concrete vs. vague)

### 4. Tracker Table Structure

**Location**: `01_Meta/Feedback/Alpha_Feedback_Tracker.md`

**Format**: Markdown table with sortable columns

```markdown
## Feedback Tracker

| ID | Category | Issue | Reader(s) | Priority | Status | Chapter | Notes |
|---|---|---|---|---|---|---|---|
| F001 | Character | [Character] feels flat | [Reader] | P2-Medium | new | Ch1 | Wait for pattern |
| F002 | Plot | Hook requires context to land | [Reader] | P3-Low | new | Ch1 | Intentional mystery? |
```

**Column definitions**:
- **ID**: Unique feedback item identifier (F001, F002, etc.)
- **Category**: Character, Plot, World-building, Prose, Technical, Engagement, Non-actionable
- **Issue**: Concise description of feedback point
- **Reader(s)**: Name(s) of readers who mentioned this (comma-separated if multiple)
- **Priority**: P0-Critical, P1-High, P2-Medium, P3-Low, P4-NoAction
- **Status**:
  - `new` - Single occurrence, tracking
  - `watching` - 2 readers mentioned, emerging pattern
  - `pattern-confirmed` - 3+ readers, ready for action
  - `triaged` - User reviewed, decision made
  - `in-revision` - Actively being addressed
  - `resolved` - Fixed in manuscript
  - `dismissed` - Decided not to act
  - `praise` - Positive feedback, tracking strengths
- **Chapter**: Which chapter/scene this affects
- **Notes**: Additional context, quotes, cross-references

### 5. User Interaction Patterns

**After processing new feedback**:

```markdown
Processed feedback from [Reader Name] - [Date]

**New items added**: [count]
**Patterns emerging**: [count]
**Patterns confirmed**: [count]

**Critical flags** (immediate attention needed):
- [Issue description] - [Priority] - [Reason]

**Emerging patterns** (2 readers, watch closely):
- [Issue description] - Readers: [names]

**Action needed**:
- Review pattern-confirmed items: [count]
- Triage critical flags: [count]

**Tracker updated**: `01_Meta/Feedback/Alpha_Feedback_Tracker.md`
```

**When presenting conflicts**:

```markdown
**CONFLICTING FEEDBACK DETECTED**

Issue: [Description]

Reader A ([name]): [Their position]
Reader B ([name]): [Their position]

**Question**: Which direction serves the story better?
- Option A: [Implication]
- Option B: [Implication]

This is a creative decision. What's your call?
```

### 6. Revision Planning Support

**When user says "ready to revise" or "triage feedback"**:

1. **Generate revision priorities** from pattern-confirmed items
2. **Group by scene/chapter**
3. **Suggest revision approach**

### 7. Strengths Tracking

**Don't only track problems** - track what works:

| What Worked | Reader(s) | Evidence | Chapter |
|---|---|---|---|
| Dynamic opening | [Readers] | "[quotes]" | Ch1 |
| Protagonist voice | [Readers] | "[quotes]" | Ch1 |

**Why track strengths**:
- Shows what NOT to change during revision
- Identifies story's natural strengths to lean into
- Morale boost (feedback is brutal, need to see wins)
- Patterns of success inform future chapters

## Red Flags: Non-Actionable Feedback

**Dismiss immediately** (but track as examples):

1. **Vague praise**: "It's good!" "I liked it!" → No actionable detail
2. **Random plot suggestions**: Unconnected to identified issues
3. **Genre confusion**: Wrong expectations for this book type
4. **Reader wants different story**: Story intent mismatch
5. **Contradicts multiple readers**: Outlier preference
6. **Theoretical concerns**: Genre conventions vs. actual engagement

## Remember

**Pattern recognition > single reactions**: One reader's confusion doesn't mean the text is unclear. Three readers' confusion means it is.

**Specific > vague**: "Page 8 felt slow" is actionable. "Too much description" is not.

**Engagement trumps convention**: If readers are engaged and want more, genre conventions can be bent.

**Track everything, act selectively**: Better to over-capture and filter later than miss a pattern.

**User decides, skill informs**: Present data and patterns, but creative decisions belong to the writer.

**Strengths matter**: Track what works so you don't accidentally fix it.
