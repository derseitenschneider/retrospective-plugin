# Retrospective Plugin for Claude Code

A self-learning plugin that analyzes coding sessions for user corrections and automatically updates project documentation (CLAUDE.md) to prevent future mistakes.

## What It Does

After each session where Claude made mistakes that required user correction, this plugin:

1. **Analyzes the conversation** for correction patterns
2. **Categorizes issues** as missing/unclear/wrong documentation vs one-off mistakes
3. **Compares with existing docs** to avoid duplicates
4. **Updates CLAUDE.md** with minimal, actionable rules
5. **Keeps documentation clean** - no bloat, only genuine learnings

## Installation

### Option 1: Local Installation (for development)

```bash
# Clone or copy this plugin to your project
cp -r retrospective-plugin /path/to/your/project/.claude/plugins/

# Or add to your user plugins
cp -r retrospective-plugin ~/.claude/plugins/
```

### Option 2: Via Marketplace (if published)

```
/plugin marketplace add derseitenschneider/retrospective-plugin
/plugin install retrospective@your-marketplace
```

### Option 3: Direct from Git

Add to your `.claude/settings.json`:

```json
{
  "enabledPlugins": [
    {
      "source": {
        "source": "github",
        "repo": "derseitenschneider/retrospective-plugin"
      }
    }
  ]
}
```

## Components

### `/retrospective` Slash Command

Manually trigger a retrospective analysis at any time:

```
/retrospective
```

This will:

- Scan the current session for corrections
- Identify documentation gaps
- Update CLAUDE.md with new rules
- Report what was learned

### Stop Hook (Automatic Trigger)

The plugin automatically evaluates each session when Claude stops. If significant corrections were detected, it triggers `/retrospective` automatically.

**Smart filtering prevents false triggers:**

- Ignores very short sessions
- Ignores user preference changes (not Claude errors)
- Ignores one-off edge cases
- Prevents infinite loops (won't trigger during retrospective)

## How It Identifies Corrections

The plugin looks for:

**Explicit corrections:**

- "No, that's wrong..."
- "I told you to..."
- "You forgot..."
- "Actually, you should..."

**Frustration markers:**

- "again"
- "every time"
- "how many times"
- User undoing Claude's changes

**Implicit corrections:**

- User repeating instructions
- User reverting files
- Claude apologizing for mistakes

## Documentation Style

The plugin maintains clean, actionable documentation:

**Good rules (will be added):**

```markdown
- Use `pnpm` for all package operations, not npm
- API routes are in `src/app/api/`, not `pages/api/`
- Always run tests before committing
```

**Bad rules (will be skipped):**

```markdown
- Remember to follow project conventions
- Be careful with the codebase structure
```

## CLAUDE.md Structure

If CLAUDE.md doesn't exist, it creates one with:

```markdown
# Project Context

## Quick Reference

[Commands and paths]

## Coding Conventions

[Patterns and practices]

## Common Pitfalls

[Things Claude gets wrong]

## Project-Specific Notes

[Unique aspects]
```

## Configuration

### Disable Automatic Triggering

If you only want manual retrospectives, remove the hook in your settings:

```json
{
  "hooks": {
    "Stop": []
  }
}
```

### Customize the Slash Command

Copy `commands/retrospective.md` to your project's `.claude/commands/` and modify as needed.

## Best Practices

1. **Review the updates** - Check what was added to CLAUDE.md after a retrospective
2. **Consolidate periodically** - Manually merge similar rules
3. **Remove obsolete rules** - Delete rules for deprecated patterns
4. **Use sections** - Keep rules organized by category

## Troubleshooting

**Retrospective runs too often:**

- The hook uses intelligent filtering, but you can disable it and run manually

**Not detecting corrections:**

- Try running `/retrospective` manually after a problematic session
- The detection focuses on explicit correction language

**CLAUDE.md getting bloated:**

- The plugin tries to be selective, but review periodically
- Remove rules that are too specific or no longer relevant

## Philosophy

This plugin embodies the idea that:

- Documentation should be a living record of lessons learned
- The best rules come from real mistakes, not speculation
- Concise, actionable instructions beat verbose guidelines
- Self-improvement should be automatic but controlled

## License

MIT
