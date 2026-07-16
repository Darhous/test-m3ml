# Master Shared Components Register

Components that, once adopted for one Feature, should be reused as
shared infrastructure across multiple Modules rather than adopted
independently per Module (e.g., a single Keycloak realm-per-tenant setup
serving every Business Module's authentication need, not one per Module).

| Shared Component | Candidate | Serves (Modules/Features) | Why Shared, Not Per-Module |
|---|---|---|---|
| Identity Provider | Keycloak (single instance, Organizations-based multi-tenancy) | Every Module (universal dependency, Wave 10 Platform Kernel) | One Keycloak deployment with tenant-scoped Organizations, not one Keycloak per Module or per tenant — matches ADR 0005's Hybrid Tenant Isolation direction and Constitution Section 10's Core Platform rule |
| Fine-Grained Policy Engine | OPA | Result Verification and Reporting (Identity and Access); Elevated Audit tier (Audit and Compliance); Consent enforcement (Audit and Compliance) | Scoped to Sensitive-Operation-grade decisions specifically, not deployed as a general-purpose per-Module authorization layer — one instance, namespaced policy bundles, now confirmed reused by 3 distinct Features across 2 Modules |
| Immutable Audit Store | immudb | Every Module emitting Sensitive-Operation or identity events | One canonical audit-write path (via the message-broker pipeline), not per-Module custom logging |
| Message Broker | RabbitMQ | Device Integration, Identity and Access (audit hooks), Audit and Compliance (immudb feed), and any future durable cross-Module event delivery | One platform-wide durable-delivery backbone, not one broker per Module |
| Fine-Grained Policy Engine (OPA, updated) | OPA | Result Verification (Identity and Access), Governance policy + Consent (Audit and Compliance), AI use-case governance (AI Operations Gateway) | Now confirmed reused across 4 distinct Features in 3 Modules — the program's strongest Cross-Feature Dependency case |
