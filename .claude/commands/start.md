---
name: start
description: Session start ritual. Establish context before working.
---

## Session Start

### 1. Context
- Which branch is active? Run `git branch --show-current`
- Any uncommitted changes? Run `git status`
- What was the last commit? Run `git log --oneline -3`

### 2. Plan
Ask: "What should we work on today?"

Based on the answer:
- **New project/feature**: enter plan mode
- **Continuation**: read relevant files, summarize where we left off
- **Quick task**: execute directly

### 3. Context Budget
Remind: "Full context window available. I'll run /compact at ~50%. Each task should be completable within half the context."

### 4. Commit Discipline
Commit immediately after each completed task. Don't batch.
