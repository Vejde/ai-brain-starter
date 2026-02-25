---
name: start
description: Developer session start. Check project state and establish what to work on.
---

## Session Start

### 1. Git Context
- Run `git branch --show-current` to show the active branch
- Run `git status` to check for uncommitted changes
- Run `git log --oneline -5` to show recent commits

### 2. Project Health
- Run `npm run build` to verify TypeScript compiles
- Run `npm test` to verify tests pass
- If either fails, report the failure and ask if fixing it should be the priority

### 3. Pending Work
- Check for any TODO comments: `grep -r "TODO\|FIXME\|HACK" api/ shared/ --include="*.ts" -n`
- If on a feature branch, summarize the diff against main: `git diff main...HEAD --stat`

### 4. Plan
Ask: "What should we work on today?"

Based on the answer:
- **New feature**: outline the implementation plan before writing code
- **Bug fix**: reproduce the issue first, then fix
- **Continuation**: read relevant files and summarize where we left off
- **Quick task**: execute directly

### 5. Reminders
- Commit after each completed task
- Run `npm run build && npm test` before every commit
- I'll run `/compact` at ~50% context usage
