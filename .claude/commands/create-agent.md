---
name: create-agent
description: Create a new subagent from template
---

Create a specialized subagent in `.claude/agents/`.

## Arguments

$ARGUMENTS should contain: `<agent-name> [description]`

## Process

### Step 1: Gather Information

If not provided in arguments, ask for:
1. **Name**: Short, descriptive (kebab-case, e.g., `grant-writer`)
2. **Purpose**: What specific task does this agent handle?
3. **Trigger**: When should Claude delegate to this agent?
4. **Tools needed**: Read, Edit, Write, Bash, Grep, Glob (limit to what's needed)
5. **Model**: sonnet (default), opus, haiku, or inherit

### Step 2: Generate Agent File

Read `templates/agent.md.template` for structure reference.
Create `.claude/agents/<name>.md` following that structure.

### Step 3: Description Quality Check

The description is CRITICAL for automatic invocation. It must include:
- What the agent does
- When it should be triggered
- "Use PROACTIVELY" if it should auto-trigger

### Step 4: Keep It Lean

- Agent file should be 30-50 lines
- Put detailed reference material in separate files
- Agent reads reference docs ON DEMAND, not at every invocation

### Step 5: Verify

List the generated file and confirm it looks correct.
Suggest testing with: "Use the <name> agent to..."
