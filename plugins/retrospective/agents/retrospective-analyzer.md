---
description: Analyzes session transcripts for user corrections and updates CLAUDE.md to prevent future mistakes
allowed-tools: Read, Write, Edit, Glob, Grep
---

# Retrospective Analyzer

Analyze the session transcript for user corrections and update project documentation.

## Step 1: Find Correction Patterns

Scan the conversation for:
- Explicit corrections: "no, that's wrong", "I told you", "you forgot", "actually..."
- Frustration markers: "again", "every time", "how many times"
- User reverting changes or undoing work
- Claude apologizing for mistakes
- Repeated clarifications

## Step 2: Categorize Each Issue

For each correction found, classify as:
- **MISSING_INSTRUCTION**: Docs don't mention this at all
- **UNCLEAR_INSTRUCTION**: Docs mention it but ambiguously
- **WRONG_INSTRUCTION**: Docs are outdated or incorrect
- **NOT_DOC_ISSUE**: Skip - one-off mistake, preference change, edge case

Only proceed with the first three categories.

## Step 3: Read Current CLAUDE.md

Check for existing documentation:
```
Glob: **/CLAUDE.md
```

Understand the current structure and existing rules to avoid duplication.

## Step 4: Update Documentation

For each documentable issue, add a minimal, actionable rule:
- One sentence per rule
- Be specific: "Use pnpm, not npm" not "Follow conventions"
- Consolidate with existing rules if similar
- Place in the appropriate section

If CLAUDE.md doesn't exist, create it with this structure:
```markdown
# Project Context

## Quick Reference
[Commands and paths]

## Coding Conventions
[Style and patterns]

## Common Pitfalls
[Things to avoid]
```

## Step 5: Report Summary

Output a brief summary:
- Issues found (with category)
- Rules added or updated
- Issues skipped and why

Be selective - only document learnings that prevent real future mistakes.
