---
name: project-status
description: Show progress against target for active project - word counts, chapter status, blockers
allowed-tools:
  - Read
  - Grep
  - Glob
---

# /project-status

Display progress metrics for active writing project.

## Usage

```
/project-status                    # Default project (first found)
/project-status [ProjectName]      # Specific project
/project-status --all              # All projects
/project-status --seeds            # Include scene seeds count
```

## Process

### Step 1: Identify Project

Scan `10_Projects/` for project folders containing `Scenes/` subdirectory.

If no project specified, use first project found or ask user to specify.

### Step 2: Gather Metrics

For each chapter/scene file:

**From frontmatter:**
- `status`: draft | review | final
- `word_count`: if present
- `timeline_date`: scene date

**Calculated:**
- Word count (if not in frontmatter)
- Last modified date

### Step 3: Display Progress

```
## [Project Name] - Progress

| Chapter | Words | Status | Last Modified |
|---------|-------|--------|---------------|
| Ch 1    | 4,325 | final  | Nov 17        |
| Ch 2    | 3,890 | final  | Dec 10        |
| Ch 3    | 1,245 | draft  | Jan 2         |

**Total:** 9,460 words
**Chapters:** 3 (2 final, 0 review, 1 draft)

### Timeline Coverage
- Earliest scene: [date]
- Latest scene: [date]

### Recent Activity
- [Most recent change description]

### Blockers
[Any TODO tags or blocking notes from frontmatter]
```

### Step 4: Optional Additions

**With --seeds flag:**
```
### Scene Seeds
- [count] seeds in 10_Projects/Scene_Seeds/
- [count] potentially for this project (based on tags/mentions)
```

**With --all flag:**
Show summary table for all projects:
```
| Project | Chapters | Words | Status |
|---------|----------|-------|--------|
| Project_A | 3 | 9,460 | Active |
| Project_B | 10 | 45,230 | Revision |
| Project_C | 0 | 0 | Planning |
```

**With --series flag:**
```
### Series Planning
Files in 10_Projects/Series_Planning/:
- [file list with summaries]
```

## Status Definitions

| Status | Meaning |
|--------|---------|
| draft | Initial writing, not reviewed |
| review | Ready for editorial pass |
| final | Approved, publication-ready |

## Target Tracking

If project has target word count defined:
```
**Target:** 80,000 words
**Progress:** 12% (9,460 / 80,000)
**Remaining:** ~70,540 words
```
