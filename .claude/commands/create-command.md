---
name: create-command
description: Create a new slash command from template
---

Create a new command in `.claude/commands/`.

## Arguments

$ARGUMENTS should contain: `<command-name> [description]`

## Process

### Step 1: Gather Information

If not provided in arguments, ask for:
1. **Name**: Short, descriptive (kebab-case, e.g., `deploy-check`)
2. **Purpose**: What workflow does this command trigger?
3. **Arguments**: What input does it expect (if any)?
4. **Delegation**: Should it delegate to an agent, or execute directly?

### Step 2: Generate Command File

Read `templates/command.md.template` for structure reference.
Create `.claude/commands/<name>.md` following that structure.

### Step 3: Verify

List the generated file and confirm it looks correct.
Suggest testing with: `/<name> [test arguments]`
