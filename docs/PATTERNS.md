# Patterns -- Lessons from Production

## Voice First

1. **Start with voice.** The single most impactful thing you can do is
   build a voice profile before anything else. 100 questions, 2-4 hours,
   and everything Claude produces sounds like you instead of a chatbot.
   See `voice-profile/` for the full process.

2. **80% boundaries, 20% aspirations.** What you refuse to do defines
   your voice more than what you choose to do. The "dead phrases" and
   "hard nos" sections of a voice profile do more work than the rest combined.

3. **Agents reference voice, never copy it.** Every agent that writes
   content should read `admin/VOICE-PROFILE.md`. None should contain
   voice rules inline. Single source of truth.

## From Vejde Ab

4. **Agent loop is non-negotiable.** GATHER > ACT > VERIFY > REPEAT.
   Without it, Claude will confidently produce wrong results.

5. **Dual-voice routing.** If you write as both yourself and your company,
   define both voices and route content to the right one.

6. **The description field is king.** Agent descriptions with
   "Use PROACTIVELY when..." auto-trigger correctly.

7. **30-50 line agents.** Keep agent files lean. Put reference
   material in separate files the agent reads on demand.

8. **Pricing is market value, not time.** Price based on what
   the result is worth, not the hours you spend. Track both.

## From shanraisshan/claude-code-best-practice

9. **CLAUDE.md under 150 lines.** Longer files get increasingly ignored.

10. **Commands for workflows, agents for delegation.** Don't make agents
    for things you trigger manually. Use commands for that.

11. **Feature-specific agents with skills beat general-purpose agents.**
    "code-reviewer with deploy-checklist skill" beats "senior engineer."

12. **Compact at 50%.** Don't wait for context to fill.

13. **Subtasks under 50% context.** If a task can't fit in half
    the context window, break it smaller.

14. **Commit after every task.** Not after every session.

15. **Subagents cannot invoke other subagents via bash.** Use the Task tool.

## From fltman/project-scaffolder

16. **Progressive disclosure.** Only universally-applicable instructions
    in CLAUDE.md. Everything else loads on demand.

17. **Never send an LLM to do a linter's job.** Put test/build/lint
    in verification commands. Automate what can be automated.

18. **WHAT/WHY/HOW.** Every CLAUDE.md answers: what is this project,
    why were these decisions made, how do I verify my work.

19. **Safe file boundaries.** Tell Claude which files it can edit
    and which it should never touch.

## Combined Insights

20. **Start with /start.** A session start ritual that checks git status,
    establishes context, and sets expectations. Saves time every session.

21. **Templates over empty files.** Annotated templates with comments
    teach while scaffolding. Empty files teach nothing.
