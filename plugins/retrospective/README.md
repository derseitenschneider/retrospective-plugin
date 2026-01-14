# Retrospective Plugin Marketplace

A Claude Code plugin marketplace containing self-learning tools.

## Installation

```bash
/plugin marketplace add your-username/retrospective-marketplace
/plugin install retrospective@retrospective-marketplace
```

Or for local development:

```bash
/plugin marketplace add /path/to/retrospective-marketplace
```

## Available Plugins

### retrospective

Analyzes coding sessions for user corrections and automatically updates project documentation (CLAUDE.md) to prevent future mistakes.

**Features:**
- Automatic trigger on session end (via Stop hook)
- Smart detection of correction patterns
- Concise, actionable documentation updates
- No bloat - only genuine learnings

See [plugins/retrospective/README.md](plugins/retrospective/README.md) for full documentation.

## License

MIT
