---
name: audit
description: Deep audit of specific file or folder - uses query-context and validate-links skills
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

# /audit

Analyze a specific file or folder for staleness, broken links, and cleanup opportunities.

## Usage

```
/audit 01_Meta/Templates/
/audit 02_World/Characters/[Character Name].md
/audit 10_Projects/[ProjectName]/
/audit --recent                    # Audit recently modified files
```

## Process - File Audit

### Step 1: Read File

- Full content
- Frontmatter fields
- Last modified date
- Word count

### Step 2: Validate Links

**REQUIRED SUB-SKILL:** Invoke `validate-links` for this file

Validate-links will check:
- All outgoing `[[wikilinks]]` resolve
- Incoming links from other files
- Bidirectional linking compliance

### Step 3: Query Usage Context

**REQUIRED SUB-SKILL:** Invoke `query-context` to find:
- Which projects/scenes reference this file
- Related entries in world bible
- Research backing (if applicable)

### Step 4: Report

```
## Audit: [Filename]

**Type:** [Character|Location|Equipment|etc.]
**Location:** [full path]
**Last modified:** [date] ([age])
**Word count:** [count]

### Frontmatter
- status: [value]
- [other fields]

### Link Analysis (from validate-links)
**Outgoing Links ([count]):**
- [[Link 1]] ✓
- [[Link 2]] ✓
- [[Missing Link]] ✗ BROKEN

**Incoming Links ([count]):**
- [File 1]
- [File 2]

**Bidirectional Status:** [OK|Issues found]

### Usage Context (from query-context)
- **Appears in projects:** [list]
- **Related world entries:** [list]
- **Research backing:** [list]

### Assessment
**Value:** [Essential|Useful|Redundant|Obsolete]
**Recommendation:** [Keep|Update|Archive|Delete]
**Reason:** [explanation]

### Suggested Actions
- [ ] Fix broken links (validate-links)
- [ ] Update stale content
- [ ] Add missing backlinks
```

## Process - Folder Audit

### Step 1: List Contents

- All files with ages
- Subdirectory structure

### Step 2: Validate All Links

**REQUIRED SUB-SKILL:** Invoke `validate-links` for folder scope

### Step 3: Query Context for Each File

**REQUIRED SUB-SKILL:** Invoke `query-context` to assess usage

### Step 4: Report

```
## Audit: [Folder Path]

**Files:** [count]
**Subdirectories:** [count]
**Oldest file:** [name] ([age])
**Newest file:** [name] ([age])

### Link Health (from validate-links)
- Valid links: [count]
- Broken links: [count]
- Missing backlinks: [count]

### File Assessment
| File | Age | Usage | Status |
|------|-----|-------|--------|
| [name] | 3mo | Active in [Project] | Keep |
| [name] | 8mo | Orphan | Review |

### Potential Redundancy
- [file1] vs [file2]: Similar names, check for duplicate content

### Recommendations
1. **Fix:** [broken links] - use validate-links
2. **Delete:** [files] - obsolete
3. **Consolidate:** [files] - redundant
4. **Create:** [missing entries] - use world-bible
```

## Skill Invocations

| Step | Required Sub-Skill |
|------|-------------------|
| Link analysis | `validate-links` |
| Usage context | `query-context` |
| Create missing | `world-bible` (if user approves) |

## Actions (After Approval)

For approved actions:
1. Fix broken links via validate-links
2. Create missing entries via world-bible
3. Delete/consolidate as approved

Report changes made.
