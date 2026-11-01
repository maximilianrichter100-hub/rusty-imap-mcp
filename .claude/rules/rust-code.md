---
paths:
  - "crates/**/*.rs"
  - "xtask/**/*.rs"
---
# Rust coding rules

Full text: AGENTS.md, "Coding standards" and "Testing expectations".

- Zero clippy warnings (`just lint`)
- No `unwrap()`, `println!`, `eprintln!`, `dbg!`, `todo!` outside tests;
  log through `tracing`
- No `#[allow(...)]` — use `#[expect(...)]` with a comment saying why
- No panics in functions returning `Result`
- No wildcard matches and no `matches!`; destructure explicitly
- 100-char lines, absolute imports, `#![deny(missing_docs)]` on public crates
- Prefer `for` loops with accumulators over non-trivial iterator chains
- Proptest for parsers and the Unicode/HTML pipeline, insta for sanitizer output
