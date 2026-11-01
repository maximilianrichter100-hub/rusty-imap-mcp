---
paths:
  - ".github/workflows/**"
  - ".github/actions/**"
---
# GitHub Actions rules

- `actionlint` and `zizmor` must pass
- Every `uses:` is a full 40-character SHA with a version comment; never a tag
  or branch
- A job outside the required status checks does not block merges — confirm the
  check name is required before adding a gate to it (AGENTS.md, "Git, commits,
  and PR workflow")
