---
paths:
  - "crates/rimap-content/**"
  - "crates/rimap-audit/**"
  - "crates/rimap-authz/**"
  - "crates/rimap-core/**"
  - "crates/rimap-imap/**"
  - "tests/injection-corpus/**"
---
# Security-sensitive crates

Full text: AGENTS.md, "Security-sensitive work".

- `rimap-content`: keep the adversarial corpus green; add a fixture for every
  new attack class. The corpus only grows
- `rimap-audit`: never hold the file lock across `.await`; never swallow write
  errors (they surface as `ERR_INTERNAL`); `log_*` methods take one record arg
- `rimap-authz` / `rimap-core`: new tools update the posture matrix in
  `rimap-core` first; denied tools must not be advertised in `list_tools`
- `rimap-imap` TLS verifier: reject on fingerprint mismatch before any data
  flows; never fall back to system trust
