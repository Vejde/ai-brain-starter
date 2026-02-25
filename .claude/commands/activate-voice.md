---
name: activate-voice
description: Wire a completed voice profile into your entire Claude Code setup
---

Take a completed voice profile and connect it to every part of your Claude Code setup.

This is the bridge between step 1 (voice) and steps 2-4 (standards, agents, workflow).

## Arguments

$ARGUMENTS should contain the path to your completed voice profile.
Default: `admin/VOICE-PROFILE.md`

## What This Command Does

Reads your voice profile and:
1. Extracts key patterns into writing standards
2. Updates all content-producing agents to reference your profile
3. Adds voice-check to your review workflow
4. Adds a voice summary to CLAUDE.md

## Process

### Step 1: Read the Voice Profile

Read the file specified in $ARGUMENTS (or `admin/VOICE-PROFILE.md`).

Extract:
- **Quick Reference Card** -- the three most important things, always/never lists
- **Dead phrases** -- from Section 3 (Aesthetic Crimes)
- **Hard nos** -- from Section 6
- **Emotional target** -- from Section 4 (what should the reader feel?)
- **Structural preferences** -- from Section 5 (openers, closers, formatting)
- **Language variations** -- from Section 2 (if multilingual)

### Step 2: Update Writing Standards

Open `.claude/rules/writing-standards.md`. Add or update these sections:

**Voice -- Always** (from Quick Reference Card "Always" list and structural preferences):
```
## Voice -- Always

- [extracted from profile: opening moves]
- [extracted from profile: closing moves]
- [extracted from profile: structural preferences]
- Trust the reader's competence
```

**Voice -- Never** (from Dead Phrases and Hard Nos):
```
## Voice -- Never

- [each dead phrase from Section 3]
- [each stylistic dealbreaker from Section 6]
- [each engagement tactic refused from Section 6]
```

**Ongoing Language Learning** (always include this):
```
## Ongoing Language Learning

- ALWAYS learn from the user's actual language use: edits, additions, comments, word choices
- Update voice profile Section 9 with new patterns when observed
- Prioritize what the user actually writes over what they say they write
```

If multilingual, add language-specific calibration from Section 2.

### Step 3: Update CLAUDE.md

Add a voice section to CLAUDE.md (after project description, before structure):

```
## Voice

Three things to always remember:

1. **[most important instruction from Quick Reference Card]**
2. **[second most important]**
3. **[third most important]**

Full voice profile: `admin/VOICE-PROFILE.md`
Writing standards: `.claude/rules/writing-standards.md`
```

### Step 4: Update Agents

For EACH agent in `.claude/agents/` that produces text (writing, communication, review):

Add to the agent's reference documents section:
```
Read at every invocation:
- `admin/VOICE-PROFILE.md` -- voice and tone source
- `.claude/rules/writing-standards.md` -- writing rules
```

Skip agents that only do code exploration or technical work.

### Step 5: Update Review Command

Open `.claude/commands/review.md`. Add voice check to the review checklist:

```
For content reviews, always check:
- [ ] Voice -- does it match `admin/VOICE-PROFILE.md`?
- [ ] No dead phrases from the voice profile?
- [ ] Source requirements met?
```

### Step 6: Report

Show what was changed:

```
Voice profile activated. Changes made:

CLAUDE.md
  + Added voice section with 3 key rules

.claude/rules/writing-standards.md
  + Voice -- Always: [N] rules extracted
  + Voice -- Never: [N] dead phrases + hard nos
  + Ongoing Language Learning section added

.claude/agents/[name].md
  + Voice profile reference added to [list agents updated]

.claude/commands/review.md
  + Voice check added to review checklist

Your voice profile is now wired into every part of your setup.
Claude will read admin/VOICE-PROFILE.md before producing any content.
```

## Important

- NEVER delete existing content in writing-standards.md. Add voice sections alongside existing rules.
- NEVER copy the full voice profile into agents or rules. Always reference the file path.
- If an agent already references the voice profile, skip it.
- Ask before overwriting any existing voice sections in CLAUDE.md.
