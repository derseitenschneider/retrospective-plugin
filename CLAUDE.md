# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Claude Code Plugin Marketplace** containing the `retrospective` plugin. The plugin enables Claude instances to automatically learn from user corrections by analyzing sessions and updating project documentation (CLAUDE.md files).

## Architecture

```
.claude-plugin/marketplace.json     # Marketplace metadata and plugin registry
plugins/retrospective/
├── .claude-plugin/plugin.json      # Plugin manifest
├── commands/retrospective.md       # Slash command definition with analysis workflow
├── hooks/hooks.json                # Stop hook for automatic triggering
└── README.md                       # Plugin documentation
```

### Key Components

- **marketplace.json**: Defines the marketplace with plugin registry pointing to `./plugins/retrospective`
- **plugin.json**: Plugin manifest declaring name, version, and commands path
- **retrospective.md**: 6-step analysis workflow triggered by `/retrospective` command
- **hooks.json**: "Stop" hook that uses prompt-based decision logic to auto-trigger retrospectives

### How It Works

1. The Stop hook evaluates each session when Claude finishes
2. If corrections are detected (user frustration, repeated instructions, Claude apologies), the hook blocks with `{"decision": "block"}` and triggers `/retrospective`
3. The retrospective command analyzes the conversation, categorizes issues (MISSING/UNCLEAR/WRONG/NOT_DOC_ISSUE), and updates CLAUDE.md

## Development Notes

- **No build system**: This is a declarative plugin using only JSON and Markdown
- **No tests**: Pure configuration, no executable code
- **No dependencies**: Self-contained plugin structure

## Claude Code Plugin Structure

Plugins follow this required structure:
- `.claude-plugin/plugin.json` - Manifest with name, version, commands path
- `commands/*.md` - Slash command definitions with frontmatter (description, allowed-tools)
- `hooks/hooks.json` - Hook definitions (optional)

Marketplaces require:
- `.claude-plugin/marketplace.json` - Registry with plugins array pointing to plugin sources
