---
name: review
description: Review content or changes with structured feedback
---

Review what is specified in $ARGUMENTS:

- **A file path**: review that file
- **"changes" or "diff"**: review uncommitted changes (`git diff`)
- **"branch"**: review current branch vs main (`git diff main...HEAD`)
- **No argument**: ask what to review

Delegate to the `reviewer` agent for the actual review.

For content reviews, always check:
- [ ] Voice -- does it match `admin/VOICE-PROFILE.md`? (if it exists)
- [ ] No dead phrases from the voice profile?
- [ ] Source requirements met?

Output the review results directly to the user.
