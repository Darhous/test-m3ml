# Architecture Review — Patient Registry / MPI

Recommended: model the platform's own Patient Aggregate against the FHIR
`Patient` resource shape (identifiers, name, demographics, contact,
identity-linkage) — a Reference, not an Engine, decision, preserving
Core Domain ownership per ADR-0011. Full MPI-grade probabilistic
matching (OpenCR/HAPI MDM) is **not adopted now** — no measured need
(Risk Register #1, no confirmed tenant/patient-volume figures) — but
identified as the evidence-based upgrade path if/when duplicate-patient-
identity issues are actually measured across facilities within a tenant.
