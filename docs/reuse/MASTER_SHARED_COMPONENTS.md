# Master Shared Components Register

Components that, once adopted for one Feature, should be reused as
shared infrastructure across multiple Modules rather than adopted
independently per Module (e.g., a single Keycloak realm-per-tenant setup
serving every Business Module's authentication need, not one per Module).

| Shared Component | Candidate | Serves (Modules/Features) | Why Shared, Not Per-Module |
|---|---|---|---|
| Identity Provider | Keycloak (single instance, Organizations-based multi-tenancy) | Every Module (universal dependency, Wave 10 Platform Kernel) | One Keycloak deployment with tenant-scoped Organizations, not one Keycloak per Module or per tenant — matches ADR 0005's Hybrid Tenant Isolation direction and Constitution Section 10's Core Platform rule |
| Fine-Grained Policy Engine | OPA | Result Verification and Reporting today; any future Sensitive/Elevated-Audit-tier consumer | Scoped to Sensitive-Operation-grade decisions specifically, not deployed as a general-purpose per-Module authorization layer — avoids over-engineering low-risk Modules |
