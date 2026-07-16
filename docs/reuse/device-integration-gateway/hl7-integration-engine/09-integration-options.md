# Integration Options — HL7 Integration Engine

Deploy as the ADR 0006 Independent Component's own gateway process, never
called directly by other Modules — output normalized into the platform's
own Domain Events, published via the message broker (`message-broker-
queueing`, this Module). Idempotency keys (Constitution Section 48)
applied at ingestion per Module 1's `audit-hooks-integration` finding
about device-message replay.
