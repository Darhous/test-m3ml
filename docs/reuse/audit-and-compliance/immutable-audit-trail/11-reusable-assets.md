# Reusable Assets — Immutable Audit Trail

| Asset Type | Asset | Source | Reuse Note |
|---|---|---|---|
| Data Model | immudb's cryptographically-linked record structure | immudb | Directly informs the platform's own Audit Event schema (actor, action, resource, timestamp, prior-record hash). |
| API Design | immudb's SQL + verification API | immudb | Reference for the Audit and Compliance Module's own query contract exposed to Compliance/Auditor personas (Wave 2). |
