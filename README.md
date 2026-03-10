# AI Brain Starter

Voice-first starter kit for Claude Code. Start with who you are, not what tools to use.

Created by [Vejde Ab](https://vejde.com) (Anna Hager).

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed (`npm install -g @anthropic-ai/claude-code`)
- Anthropic API key or [Claude Max subscription](https://claude.ai)
- Git

## Quick Start

```bash
git clone https://github.com/Vejde/ai-brain-starter.git
cd ai-brain-starter
claude
```

Inside Claude Code, scaffold into your project:

```
> /scaffold ~/my-project solo
```

The path is where YOUR project lives (not this repo). Use an absolute path like `~/my-project` or `/Users/you/work/client-x`. The scaffold copies files from this starter kit into that directory.

Interactive interview generates your CLAUDE.md, agents, rules, and a voice profile template. Takes 5 minutes.

**Fork or clone?** Clone is fine for getting started. If you want to track updates or contribute back, fork first, then clone your fork. Your actual projects live in separate directories — this repo is just the scaffolding tool.

After scaffolding, build your voice profile (the part that actually matters):

1. Copy `voice-profile/ai-facilitator-prompt.md` into a Claude conversation
2. Answer 100 questions about how you communicate (2-4 hours)
3. Save answers as `admin/VOICE-PROFILE.md`
4. Run `/activate-voice`

Done. Claude now writes like you, not like a chatbot.

## Alternative Paths

**Just the voice profile** (no scaffolding):
Work through [voice-profile/interview-guide.md](voice-profile/interview-guide.md) on your own or have someone interview you. Save to `admin/VOICE-PROFILE.md`, then run `/activate-voice`.

**Browse and copy**:
Look at [examples/solo-consultant/](examples/solo-consultant/) or [examples/dev-team/](examples/dev-team/) for complete working setups. Take what fits.

## What `/activate-voice` Does

Reads your completed voice profile and:
1. Extracts your dead phrases and hard nos into writing standards
2. Updates all content-producing agents to reference your profile
3. Adds voice-check to your review workflow
4. Adds a voice summary to CLAUDE.md

One command. Everything connected.

## Scaffold Profiles

| Profile | For | Creates |
|---------|-----|---------|
| `minimal` | Getting started | CLAUDE.md, settings, agent-loop, /start |
| `solo` | Solo consultants | + voice profile, reviewer, strategist, brand DNA |
| `team` | Dev teams | + explorer, code-reviewer, fix-issue skill |

## What's Inside

### Voice Profile (`voice-profile/`)

100 questions that force you to confront how you actually communicate.

| File | What it does |
|------|-------------|
| [interview-guide.md](voice-profile/interview-guide.md) | 100 questions across 9 sections |
| [voice-profile-template.md](voice-profile/voice-profile-template.md) | Structure for your answers |
| [ai-facilitator-prompt.md](voice-profile/ai-facilitator-prompt.md) | Turns AI into your interviewer |

### Agents (`.claude/agents/`)

| Agent | Purpose |
|-------|---------|
| `explorer` | Deep codebase exploration |
| `reviewer` | Structured review (code + content) |
| `strategist` | Business strategy coach |

### Commands (`.claude/commands/`)

| Command | Purpose |
|---------|---------|
| `/scaffold` | Generate Claude Code structure in any project |
| `/activate-voice` | Wire voice profile into your entire setup |
| `/start` | Session start ritual |
| `/review` | Structured review (includes voice check) |
| `/create-agent` | Generate new agent from template |
| `/create-command` | Generate new command from template |

### Rules (`.claude/rules/`)

| Rule | Purpose |
|------|---------|
| `agent-loop` | GATHER > ACT > VERIFY > REPEAT |
| `writing-standards` | Quality standards for generated text |

### Templates (`templates/`)

Business frameworks from production use: ICP, offerings, sales playbook, brand DNA.

### Documentation (`docs/`)

| Doc | What it covers |
|-----|---------------|
| [ARCHITECTURE.md](docs/ARCHITECTURE.md) | Layers, settings, frontmatter reference |
| [PATTERNS.md](docs/PATTERNS.md) | Hard-won lessons from production |
| [BRAND-DNA-TEMPLATE.md](docs/BRAND-DNA-TEMPLATE.md) | Framework for documenting your brand |

### Complete Examples

| Example | For |
|---------|-----|
| [solo-consultant](examples/solo-consultant/) | Freelancers, solopreneurs. Full voice profile included. |
| [dev-team](examples/dev-team/) | Development teams. Code review, exploration, fix-issue skill. |

## Architecture

Claude Code has five layers:

| Layer | When | Location |
|-------|------|----------|
| **CLAUDE.md** | Always loaded | Root |
| **Rules** | Always loaded | `.claude/rules/` |
| **Commands** | On demand (`/name`) | `.claude/commands/` |
| **Agents** | Delegated via Task tool | `.claude/agents/` |
| **Skills** | Preloaded into agents | `.claude/skills/` |

Golden rule: **CLAUDE.md under 150 lines.** Everything else goes in rules, commands, agents, or skills.

## Key Patterns

1. **Start with voice.** 2-4 hours. Transforms every interaction after.
2. **GATHER > ACT > VERIFY > REPEAT.** Don't let Claude run ahead without checking.
3. **Agents are specialists, not generalists.** "Business development agent" beats "general assistant."
4. **Reference, don't copy.** Agents point to your voice profile. They don't contain a copy.
5. **Progressive disclosure.** Rules load every session. Commands load on demand. Don't front-load.
6. **Never send an LLM to do a linter's job.** Automate what can be automated.
7. **Commit after every task.** Not after every session.

More in [docs/PATTERNS.md](docs/PATTERNS.md).

## Why

Everyone's Claude Code setup sounds the same. Competent, smooth, forgettable. Because the technology has nothing real to work with.

We give AI a topic and a tone. Sometimes a "write like a thought leader" instruction. Then we're surprised when it produces thought-leader-shaped filler.

The problem was never the AI. The problem is that we never articulated what makes us *us*.

This starter kit fixes that. You begin with yourself, not with scaffolding.

## Talk to Claude

Voice input changes everything. Instead of typing prompts, talk. Especially for voice profiles and brainstorming.

- **[jarrodwatts/claude-stt](https://github.com/jarrodwatts/claude-stt)** -- Speech-to-text plugin for Claude Code. Live streaming dictation. Install with `claude install-plugin jarrodwatts/claude-stt`
- **[fltman/whisper.cpp](https://github.com/ggerganov/whisper.cpp)** -- Local Whisper for offline transcription (C/C++ port, no cloud dependency)

## Credits

- **[shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice)** -- Command > Agent > Skills architecture
- **[fltman/project-scaffolder](https://github.com/fltman/project-scaffolder)** -- Progressive disclosure, WHAT/WHY/HOW framework
- **[Anthropic Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code)** -- The official documentation

## License

MIT. Use it, fork it, improve it.
