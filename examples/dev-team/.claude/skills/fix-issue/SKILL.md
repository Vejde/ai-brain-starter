---
name: fix-issue
description: Fix a GitHub issue end-to-end. Reads the issue, finds relevant code, implements the fix, writes tests, and creates a commit.
argument-hint: [issue-number]
---

Fix the GitHub issue specified in $ARGUMENTS.

## Steps

### 1. Understand the Issue
- Fetch the issue details: `gh issue view $ARGUMENTS`
- Read the title, description, labels, and any linked issues
- Identify whether this is a bug fix, feature request, or improvement

### 2. Find Relevant Code
- Delegate to the `explorer` agent to locate the code involved
- For bugs: find the failing code path and understand the expected behavior
- For features: find where the new code should live based on existing patterns

### 3. Create a Branch
- Branch from main: `git checkout -b fix/$ARGUMENTS-short-description`

### 4. Implement the Fix
- Follow existing patterns in the codebase
- Use typed errors from `shared/errors.ts`
- Add Zod validation for any new input
- Keep changes minimal and focused on the issue

### 5. Write Tests
- Unit test for the service logic
- Integration test for the endpoint (if applicable)
- Test the specific scenario described in the issue
- Test edge cases around the fix

### 6. Verify
- Run `npm run build` -- must compile cleanly
- Run `npm test` -- all tests must pass
- Run `npm run lint` -- no lint violations

### 7. Commit
- Commit with message: `fix(scope): description (closes #$ARGUMENTS)`
- Include what was wrong and what the fix does
