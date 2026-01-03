---
name: vault-health
description: Check entire vault health - uses validate-links and query-context skills
allowed-tools:
  - Read
  - Grep
  - Glob
---

# /vault-health

Comprehensive health check across the entire vault.

## Usage

```
/vault-health                      # Full vault check
/vault-health --quick              # Critical issues only
/vault-health --links              # Link integrity focus
```

## Process

### Step 1: Scan Vault Structure

Check all folders exist and are populated:
- `00_Inbox/`
- `01_Meta/`
- `02_World/`
- `03_Research/`
- `04_Media/`
- `05_Marketing/`
- `10_Projects/`

### Step 2: Validate All Links

**REQUIRED SUB-SKILL:** Invoke `validate-links` with full vault scope

Validate-links will check:
- All `[[wikilinks]]` resolve
- Bidirectional linking in world bible
- Orphaned files (no incoming links)

### Step 3: Check Inbox Health

Scan `00_Inbox/`:
- Count files
- Flag files >7 days old
- Check parking lot status

**If issues found:** Recommend `/inbox-processor` command

### Step 4: Query Stale Content

**REQUIRED SUB-SKILL:** Invoke `query-context` to find:
- Files not modified in >6 months
- World bible entries never referenced in scenes
- Research files never linked from world bible
- Scene seeds >3 months old

### Step 5: Check Structural Issues

- Files in wrong folders (e.g., scene in 01_Meta)
- Missing required frontmatter
- Empty folders

### Step 6: Report by Severity

```
## Vault Health Report

**Scan date:** [date]
**Files scanned:** [count]

---

### 🔴 Critical (Fix Now)

**Broken Links:** (from validate-links)
[list]

**Structural Errors:**
[list]

---

### 🟡 Warning (Review Soon)

**Inbox Issues:**
- 00_Inbox has [X] files >7 days old
  → Run /inbox-processor

**Missing Backlinks:** (from validate-links)
[list]

**Stale Content:** (from query-context)
[list]

---

### 🟢 Info (When Convenient)

**Orphaned Entries:** (from validate-links)
[list]

**Old Scene Seeds:**
[list]

---

### ✅ Healthy Areas

- Link integrity: [X]% (from validate-links)
- Frontmatter compliance: [X]%
- Folder structure: OK

---

### Summary

| Category | Status | Action |
|----------|--------|--------|
| Links | [status] | validate-links |
| Inbox | [status] | /inbox-processor |
| Stale content | [status] | /audit [folder] |

**Overall:** [Healthy|Needs Attention|Requires Cleanup]
```

### Step 7: Recommend Actions

```
### Priority Actions

1. **Links:** Use validate-links to fix [X] issues
2. **Inbox:** Run /inbox-processor
3. **Stale:** Run /audit on [folders]
4. **Missing entries:** Use world-bible for [items]
```

## Skill Invocations

| Check | Required Sub-Skill |
|-------|-------------------|
| Link integrity | `validate-links` |
| Stale content | `query-context` |
| Fix broken links | `validate-links` |
| Create missing | `world-bible` |

## Quick Mode (--quick)

Only check critical issues:
- Invoke validate-links for broken links only
- Check inbox age
- Skip stale content analysis

## Links Mode (--links)

Focus entirely on link integrity:
- Full validate-links analysis
- Detailed orphan report
- Backlink recommendations
