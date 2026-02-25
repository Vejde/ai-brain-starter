---
name: scaffold
description: Generate a voice-first Claude Code setup in any project directory
---

Generate a complete Claude Code setup for a project. Voice first.

## Arguments

$ARGUMENTS should contain: `<project-path> [profile]`

- `<project-path>`: absolute or relative path to the target project
- `[profile]`: "minimal" (default), "solo", or "team"

## Profiles

### minimal (default)
For getting started quickly:
- CLAUDE.md (generated from interview)
- .claude/settings.json
- .claude/rules/agent-loop.md
- .claude/commands/start.md

### solo
For solo consultants, freelancers, solopreneurs:
- Everything in minimal, plus:
- admin/VOICE-PROFILE.md (voice profile template)
- admin/BRAND-DNA.md (brand DNA template)
- .claude/agents/reviewer.md
- .claude/agents/strategist.md
- .claude/commands/review.md
- .claude/commands/create-agent.md
- .claude/commands/create-command.md
- .claude/rules/writing-standards.md

### team
For development teams:
- Everything in minimal, plus:
- .claude/agents/explorer.md
- .claude/agents/reviewer.md (code-focused)
- .claude/commands/review.md
- .claude/commands/create-agent.md
- .claude/commands/create-command.md
- .claude/rules/writing-standards.md

## Process

### Step 1: Voice First

Ask: "Do you have a voice profile? A document that captures how you communicate?"

**If yes:** Ask for the path. Reference it in CLAUDE.md and all agents.

**If no (solo profile):** Explain the voice profile process:
"The most impactful thing you can do is build a voice profile. It takes 2-4 hours but transforms everything Claude produces for you. I'll set up the template. You can do the interview after scaffolding."

Copy `voice-profile/voice-profile-template.md` to `admin/VOICE-PROFILE.md`.
Copy `voice-profile/ai-facilitator-prompt.md` to `admin/AI-FACILITATOR-PROMPT.md`.

**If no (team profile):** Skip voice profile. Teams typically define voice in style guides.

### Step 2: Verify Target

Check that the project path exists. Warn if not a git repo.
Check if .claude/ already exists. If so, ask: merge or skip existing files?

### Step 3: Project Interview

Ask these questions to generate a project-specific CLAUDE.md:

1. **What is this project?** (one sentence)
2. **What tech stack?** (languages, frameworks, key dependencies)
3. **How do you verify it works?** (test command, build command, lint command)
4. **What are the key directories?** (src/, docs/, tests/, etc.)
5. **Any patterns Claude should follow?** (naming conventions, architecture patterns)
6. **What should Claude NEVER do?** (destructive operations, specific files to avoid)

### Step 4: Generate Structure

Based on profile and interview answers:

1. Create directories: `.claude/agents/`, `.claude/commands/`, `.claude/rules/`
2. If voice profile exists, add to CLAUDE.md:
   ```
   ## Voice
   Read `admin/VOICE-PROFILE.md` before writing any content.
   Match the voice, don't caricature it.
   ```
3. Generate CLAUDE.md using the WHAT/WHY/HOW framework:
   - **WHAT**: Project description, tech stack, key directories
   - **WHY**: Architecture decisions, patterns to follow, voice reference
   - **HOW**: Verification commands (test, build, lint)
4. Copy appropriate files from this starter kit's templates/ directory
5. Generate .claude/settings.json with permission pre-approvals for test/build/lint commands
6. Ensure all agents that write content include: "Read admin/VOICE-PROFILE.md before writing."

### Step 5: Replace Placeholders

In each generated file, replace:
- `{{PROJECT_NAME}}` with project name
- `{{PROJECT_DESCRIPTION}}` with description from interview
- `{{TEST_COMMAND}}` with test command
- `{{BUILD_COMMAND}}` with build command
- `{{LINT_COMMAND}}` with lint command

### Step 6: Report

List all generated files.
Show the generated CLAUDE.md for approval.
Print next steps:

```
Setup complete. Next steps:

1. BUILD YOUR VOICE PROFILE (most impactful step)
   Copy admin/AI-FACILITATOR-PROMPT.md into a Claude conversation.
   Let it interview you. Takes 2-4 hours. Transforms everything after.

2. Review and customize CLAUDE.md
3. Run `claude` in your project directory
4. Type /start to test the session ritual
5. Use /create-agent to add custom agents
```

## Important

- NEVER overwrite existing files without asking
- Always show what will be created before creating it
- Generated CLAUDE.md should be under 100 lines
- Voice profile is always the first recommendation, never an afterthought
