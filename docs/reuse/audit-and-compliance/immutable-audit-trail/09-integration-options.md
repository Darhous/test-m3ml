# Integration Options — Immutable Audit Trail

immudb deployed as a separate service; the message broker path already
recommended in Module 1's `audit-hooks-integration` Feature (Keycloak
Event Listener SPI → broker → this Feature) writes into immudb rather
than a generic log sink. Every other Module's own Sensitive-Operation
events (Result Verification, Payroll dual-control) follow the same
pipeline shape, giving the platform one canonical immutable-audit
ingestion path rather than per-Module custom logging.
