# AI Brain Starter

Most AI setups start with technology. This one starts with you.

100 questions that force you to confront how you actually communicate. The output is a voice profile that makes AI write like you, not like a chatbot. Then: agents, commands, and workflows that build on that foundation.

The result is a Claude Code environment that feels like yours from the first sentence it produces.

Created by [Vejde Ab](https://vejde.com) (Anna Hager).

---

## The Idea

Everyone's Claude Code setup sounds the same. Competent, smooth, forgettable. Because the technology has nothing real to work with.

We give AI a topic and a tone. Sometimes a "write like a thought leader" instruction. Then we're surprised when it produces thought-leader-shaped filler.

The problem was never the AI. The problem is that we never articulated what makes us *us*.

This starter kit fixes that. You begin with yourself, not with scaffolding.

## How It Works

```
1. VOICE       Who are you? (100 questions, voice profile)
2. ACTIVATE    /activate-voice wires your profile into everything
3. STANDARDS   Writing rules extracted from YOUR voice (not generic defaults)
4. AGENTS      Specialized AI partners that read your voice before writing
5. WORKFLOW    Commands and rituals, with voice-check built in
```

Step 2 is the bridge. It reads your completed voice profile and extracts your dead phrases into writing standards, adds voice references to every agent that writes, and puts voice-check into your review workflow. One command, everything connected.

## Quick Start

### Option A: Start with your voice (recommended)

```bash
git clone https://github.com/vejdeab/ai-brain-starter.git
cd ai-brain-starter
claude
```

Then either:
- Copy `voice-profile/ai-facilitator-prompt.md` into Claude and let it interview you (2-4 hours, best results)
- Work through `voice-profile/interview-guide.md` on your own
- Have someone interview you using the guide

Your answers become `admin/VOICE-PROFILE.md`. Then run `/activate-voice` to wire it into your entire setup.

### Option B: Scaffold a project

```bash
# Inside the starter kit
> /scaffold /path/to/your/project solo
```

Interactive interview generates your CLAUDE.md, agents, and rules.
The `solo` profile includes voice profile setup.

### Option C: Browse and copy

Look at `examples/solo-consultant/` or `examples/dev-team/`
for complete working setups. Copy what fits.

## What's Inside

### Voice Profile (`voice-profile/`)

The core of the kit. An open-source process for capturing your authentic voice.

| File | What it does |
|------|-------------|
| [interview-guide.md](voice-profile/interview-guide.md) | 100 questions across 9 sections. The process. |
| [voice-profile-template.md](voice-profile/voice-profile-template.md) | Structure for your answers |
| [ai-facilitator-prompt.md](voice-profile/ai-facilitator-prompt.md) | Turns AI into your interviewer |
| [examples/anna-hager.md](voice-profile/examples/anna-hager.md) | What a finished profile looks like |

### Working Agents (`.claude/agents/`)

| Agent | Purpose |
|-------|---------|
| `explorer` | Deep codebase exploration |
| `reviewer` | Structured review (code + content) |
| `strategist` | Business strategy coach |

### Working Commands (`.claude/commands/`)

| Command | Purpose |
|---------|---------|
| `/scaffold` | Generate Claude Code structure in any project |
| `/activate-voice` | Wire a completed voice profile into your entire setup |
| `/start` | Session start ritual |
| `/review` | Structured review workflow (includes voice check) |
| `/create-agent` | Generate new agent from template |
| `/create-command` | Generate new command from template |

### Rules (`.claude/rules/`, always loaded)

| Rule | Purpose |
|------|---------|
| `agent-loop` | GATHER > ACT > VERIFY > REPEAT |
| `writing-standards` | Quality standards for generated text |

### Templates (`templates/`)

Business frameworks from production use:
- ICP (Ideal Customer Profile) framework
- Productized offerings structure
- Sales playbook framework
- Brand DNA structure

### Documentation (`docs/`)

| Doc | What it covers |
|-----|---------------|
| [ARCHITECTURE.md](docs/ARCHITECTURE.md) | Command > Agent > Skills pattern, layers, settings |
| [PATTERNS.md](docs/PATTERNS.md) | Hard-won lessons from production |
| [BRAND-DNA-TEMPLATE.md](docs/BRAND-DNA-TEMPLATE.md) | Framework for documenting your brand |

### Complete Examples

| Example | For | Includes |
|---------|-----|----------|
| `solo-consultant` | Freelancers, solopreneurs | Agents, commands, filled-in voice profile |
| `dev-team` | Development teams | Code review, exploration, fix-issue skill |

## Architecture

Claude Code has five layers. Use them in order of need:

| Layer | What | When | Location |
|-------|------|------|----------|
| **CLAUDE.md** | Project identity | Always loaded | Root |
| **Rules** | Always-on guardrails | Every session | `.claude/rules/` |
| **Commands** | User-triggered workflows | On demand | `.claude/commands/` |
| **Agents** | Specialized subagents | Delegated tasks | `.claude/agents/` |
| **Skills** | Preloaded knowledge for agents | Agent startup | `.claude/skills/` |

The golden rule: **CLAUDE.md under 150 lines.** Everything else goes
in rules, commands, agents, or skills.

## Patterns

1. **Start with voice.** Everything else builds on knowing who you are.
   A voice profile takes 2-4 hours and transforms every interaction after.

2. **GATHER > ACT > VERIFY > REPEAT.** The agent loop.
   Don't let Claude run ahead without checking its work.

3. **Keep CLAUDE.md under 150 lines.** It loads every session.

4. **Progressive disclosure.** Rules load every session. Commands load on demand.
   Skills preload into agents. Don't front-load everything.

5. **Never send an LLM to do a linter's job.** Automate what can be automated.

6. **Agents are specialists, not generalists.** "Business development agent"
   beats "general assistant."

7. **Reference, don't copy.** Agents point to your voice profile.
   They don't contain a copy of it.

8. **Commit after every task.** Not after every session.

More in [docs/PATTERNS.md](docs/PATTERNS.md).

## Scaffold Profiles

| Profile | For | Creates |
|---------|-----|---------|
| `minimal` | Getting started | CLAUDE.md, settings, agent-loop, /start |
| `solo` | Solo consultants | + voice profile, reviewer, strategist, brand DNA |
| `team` | Dev teams | + explorer, code-reviewer, fix-issue skill |

## Credits

This starter kit stands on the shoulders of:

- **[shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice)**
  Command > Agent > Skills architecture, frontmatter references, workflow best practices.

- **[fltman/project-scaffolder](https://github.com/fltman/project-scaffolder)**
  Progressive disclosure, WHAT/WHY/HOW framework, "never send an LLM to do a linter's job."

- **[Anthropic Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code)**
  The official documentation that makes all of this possible.

## Philosophy

"AI as craft, not commodity."

Anyone can install Claude Code. The difference is in how you set it up.
Most people start with the technology. We start with the person.

A voice profile, purpose-built agents, and clear workflows turn Claude
from a general assistant into something that sounds like you, thinks
like your best advisor, and works the way you work.

This repo gives you the starting patterns. You make them yours.

## License

MIT. Use it, fork it, improve it.

Created by [Vejde Ab](https://vejde.com).
