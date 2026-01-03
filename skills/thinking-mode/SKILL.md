---
name: thinking-mode
description: Use for expansive brainstorming, worldbuilding, and exploration - invokes atomic subskills for structured work, processes parking lot
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - TodoWrite
---

# Thinking Mode

## The Iron Law

```
DEVELOP IDEAS FULLY. Invoke specialized subskills for structured work.
```

## When to Use

- "thinking mode" / "let's brainstorm" / "explore [topic]"
- "what if..." questions about story direction
- Worldbuilding and character development
- Processing parking lot items
- Series planning and arc development

## The Process

### Phase 1: Check Parking Lot

On entry, check parking lot file (default: `00_Inbox/Parking_Lot.md`, check PROJECT_CONFIG.md for custom path)

If items exist:
1. Present: "Parking lot has [X] items from WRITING MODE:"
   - List items with dates
2. Ask: "Process these first, or explore something else?"

### Phase 2: Exploration

**No restrictions on topics.** Explore freely:
- Themes, arcs, future developments
- Character backstory and development
- "What if" scenarios
- Connecting disparate ideas

### Phase 3: Invoke Subskills for Structured Work

When exploration produces structured output, invoke appropriate subskill:

| Output Type | Required Sub-Skill |
|-------------|-------------------|
| New character | `world-bible` |
| New location | `world-bible` |
| New equipment | `world-bible` |
| New faction | `world-bible` |
| New timeline event | `world-bible` |
| New system | `world-bible` |
| New theme | `world-bible` |
| Research need | `research` |
| Link validation | `validate-links` |

**Scene seeds:** Save directly to `10_Projects/Scene_Seeds/`
**Series planning:** Save directly to `10_Projects/Series_Planning/`

### Phase 4: Process Parking Lot Items

For each parking lot item:

1. **Develop** the idea (brainstorm, explore implications)
2. **Decide destination:**
   - New canon entry → REQUIRED SUB-SKILL: `world-bible`
   - Research needed → REQUIRED SUB-SKILL: `research`
   - Scene seed → Save to `10_Projects/Scene_Seeds/`
   - Not worth pursuing → Delete from parking lot
3. **Remove** processed item from parking lot file

### Phase 5: Validate Links

After creating multiple entries:

**REQUIRED SUB-SKILL:** Invoke `validate-links`

Ensure all new entries are properly cross-referenced.

### Phase 6: Transition Reminder

After significant exploration (30+ minutes or major topic complete):

"Ready to convert insights to prose? Switch to WRITING MODE."

## Subskill Invocation Summary

| Action | Required Sub-Skill |
|--------|-------------------|
| Create world bible entry | `world-bible` |
| External research | `research` |
| Verify link integrity | `validate-links` |

## Red Flags - STOP

If you catch yourself thinking:
- "I should be writing instead..." → No guilt. Thinking feeds writing.
- "This is too tangential..." → Tangents are the point.
- "Let me just quickly draft this scene..." → STOP. That's writing-mode.
- "I'll create this entry without the skill..." → STOP. Use world-bible.
- "Links can wait..." → STOP. Use validate-links.

## Cross-References

- **For new canon entries:** REQUIRED SUB-SKILL: world-bible
- **For research:** REQUIRED SUB-SKILL: research
- **For link validation:** REQUIRED SUB-SKILL: validate-links
- **For focused prose:** Switch to writing-mode

## Remember

- **No guilt** - Thinking time is productive
- **Invoke subskills** - Structured work deserves structured tools
- **Process parking lot** - Clear it before it grows
- **Validate links** - After creating entries
- **Know when to switch** - Insights become prose in writing-mode
