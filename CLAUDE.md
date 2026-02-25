# AI Brain Starter

Start with voice, build from there.
Created by Vejde Ab (Anna Hager). "AI as craft, not commodity."

## What This Repo Is

A voice-first starter kit for Claude Code. You begin by articulating
who you are (voice profile), then build agents, commands, and rules
that reference that foundation. The result: AI that sounds like you.

## The Flow

1. **Voice**: `voice-profile/` -- 100 questions, AI facilitator, template
2. **Activate**: `/activate-voice` -- wires your profile into standards, agents, review
3. **Standards**: `.claude/rules/` -- writing quality, agent loop (now voice-aware)
4. **Agents**: `.claude/agents/` -- specialized partners that read your voice
5. **Workflow**: `.claude/commands/` -- session rituals, scaffolding, review

## Structure

- `voice-profile/` -- THE foundation. Interview guide, facilitator prompt, template
- `docs/` -- architecture guides, patterns, brand DNA template
- `templates/` -- annotated templates for agents, commands, rules, sales frameworks
- `examples/` -- complete working examples (solo-consultant, dev-team)
- `.claude/` -- working agents, commands, rules, skills

## Agents

- **explorer** -- deep codebase exploration
- **reviewer** -- structured review with severity levels
- **strategist** -- business strategy coach with contrarian questions

## Commands

- `/scaffold` -- generate Claude Code structure in any project (voice-first)
- `/activate-voice` -- wire a completed voice profile into your entire setup
- `/start` -- session start ritual
- `/review` -- structured review workflow (includes voice check)
- `/create-agent` -- generate new agent from template
- `/create-command` -- generate new command from template

## Rules (always loaded)

- `agent-loop.md` -- GATHER > ACT > VERIFY > REPEAT
- `writing-standards.md` -- quality standards for text

## Principles

- Start with voice. Everything else references it.
- Progressive disclosure: CLAUDE.md under 150 lines, details in rules/agents/skills
- Never send an LLM to do a linter's job
- WHAT/WHY/HOW: what is the project, why these decisions, how to verify
- Commit often. Compact at 50%. Break tasks small.

## Credits

Inspired by shanraisshan/claude-code-best-practice and fltman/project-scaffolder.
Built on patterns proven in production at Vejde Ab.
