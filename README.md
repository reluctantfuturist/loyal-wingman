# Loyal Wingman

> "I think of AI as a loyal wingman—a powerful tool, but a terrible master."
> — [The Loyal Wingman](https://loyalwingman.org/the-loyal-wingman/)

A Claude Code plugin for fiction writing that embodies the Loyal Wingman philosophy: AI excels in supporting roles while the human writer remains the creative decision-maker.

## Philosophy

AI works best when it:
- **Handles tedious research** - Information gathering, fact-checking, sourcing
- **Serves as brainstorming partner** - Listening, synthesizing, unblocking
- **Provides tough feedback** - Honest editing, pattern detection, voice checking
- **Never replaces the writer** - Support, don't supplant

This plugin implements that philosophy through structured workflows that keep you in control while providing powerful assistance.

## Features

### Core Workflow Skills

- **writing-mode** - Focused prose production with outline → query → draft → polish phases
- **thinking-mode** - Expansive brainstorming and worldbuilding exploration

### Support Skills

- **outliner** - Create or review scene outlines (discovery mode to detailed beats)
- **query-context** - Comprehensive vault search before writing
- **draft-support** - Real-time assistance during drafting (without writing for you)
- **prose-editor** - AI pattern detection, voice consistency, teaching feedback
- **voice-checker** - Verify all characters' dialogue against voice capsules
- **plot-threads** - Track narrative threads, setups/payoffs, Chekhov's guns
- **research** - Find, validate, archive research with proper sourcing

### World Management Skills

- **world-bible** - Create and maintain world bible entries with proper linking
- **validate-links** - Check bidirectional link integrity

### Utility Skills

- **feedback-processor** - Process alpha reader feedback, track patterns

### Commands

| Command | Purpose |
|---------|---------|
| `/writing` | Enter focused writing mode |
| `/thinking` | Enter brainstorming mode |
| `/project-status` | View progress metrics |
| `/character-map` | Show character relationships |
| `/vault-health` | Check vault integrity |
| `/audit` | Deep audit of files/folders |
| `/inbox-processor` | Triage inbox contents |

## Installation

### From Marketplace

```bash
# Add the loyal-wingman marketplace
/plugin marketplace add reluctantfuturist/loyal-wingman

# Install the plugin
/plugin install loyal-wingman@loyal-wingman
```

### Local Development

```bash
# Clone the repository
git clone https://github.com/reluctantfuturist/loyal-wingman.git

# Use with Claude Code
claude --plugin-dir /path/to/loyal-wingman
```

## Expected Vault Structure

The plugin expects an Obsidian-style vault with this structure:

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

## Using with Obsidian

This plugin is designed to work with Obsidian-style markdown vaults. While it doesn't require Obsidian itself, the workflow assumes:

- **Wikilinks** - `[[Entity Name]]` style links for cross-references
- **Frontmatter** - YAML metadata at the top of files
- **Folder structure** - Organized directories for world bible, research, projects

### Required Templates

The plugin references templates in `01_Meta/Templates/` that you'll need to create for your project. Each template defines the structure for a type of world bible entry:

| Template | Purpose |
|----------|---------|
| `_character.md` | Character sheets with voice, relationships, arc |
| `_location.md` | Location entries with sensory details, history |
| `_equipment.md` | Equipment specs, story function, costs |
| `_faction.md` | Faction structure, goals, key members |
| `_event.md` | Timeline events with context, consequences |
| `_system.md` | Magic/tech systems with rules, costs, limits |
| `_theme.md` | Thematic elements with manifestations, questions |
| `_research.md` | Research notes with sources, reliability |

Templates should include frontmatter fields and section headers appropriate to your project. The skills will read these templates when creating new entries.

### Recommended Obsidian Plugins

While optional, these Obsidian plugins enhance the workflow:
- **Dataview** - Query frontmatter for project dashboards
- **Templater** - Advanced template insertion
- **Longform** - Multi-scene project management

## Project Configuration

For project-specific customization, create a `PROJECT_CONFIG.md` in your project root. See `PROJECT_CONFIG_TEMPLATE.md` for the full template.

Key sections:
- **Project Overview** - Genre, tone, setting, themes
- **Character Voice Profiles** - POV character voice definitions
- **Style Guide Summary** - Prose texture, anti-patterns
- **QA Checklist** - Project-specific quality checks
- **Research Priorities** - What to focus research on

## Core Workflow

### Writing Mode (`/writing`)

1. **Outline Phase** - Review existing outline or create one (discovery/compass/detailed)
2. **Query Phase** - Search vault for all relevant context
3. **Research Phase** - Fill gaps with external research
4. **Draft Phase** - User writes, assistant supports
5. **Polish Phase** - Teaching feedback, then approved edits

The key principle: **you write the draft**. The wingman answers questions, provides research, and catches issues—but never takes the keyboard from you.

### Thinking Mode (`/thinking`)

1. Check parking lot for captured ideas
2. Explore freely without restrictions
3. Invoke subskills for structured output
4. Validate links after creating entries

## The Wingman Principles in Practice

### Support, Don't Supplant

During drafting, the plugin answers questions and provides research. It does NOT write prose unless explicitly requested. Your voice, your story.

### Teaching Over Fixing

Prose feedback explains WHY something doesn't work, with quotes and examples. You learn, you decide, you improve.

### Research-Backed Fiction

All technical, cultural, and historical details should have sources. The wingman does the tedious lookups so you can focus on story.

### Never Assume

Gaps in the vault are flagged for your decision, not filled with AI creativity. The wingman asks, you decide.

## Skills Reference

| Skill | Invoked By | Purpose |
|-------|-----------|---------|
| writing-mode | `/writing` | Focused prose production |
| thinking-mode | `/thinking` | Brainstorming, worldbuilding |
| outliner | writing-mode, Manual | Scene outline creation/review |
| query-context | writing-mode | Comprehensive vault search |
| draft-support | writing-mode | Real-time drafting assistance |
| prose-editor | writing-mode | Polish and de-AI-ify prose |
| voice-checker | prose-editor, Manual | Check dialogue against voice capsules |
| plot-threads | query-context, writing-mode, Manual | Track narrative threads |
| research | writing-mode, thinking-mode | Research with proper sourcing |
| world-bible | thinking-mode | Create/maintain world bible entries |
| validate-links | world-bible | Check link integrity |
| feedback-processor | Manual | Process reader feedback |

## Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT License - see LICENSE file for details.

## Changelog

### 0.2.0

- New skill: plot-threads for narrative thread tracking
- Integration with query-context and writing-mode workflows

### 0.1.0

- 10 skills for fiction writing workflow
- 7 commands for project management
- Project configuration template
- Comprehensive documentation
- Loyal Wingman philosophy throughout
