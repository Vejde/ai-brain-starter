# Agent Loop

All work follows this pattern:

```
GATHER CONTEXT > TAKE ACTION > VERIFY > REPEAT
```

1. **Gather**: Read relevant files, search codebase, understand the problem fully BEFORE acting
2. **Act**: Execute changes in small, verifiable chunks
3. **Verify**: Run `npm run build && npm test` after changes. Check that the result matches intent.
4. **Repeat**: If not done, gather more context and continue

## Context Management

- Run `/compact` at ~50% context usage
- Use subagents for research tasks (isolates context)
- Break work into chunks completable within half the context budget
- Commit immediately after completing each task

## Thinking Levels

Use these trigger phrases for complex work:
- "think" -- simple planning, basic decisions
- "think hard" -- feature implementation, complex queries
- "think harder" -- architecture decisions, schema changes
- "ultrathink" -- security-sensitive work, migration design
