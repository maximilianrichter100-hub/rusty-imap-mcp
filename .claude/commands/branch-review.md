---
description: Review the current branch diff against main before opening a PR
---
## Changed files

!`git diff --name-only origin/main...HEAD`

## Detailed diff

!`git diff origin/main...HEAD`

Review the above changes for:
1. Correctness bugs and panic paths reachable from untrusted email input
2. Violations of the coding standards in CLAUDE.md / AGENTS.md
3. Missing tests (error paths, edges, adversarial corpus fixtures)
4. Security impact on sanitization, audit log, posture matrix, TLS pinning

Give specific, actionable feedback per file. For deep security questions,
hand off to the matching agent in `.claude/agents/`.
