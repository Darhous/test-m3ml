# Candidate Repositories — Immutable Audit Trail

| Candidate | Repository | What It Is | Latest Activity |
|---|---|---|---|
| immudb | `codenotary/immudb` | Cryptographically-verifiable immutable database (key-value + SQL layer), purpose-built for tamper-evident audit trails | Active — 1.11 released May 2026, explicit healthcare-compliance framing |
| Trillian | `google/trillian` | Merkle-tree-based tamper-evident log (Certificate Transparency's underlying tech), general-purpose append-only verifiable log | Active, mature (Google-originated, widely used in the CT ecosystem), lower-frequency releases than immudb |
| PostgreSQL append-only pattern (BUILD fallback) | N/A — pattern, not a repository | `REVOKE UPDATE/DELETE` + insert-only table + optional row-hash-chaining trigger | N/A |
