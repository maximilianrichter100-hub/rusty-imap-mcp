# Project: rusty-imap-mcp

Security-first MCP server for IMAP email, written in Rust. Every byte of email
content is untrusted adversarial input; prompt injection is the #1 threat.

This file holds the essentials. The full contributor guide is
[AGENTS.md](AGENTS.md) — read the relevant section before non-trivial work.
Design specs live in `docs/superpowers/specs/`, plans in `docs/superpowers/plans/`.

## Commands

Always use `just`, never bare cargo for checks. If `just ci` passes, CI passes.

```bash
just check        # fast compile-check (inner loop)
just fmt          # format in place
just lint         # clippy -D warnings
just test-fast    # inner-loop unit tests, no containers (1–3 min)
just test         # full nextest workspace — run in the background
just ci           # full local-CI equivalent (tens of minutes) — run in the background
```

Narrow a failure with `cargo nextest run -p <crate> -E 'test(substring)'` or
`just test-fast -- substring`, never a workspace sweep.

## Architecture

- Cargo workspace, edition 2024, toolchain 1.94.0, MSRV 1.88.0
- `crates/rimap-core` shared types · `rimap-config` · `rimap-imap` (transport)
  · `rimap-content` (sanitizer, no network deps) · `rimap-audit` (JSONL log)
  · `rimap-authz` (posture matrix) · `rimap-smtp` · `rimap-server` (bin)
- Crate isolation is load-bearing: no new cross-crate coupling
- Dependencies only in root `[workspace.dependencies]`, members use `workspace = true`

## Conventions

- No `unwrap()`, `println!`, `dbg!`, `todo!`, `#[allow]`, `matches!` or
  wildcard matches in non-test code (stdout is the MCP transport)
- `thiserror` in libraries, `anyhow` in `rimap-server`
- Newtypes over primitives, enums over boolean flags, absolute imports only
- TDD: failing test first. Test behavior, not implementation
- Commits: imperative, ≤72 chars, conventional prefixes (`feat:`, `fix:`, …)

## Watch out for

- Never commit on `main`; never `--no-verify`, never amend pushed commits
- MSRV 1.88.0 — no newer syntax or dependencies
- `.snap` diffs in wire transcripts are agent-facing changes: never blind-accept
- No new runtime dependencies without explicit approval
- Not done until `just ci` is green locally
