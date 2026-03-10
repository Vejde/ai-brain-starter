---
name: scaffold
description: Generate a voice-first Claude Code setup in any project directory
---

Generate a complete Claude Code setup for a project. Voice first.

## Arguments

$ARGUMENTS should contain: `<project-path> [profile]`

- `<project-path>`: absolute or relative path to the target project
- `[profile]`: "minimal" (default), "solo", or "team"

## File Mapping

All source paths are relative to THIS repo (ai-brain-starter).
All destination paths are relative to the TARGET project.

### minimal (default)

| Source | Destination | Action |
|--------|-------------|--------|
| templates/CLAUDE.md.template | CLAUDE.md | Generate from interview |
| .claude/rules/agent-loop.md | .claude/rules/agent-loop.md | Copy |
| .claude/commands/start.md | .claude/commands/start.md | Copy |
| — | .claude/settings.json | Generate from interview |

### solo (includes everything in minimal, plus:)

| Source | Destination | Action |
|--------|-------------|--------|
| voice-profile/voice-profile-template.md | admin/VOICE-PROFILE.md | Copy |
| voice-profile/ai-facilitator-prompt.md | admin/AI-FACILITATOR-PROMPT.md | Copy |
| docs/BRAND-DNA-TEMPLATE.md | admin/BRAND-DNA.md | Copy |
| .claude/agents/reviewer.md | .claude/agents/reviewer.md | Copy |
| .claude/agents/strategist.md | .claude/agents/strategist.md | Copy |
| .claude/commands/review.md | .claude/commands/review.md | Copy |
| .claude/commands/create-agent.md | .claude/commands/create-agent.md | Copy |
| .claude/commands/create-command.md | .claude/commands/create-command.md | Copy |
| .claude/rules/writing-standards.md | .claude/rules/writing-standards.md | Copy |

### team (includes everything in minimal, plus:)

| Source | Destination | Action |
|--------|-------------|--------|
| .claude/agents/explorer.md | .claude/agents/explorer.md | Copy |
| .claude/agents/reviewer.md | .claude/agents/reviewer.md | Copy |
| .claude/commands/review.md | .claude/commands/review.md | Copy |
| .claude/commands/create-agent.md | .claude/commands/create-agent.md | Copy |
| .claude/commands/create-command.md | .claude/commands/create-command.md | Copy |
| .claude/rules/writing-standards.md | .claude/rules/writing-standards.md | Copy |

## Process

### Step 1: Verify Target

Resolve the project path to an absolute path. If relative, resolve from the USER'S working directory (not this repo's root).

Example: if the user runs `/scaffold ~/my-project solo`, the target is `/Users/[username]/my-project`.
Example: if the user runs `/scaffold my-project solo`, the target is `[cwd]/my-project`.

If the path doesn't exist, ask: "Directory doesn't exist. Create it?"

Check if `.claude/` already exists in the target. If so, ask: merge or skip existing files?
Warn if the target is not a git repo.

### Step 2: Voice First (solo profile only)

Ask: "Do you have a voice profile? A document that captures how you communicate?"

**If yes:** Ask for the path. Reference it in CLAUDE.md and all agents.

**If no:** Explain:
"The most impactful thing you can do is build a voice profile. It takes 2-4 hours but transforms everything Claude produces for you. I'll set up the template. You can do the interview after scaffolding."

Then copy voice-profile files per the file mapping above.

**Team profile:** Skip voice profile. Teams typically define voice in style guides.

### Step 3: Project Interview

Ask these questions to generate CLAUDE.md:

1. **What is this project?** (one sentence)
2. **What tech stack?** (languages, frameworks, key dependencies)
3. **How do you verify it works?** (test command, build command, lint command)
4. **What are the key directories?** (src/, docs/, tests/, etc.)
5. **Any patterns Claude should follow?** (naming conventions, architecture patterns)
6. **What should Claude NEVER do?** (destructive operations, specific files to avoid)

### Step 4: Preview Before Writing

Show the full list of files that will be created, grouped by action:

```
Files to COPY (unchanged from starter kit):
  .claude/rules/agent-loop.md
  .claude/commands/start.md
  ...

Files to GENERATE (from interview answers):
  CLAUDE.md
  .claude/settings.json
```

Ask for confirmation before writing any files.

### Step 5: Generate Files

1. Create directories: `admin/`, `.claude/agents/`, `.claude/commands/`, `.claude/rules/`
2. **Copy** all files marked "Copy" in the file mapping. Read each source file, then write to destination.
3. **Generate** CLAUDE.md from `templates/CLAUDE.md.template` using interview answers:
   - Replace `{{PROJECT_NAME}}` with project name
   - Replace `{{PROJECT_DESCRIPTION}}` with description
   - Replace `{{TECH_STACK}}` with tech stack
   - Replace `{{KEY_DIRECTORIES}}` with directory list
   - Replace `{{TEST_COMMAND}}`, `{{BUILD_COMMAND}}`, `{{LINT_COMMAND}}` with commands
   - Replace `{{PATTERNS}}` with patterns to follow
   - Replace `{{NEVER_DO}}` with things Claude should never do
   - If voice profile exists, add a Voice section referencing `admin/VOICE-PROFILE.md`
4. **Generate** `.claude/settings.json`:
   ```json
   {
     "permissions": {
       "allow": [
         "Bash(ls:*)",
         "Bash(git:*)",
         "Bash({{TEST_COMMAND}})",
         "Bash({{BUILD_COMMAND}})",
         "Bash({{LINT_COMMAND}})"
       ]
     }
   }
   ```
   Omit test/build/lint entries if the user didn't provide them.

### Step 6: Report

List all created files. Then print:

```
Setup complete. Created [N] files.

Next steps:

1. BUILD YOUR VOICE PROFILE (most impactful step)
   Copy admin/AI-FACILITATOR-PROMPT.md into a Claude conversation.
   Let it interview you. Takes 2-4 hours. Transforms everything after.

2. Review and customize CLAUDE.md
3. Run `claude` in your project directory
4. Type /start to test the session ritual
5. Run /activate-voice after completing your voice profile
```

## Important

- NEVER overwrite existing files without asking
- Always preview before writing (Step 4)
- Generated CLAUDE.md should be under 100 lines
- Voice profile is always the first recommendation, never an afterthought
