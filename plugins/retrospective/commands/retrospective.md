---
description: Analyze this session for corrections and update project documentation to prevent future mistakes
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(cat:*), Bash(head:*), Bash(tail:*)
---

# Retrospective Analysis

You are performing a retrospective analysis of this coding session. Your goal is to identify instances where you (the agent) made mistakes or had to be corrected by the user, then update the project's CLAUDE.md or other context files to prevent these mistakes in the future.

## Step 1: Analyze the Session Transcript

Review the current conversation for patterns where:
- The user explicitly corrected you ("No, that's wrong...", "I told you to...", "You forgot...")
- The user had to repeat themselves or clarify instructions
- You made assumptions that turned out to be incorrect
- You missed important project conventions or patterns
- You used deprecated APIs, wrong file paths, or incorrect syntax specific to this project
- You failed to follow established patterns in the codebase

Look for language indicating correction:
- "No", "Wrong", "Not like that", "Actually..."
- "I said...", "I meant...", "I already told you..."
- "Always", "Never", "Remember to..."
- Frustration markers: "again", "every time", "how many times"
- User undoing or reverting your changes

## Step 2: Categorize the Issues

For each identified issue, determine if it's:

1. **MISSING_INSTRUCTION**: The project docs don't mention this at all
2. **UNCLEAR_INSTRUCTION**: The docs mention it but ambiguously
3. **WRONG_INSTRUCTION**: The docs say something incorrect/outdated
4. **NOT_DOC_ISSUE**: One-off misunderstanding, user preference change mid-task, or edge case (skip these)

Only proceed with categories 1-3.

## Step 3: Read Current Documentation

Read the current project context files:
- CLAUDE.md in the project root
- Any .claude/ directory files
- Any CONVENTIONS.md, ARCHITECTURE.md, or similar files

Understand the current structure and style of these files.

## Step 4: Draft Updates

For each issue that IS a documentation problem, draft a minimal, precise update:

**Principles for updates:**
- Be CONCISE - one clear sentence is better than a paragraph
- Be SPECIFIC - "Use pnpm, not npm" not "Consider the package manager"
- Be ACTIONABLE - write instructions Claude can follow
- CONSOLIDATE - if similar to existing rules, merge rather than add
- PLACE CORRECTLY - put rules in relevant sections, create sections if needed
- NO BLOAT - if a rule is too edge-case or one-off, don't add it

**Format for rules:**
```
- [WHAT TO DO/NOT DO]: [Brief reason if not obvious]
```

Examples of GOOD additions:
- "Use `pnpm` for all package operations, not npm or yarn"
- "Run `pnpm test` before committing - tests must pass"
- "API routes are in `src/app/api/`, not `pages/api/`"
- "Always use relative imports within the same module"

Examples of BAD additions (too vague or bloated):
- "Remember to follow the project conventions"
- "Be careful with the API structure as it has specific requirements that should be followed"
- "The testing framework has certain expectations that need to be met"

## Step 5: Apply Updates

Edit the appropriate file(s) to add the new rules. If CLAUDE.md doesn't exist, create it with a clean structure.

**Suggested CLAUDE.md structure:**
```markdown
# Project Context

## Quick Reference
[Most important commands and paths]

## Coding Conventions
[Style, patterns, and practices]

## Common Pitfalls
[Things Claude tends to get wrong]

## Project-Specific Notes
[Unique aspects of this codebase]
```

## Step 6: Report Summary

After making updates, provide a brief summary:
- What corrections were identified
- What updates were made (if any)
- What was skipped and why

---

**Begin the retrospective analysis now. Be thorough but selective - only document learnings that will genuinely prevent future mistakes.**
