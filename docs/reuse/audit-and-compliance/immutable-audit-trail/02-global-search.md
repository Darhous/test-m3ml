# Global Search Log — Immutable Audit Trail

## Query Run

`open source immutable audit log tamper-evident logging system 2026
healthcare`

## Landscape Notes

**immudb** (Codenotary) surfaced as the strongest, most directly relevant
candidate — a cryptographically-verifiable immutable database, with its
own May 2026 release explicitly citing healthcare as a target regulated
industry ("simplified compliance by relying on built-in, trustworthy
audit trails instead of complex logging setups"). Two other credible
architectural patterns found: **Trillian/transparency.dev** (a
Google-originated tamper-evident Merkle-tree log, the same technology
class underlying Certificate Transparency — general-purpose, more
infrastructure-heavy to operate) and a **DIY OpenTelemetry + append-only
storage + hash-chaining** pattern (a recipe, not a product — would be a
BUILD, not a Reuse candidate).

## Candidates Carried Forward

immudb (primary), Trillian (architectural alternative, heavier
operational footprint), PostgreSQL append-only-table-with-triggers
pattern (fallback BUILD option, evaluated for completeness).
