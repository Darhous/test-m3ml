# Master Platform Components Register

Candidates specifically serving the Platform Kernel (Identity and Access,
Tenant and Organization Management, Audit and Compliance) and Shared
Infrastructure (Device Integration Gateway, Notification Service, AI
Operations Gateway) layers — the components every other Module depends
on, per Wave 10's Domain Core / Platform Kernel / Shared Infrastructure
distinction.

| Layer | Component | Candidate | Decision | Note |
|---|---|---|---|---|
| Platform Kernel | Identity Provider (Identity and Access Module) | Keycloak | ENGINE + ADAPTER | Solves 6 of this Module's 7 Features; see `MASTER_DEPENDENCY_MATRIX.md` |
| Platform Kernel | Fine-Grained Policy Engine (Identity and Access Module) | Open Policy Agent | ENGINE + ADAPTER | Scoped to Sensitive-Operation-grade decisions |
| Platform Kernel | Multi-Tenant Data Isolation (Tenant and Organization Management Module) | PostgreSQL Row-Level Security | REFERENCE | Evidence toward `open-questions.md` #15, not a resolution of it |
| Platform Kernel | Feature Flags / Tenant Configuration (Tenant and Organization Management Module) | Unleash + OpenFeature | ENGINE + ADAPTER | Shared engine across 2 Features |
| Platform Kernel | Immutable Audit Trail (Audit and Compliance Module) | immudb | ENGINE + ADAPTER | Cryptographic tamper-evidence, mitigates Risk #25 |
| Platform Kernel | Governance Policy Engine (Audit and Compliance Module) | OPA (reused from Identity and Access) | ENGINE + ADAPTER | 2nd Module reusing the same engine |
| Platform Kernel | Compliance Tracking (Audit and Compliance Module) | Eramba Community (tentative) | ENGINE + ADAPTER (low confidence) | Flagged for reconsideration at SAD time |
| Shared Infrastructure | HL7/ASTM Integration Engine (Device Integration Gateway Module) | Mirth Connect 4.5.2 (tentative) / Apache Camel | ENGINE + ADAPTER (frozen-OSS risk flagged) | Reused by Laboratory Execution's `analyzer-middleware-integration` |
| Shared Infrastructure | Message Broker (Device Integration Gateway Module) | RabbitMQ | ENGINE + ADAPTER | Platform-wide durable-delivery backbone |
| Shared Infrastructure | Multi-Channel Notification Engine (Notification Service Module) | Novu | ENGINE + ADAPTER | Reused by 4 Modules total (see `MASTER_SHARED_COMPONENTS.md`) |
| Shared Infrastructure | LLM Gateway (AI Operations Gateway Module) | Portkey Gateway | ENGINE + ADAPTER | Full OSS release March 2026 |
| Shared Infrastructure | Semantic Search (AI Operations Gateway Module) | pgvector | REFERENCE/LIBRARY | Reuses existing PostgreSQL, no dedicated vector DB |

**Scope note (final):** This register covers Platform Kernel and Shared
Infrastructure only, per Wave 10's layer distinction — the 19 Business
Modules and the Commercial Module each have their own dominant Engine
(ERPNext, OpenBoxes, Frappe HR, openIMIS, Kill Bill, etc.), catalogued
in `MASTER_ENGINE_CATALOG.md` and `MASTER_SHARED_COMPONENTS.md` instead,
not duplicated here. Program complete — this table is final.
