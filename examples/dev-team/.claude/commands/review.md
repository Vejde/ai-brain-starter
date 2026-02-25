---
name: review
description: Code review workflow. Review a file, diff, or branch.
---

Review what is specified in $ARGUMENTS:

- **A file path**: review that specific file
- **"changes" or "diff"**: review uncommitted changes (`git diff`)
- **"staged"**: review staged changes (`git diff --cached`)
- **"branch"**: review current branch vs main (`git diff main...HEAD`)
- **A PR number**: review the pull request (`gh pr diff $ARGUMENTS`)
- **No argument**: ask what to review

Delegate to the `code-reviewer` agent for the actual review.

Output the review results directly to the user.
