# Final Decision — Immutable Audit Trail

## Decision: **ENGINE + ADAPTER**

**Engine:** immudb (Apache-2.0). **Adapter:** the Audit and Compliance
Module's own write path, fed by the message-broker pipeline already
recommended in Module 1.

## Why Not Trillian

Credible, equally strong on tamper-evidence, but heavier operational
footprint (designed for planet-scale Certificate Transparency logs) and
no native SQL query layer — would require a secondary read-store for
audit-record browsing/reporting, an avoidable complexity given immudb
offers both properties natively.

## Why Not Build (Postgres Append-Only)

Scored lowest specifically on Security (2/5) — cannot make the
cryptographic-tamper-evidence claim Risk #25 actually needs; a
sufficiently privileged actor could still alter a plain Postgres table
regardless of `REVOKE` grants (a superuser bypass), which is exactly the
threat Risk #25 names.
