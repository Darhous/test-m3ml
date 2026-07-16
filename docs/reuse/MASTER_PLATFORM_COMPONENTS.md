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
