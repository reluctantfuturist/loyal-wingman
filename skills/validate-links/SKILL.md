---
name: validate-links
description: Check bidirectional link integrity across world bible. Use when user asks "check my links", "find broken references", "are there orphaned entries", or after creating/updating world bible entries
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

# Validate Links

## The Iron Law

```
LINKS MUST BE BIDIRECTIONAL. If A links to B, B must reference A.
```

## When to Use

- After creating new entity (called by world-bible)
- After major vault reorganization
- When checking vault health
- When user asks about link integrity

## The Process

### Phase 1: Identify Scope

Determine what to validate:
- **Single file:** Check all links in/out of one file
- **Folder:** Check all files in a folder
- **Full vault:** Check entire `02_World/` structure

### Phase 2: Extract Links

For each file in scope:

**Outgoing links:**
- All `[[wikilinks]]` in content
- All links in frontmatter (related_characters, etc.)

**Incoming links:**
- All files that link TO this file
- Search vault for `[[Filename]]`

### Phase 3: Check Link Resolution

For each outgoing link:
- Does target file exist?
- Is filename spelled correctly?
- Is path correct?

**Mark as:**
- ✓ Valid (resolves to file)
- ✗ Broken (no target file)
- ⚠ Possible typo (similar file exists)

### Phase 4: Check Bidirectionality

For each relationship:
- If A links to B, does B reference A?
- Reference can be wikilink OR text mention in appropriate section

**Mark as:**
- ✓ Bidirectional
- ⚠ One-way (needs backlink)

### Phase 5: Identify Orphans

Find files with:
- No incoming links (nothing references them)
- No outgoing links (reference nothing)

**Orphan types:**
- **Isolated:** No links in either direction
- **Dead-end:** Has incoming but no outgoing
- **Unreferenced:** Has outgoing but no incoming

### Phase 6: Report Findings

```
## Link Validation: [Scope]

### Broken Links
- [File]: [[Missing Target]] ✗

### Missing Backlinks
- [File A] links to [File B]
  But [File B] doesn't reference [File A]
  → Add to [section] in [File B]

### Orphaned Files
- [File]: No incoming links (unreferenced)

### Summary
- Files checked: X
- Valid links: Y
- Broken links: Z
- Missing backlinks: N
- Orphaned files: M
```

### Phase 7: Fix Issues (with approval)

For each issue, offer:
- **Broken link:** Delete link or create target file?
- **Missing backlink:** Add backlink to [section]?
- **Orphan:** Delete or find appropriate link?

**WAIT for user approval before making changes.**

## Red Flags - STOP

If you catch yourself thinking:
- "This link is probably fine..." → STOP. Verify it resolves.
- "The backlink isn't important..." → STOP. Bidirectional is the rule.
- "I'll fix these later..." → STOP. Fix now or flag clearly.

## Cross-References

- **Called by:** world-bible (Phase 6)
- **Used by:** vault-health command
- **For creating missing targets:** world-bible

## Remember

- **Bidirectional is required** - One-way links break navigation
- **Orphans are suspicious** - Why isn't it referenced?
- **Verify, don't assume** - Actually check file exists
- **Report clearly** - User needs to see the issues
