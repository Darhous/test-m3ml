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
| Fine-Grained Policy Engine (OPA, final) | OPA | authorization-rbac-abac (Identity and Access), policy-engine + Consent (Audit and Compliance), ai-use-case-governance (AI Operations Gateway), result-review-verification-workflow + result-amendment-workflow (Result Verification and Reporting), payroll-approval-dual-control (Payroll), usage-metering-entitlements (SaaS Commercial Operations) | **Final count: 8 confirmed reuses across 6 Modules** — the program's strongest Cross-Feature Dependency case, decided once at Module 1 and never re-derived |
| Multi-Channel Notification Engine (Novu) | Novu | Notification Service, Scheduling and Encounters (reminders), Result Verification and Reporting (critical-result-escalation), CRM and Support (campaign-management) | 4 Modules, one delivery Adoption Point — every platform-originated message routes through the same Engine |
| ERP / Financial Backbone (ERPNext) | ERPNext | Procurement, Supplier Management, Billing, Payments and Treasury, Accounting | 5 Modules — the program's broadest single-Engine footprint after Keycloak; explicitly does NOT own inventory (OpenBoxes) or SaaS subscription revenue (Kill Bill), both proactively kept separate |
| Inventory / Stock Ledger (OpenBoxes) | OpenBoxes | Inventory, Asset and Maintenance (spare parts, supersedes Atlas CMMS), Procurement (receiving-goods stock-increase step) | Single stock-management Adoption Point across 3 Modules |
| HR/Workforce Backbone (Frappe HR) | Frappe HR | Workforce Management, Payroll | Same-vendor-family sibling to ERPNext, kept as a separate app deployment |

**Program complete.** These 5 rows are the platform's core Shared
Component backbone, each confirmed reused across 3+ Modules — the
single strongest evidence in this program for the "if it can save 1000
hours, reuse it" directive, since each represents a mature capability
adopted once and consumed everywhere it applies rather than rebuilt or
re-decided per Module.
