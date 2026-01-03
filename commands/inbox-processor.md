---
name: inbox-processor
description: Triage 00_Inbox contents - categorize, move, or delete stale files
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

# /inbox-processor

Systematically triage all files in `00_Inbox/`, moving to proper locations or deleting stale content.

## Process

### Step 1: Scan Inbox

List all files in `00_Inbox/` with:
- File name
- Age (days since modified)
- First 100 characters of content

Flag files >7 days old as STALE.

### Step 2: Categorize Each File

For each file, determine category:

| Category | Destination | Action |
|----------|-------------|--------|
| Scene seed | `10_Projects/Scene_Seeds/` | Move |
| Research note | `03_Research/[category]/` | Move |
| World bible content | `02_World/[category]/` | Flag for world-bible |
| Series planning | `10_Projects/Series_Planning/` | Move |
| Parking lot | Already in place | Process items |
| Stale/obsolete | N/A | Delete |

### Step 3: Present Recommendations

```
## Inbox Triage: [count] files

### Move to Scene_Seeds
- [file]: [reason] → `10_Projects/Scene_Seeds/[name].md`

### Move to Research
- [file]: [reason] → `03_Research/[category]/[name].md`

### Create World Bible Entry
- [file]: [reason] → Use world-bible skill

### Delete (Stale)
- [file]: [age] days old, [reason for deletion]

### Parking Lot Items
[If Parking_Lot.md exists and has content]
- [item 1]: [recommendation]
- [item 2]: [recommendation]

**Approve these actions?**
```

### Step 4: Execute (After Approval)

For each approved action:
1. Move files to destinations
2. Delete approved deletions
3. For world bible content: invoke `world-bible` skill
4. Clear processed parking lot items

### Step 5: Report Final State

```
## Inbox Processed

**Moved:** [count] files
**Deleted:** [count] files
**Created:** [count] world bible entries

**Current inbox state:** [count] files remaining
**Oldest file:** [age] days

Target: <5 files, all <7 days old
Status: [HEALTHY|NEEDS ATTENTION]
```

## Parking Lot Special Handling

If `00_Inbox/Parking_Lot.md` exists:

1. Read all items
2. For each item, recommend:
   - Develop into scene seed
   - Create world bible entry
   - Research needed
   - Delete (not worth pursuing)
3. Present for user decision
4. Process according to decision
5. Remove processed items from file

## Target State

After processing:
- `00_Inbox/` should have <5 files
- No files older than 7 days
- `Parking_Lot.md` cleared or with only recent items
