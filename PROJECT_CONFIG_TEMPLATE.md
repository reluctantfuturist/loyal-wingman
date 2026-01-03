# Project Configuration Template

Copy this file to your writing project as `PROJECT_CONFIG.md` or integrate into your `CLAUDE.md` to customize the loyal-wingman plugin for your specific project.

---

## Project Overview

**Project Name:** [Your Project Name]
**Genre:** [e.g., Urban Fantasy, Sci-Fi Noir, Historical Fiction]
**Tone:** [e.g., Grimdark with earned hope, Light adventure, Literary drama]
**Setting Period:** [e.g., 2005-2010, Victorian Era, Near Future 2050]
**Setting Location:** [e.g., Moscow, London, Mars Colony]

**Logline:** [One sentence describing your project]

**Thematic Pillars:**
- [Theme 1]
- [Theme 2]
- [Theme 3]

## Vault Structure

The loyal-wingman plugin expects this standard structure. Customize paths if your project differs:

**Parking Lot Path:** `00_Inbox/Parking_Lot.md` (customize if different)

```
YourProject/
├── 00_Inbox/           # Temporary capture, parking lot
├── 01_Meta/            # Operational docs
│   ├── Style_Guide/    # Voice, craft, project-specific patterns
│   ├── Templates/      # File templates for entities
│   └── Feedback/       # Alpha reader tracking
├── 02_World/           # World bible (canonical truth)
│   ├── Characters/
│   ├── Equipment/
│   ├── Factions/
│   ├── Locations/
│   ├── Systems/
│   ├── Themes/
│   └── Timeline_Events/
├── 03_Research/        # Real-world grounding (sourced)
│   ├── Culture/
│   ├── Equipment/
│   ├── Geography/
│   ├── History/
│   └── Technology/
├── 04_Media/           # Portraits, mood boards
├── 05_Marketing/       # Blurbs, query letters, synopses
├── 10_Projects/        # Active writing
│   ├── [Book Name]/
│   │   └── Scenes/
│   ├── Scene_Seeds/
│   └── Series_Planning/
└── .claude/            # Claude Code configuration
```

## Character Voice Profiles

Define voice profiles for POV characters. The prose-editor skill will check against these.

### [Protagonist Name]

**Internal Voice:**
- [Describe internal monologue style: analytical, emotional, detached, etc.]

**Dialogue Style:**
- [Describe speech patterns: terse, flowery, formal, etc.]

**Recurring Patterns:**
- "[Catchphrase or recurring thought 1]"
- "[Catchphrase or recurring thought 2]"

**Never:**
- [Things this character would never say/think/do]

### [Secondary POV Character]

[Repeat format above]

## Style Guide Summary

Key style rules for the prose-editor skill to enforce:

### Prose Texture
- [e.g., Sparse and muscular / Lush and descriptive]
- [e.g., Verbs over adjectives / Rich sensory detail]
- [e.g., Short sentences for tension / Long for reflection]

### Cultural/Setting Elements
- [e.g., Max 2 foreign words per page]
- [e.g., Period-appropriate technology only]
- [e.g., Specific naming conventions]

### Genre Conventions
- [e.g., Magic always has costs]
- [e.g., Violence is clinical, aftermath visceral]
- [e.g., Hope must be earned, not gifted]

### Anti-Patterns (Things to Avoid)
- [e.g., Info-dumps disguised as dialogue]
- [e.g., Melodramatic declarations]
- [e.g., Convenient coincidences]

## QA Checklist

Project-specific checklist for the prose-editor skill:

- [ ] Sensory anchor in opening lines?
- [ ] Stakes clear within first page?
- [ ] [Project-specific check 1]
- [ ] [Project-specific check 2]
- [ ] [Project-specific check 3]
- [ ] Character voices distinct?
- [ ] Setting feels alive?
- [ ] Prose matches project style?

## Research Priorities

What the research skill should focus on for this project:

### High Priority
- [e.g., Russian cultural authenticity 2005-2010]
- [e.g., Firearms specifications]
- [e.g., Moscow geography]

### Medium Priority
- [e.g., Political context]
- [e.g., Technology limitations]

### Research Red Flags
- [e.g., Avoid tourist-y stereotypes]
- [e.g., Verify period-appropriate tech]

## World Bible Conventions

### Naming Conventions
- [e.g., Russian names with patronymics]
- [e.g., Location names in local language]

### Special Systems
- [e.g., Magic system name and core rules]
- [e.g., Technology constraints]

### Key Factions
- [List major factions for reference]

## Feedback Processing Notes

Reader-specific considerations for feedback-processor skill:

- [e.g., Russian readers may have different genre expectations]
- [e.g., Technical readers will scrutinize equipment details]
- [e.g., Genre readers expect X conventions]

## Active Projects

Current project default for /project-status:

**Default Project:** `10_Projects/[BookName]/`

**Other Active Projects:**
- `10_Projects/[Project2]/` - [Status]
- `10_Projects/[Project3]/` - [Status]

---

## Usage

1. Copy this template to your project root as `PROJECT_CONFIG.md`
2. Fill in all sections relevant to your project
3. Reference from your `CLAUDE.md` if desired
4. Skills will read this file for project-specific guidance

The loyal-wingman plugin skills will check for this file and use it to customize their behavior for your specific project.
