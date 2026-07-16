# Integration Options — Consent Management

Consent status stored as a platform-owned, RLS-isolated Aggregate
(FHIR-`Consent`-shaped). Enforcement checks call the same OPA instance
already integrated for Result Verification (Module 1,
`authorization-rbac-abac`) — consent becomes one more attribute in a
policy evaluation, not a separately-built rules engine. All
consent-check decisions are written to the immudb-backed audit trail
(`immutable-audit-trail`, this Module).
