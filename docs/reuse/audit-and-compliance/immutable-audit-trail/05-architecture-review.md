# Architecture Review — Immutable Audit Trail

| Dimension | immudb | Trillian | PostgreSQL append-only (BUILD) |
|---|---|---|---|
| Purpose-fit | Purpose-built for exactly this use case (audit-trail-as-a-database) | General-purpose verifiable log — more assembly required to become "the audit trail" specifically | Achievable, but tamper-evidence (cryptographic proof, not just "no DELETE grant") requires custom hash-chaining code |
| Query model | Full SQL layer alongside the immutability guarantee — audit records remain queryable like normal data | Primarily an append/verify API, not a rich query layer — would need a secondary read-store | Native SQL (Postgres), no extra layer needed, but no cryptographic proof |
| Operational footprint | One additional deployed service | One additional deployed service, generally heavier operationally (originally built for planet-scale CT logs) | Zero extra service — reuses the already-selected PostgreSQL |
| Cryptographic verifiability | Yes — every record cryptographically linked, independently verifiable | Yes — Merkle-tree proofs | No — relies on access-control discipline only, the weakest guarantee of the three |

## Assessment

immudb is the strongest fit: purpose-built, SQL-queryable (avoiding a
second read-path other Modules would need to learn), Apache-2.0, and
explicitly healthcare-framed by its own maintainers in 2026. Directly
composes with Module 1's `audit-hooks-integration` Feature (the event
source) and Constitution Section 23's immutability requirement.
