# Architecture Guide

## The Five Layers

Claude Code has five layers, each with different loading behavior:

| Layer | Loaded | Purpose |
|-------|--------|---------|
| **CLAUDE.md** | Always, at session start | Project identity, key patterns |
| **Rules** | Always, at session start | Guardrails that apply to everything |
| **Commands** | On demand, when user types /name | User-triggered workflows |
| **Agents** | On demand, via Task tool | Specialized subagents for delegation |
| **Skills** | Preloaded into agents at startup | Domain knowledge for agents |

## The Three-Tier Pattern: Command > Agent > Skills

From shanraisshan/claude-code-best-practice:

```
User types /command
    |
    v
Command (entry point, orchestrates workflow)
    |
    v
Agent (executes with preloaded skills)
    |-- Skill A (domain knowledge)
    |-- Skill B (domain knowledge)
    v
Result back to user
```

**Why this matters:** Commands handle user interaction. Agents handle execution. Skills provide knowledge. Clean separation of concerns.

## CLAUDE.md: The WHAT/WHY/HOW Framework

From fltman/project-scaffolder:

- **WHAT**: Project description, tech stack, key directories
- **WHY**: Architecture decisions, patterns, constraints
- **HOW**: Verification commands (test, build, lint)

Keep it under 150 lines. It loads every session.

## Progressive Disclosure

Not everything needs to be in CLAUDE.md:

| Always loaded | On demand |
|---------------|-----------|
| CLAUDE.md (< 150 lines) | Commands (user invokes) |
| Rules (.claude/rules/) | Skills (agent preloads) |
| | Agents (Task tool delegates) |

## Settings Hierarchy

Settings merge in this order (later overrides earlier):

1. `~/.claude/settings.json` (global defaults)
2. `.claude/settings.json` (project, team-shared, committed)
3. `.claude/settings.local.json` (personal, git-ignored)

## CLAUDE.md in Monorepos

From shanraisshan/claude-code-best-practice:

- **Ancestor loading (UP)**: All CLAUDE.md files from current dir to root load at startup
- **Descendant loading (DOWN)**: Subdirectory CLAUDE.md files load lazily when files in those dirs are accessed
- **Siblings never load**: Working in `frontend/` does not load `backend/CLAUDE.md`

This means you can have:
```
repo/
  CLAUDE.md              # Shared patterns (always loaded)
  frontend/
    CLAUDE.md            # Frontend patterns (loaded when frontend/ accessed)
  backend/
    CLAUDE.md            # Backend patterns (loaded when backend/ accessed)
```

## Frontmatter Quick Reference

### Agents (.claude/agents/*.md)

```yaml
---
name: agent-name           # Required
description: What it does   # Required. Include "Use PROACTIVELY" for auto-trigger.
tools: Read, Grep, Glob     # Optional. Limits available tools.
model: inherit              # Optional. sonnet, opus, haiku, or inherit.
---
```

### Commands (.claude/commands/*.md)

```yaml
---
name: command-name          # The /name users type
description: What it does   # Shown in command list
---
```

Use `$ARGUMENTS` in the body to access user input after the command name.

### Skills (.claude/skills/*/SKILL.md)

```yaml
---
name: skill-name            # Identifier
description: What it does   # Tells Claude when to use it
argument-hint: [input]      # Shows users expected input
---
```

Skills are injected into agent context at startup. They're static knowledge, not dynamically invoked.

## Memory

Agents can maintain persistent memory via MEMORY.md files.

| Scope | Location | Shared |
|-------|----------|--------|
| User | `~/.claude/` | No |
| Project | `.claude/` | Yes |
| Local | `.claude/*.local.*` | No |

The first 200 lines of MEMORY.md are injected at session start.
