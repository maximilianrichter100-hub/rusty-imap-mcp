---
description: Investigate and fix a GitHub issue
argument-hint: [issue-number]
---
Look at issue #$ARGUMENTS in this repo.

!`gh issue view $ARGUMENTS`

Understand the bug and trace it to the root cause. Write a failing test that
reproduces it first, then fix it, then confirm the test passes with
`just test-fast -- <substring>`. Work on a feature branch, never on `main`.
