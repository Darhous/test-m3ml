# Master Engine Catalog

Candidates classified as a full **Engine** (a substantial runtime system
you deploy and adapt via configuration/plugins, e.g., a full LIS, a full
IAM server, a full workflow engine) — as distinct from a Library or SDK.
Cross-references `10-final-decision.md` entries with an ENGINE + ADAPTER
decision.

| Module | Feature | Engine | What It Replaces | Adapter Boundary |
|---|---|---|---|---|
| Identity and Access | authentication, sso-oidc-oauth, multi-factor-auth, session-management, user-group-management | Keycloak | A full custom-built IAM system (credential storage, OIDC/OAuth2/SAML provider, MFA, session store, admin console) | Anti-Corruption Layer inside the Identity and Access Bounded Context — OIDC/OAuth2 + Admin REST API only |
| Identity and Access | authorization-rbac-abac | Open Policy Agent | A custom rules engine for the 8-dimension Configurable Result Verification Policy Model | Called only by the Result Verification and Reporting Module |
| Tenant and Organization Management | feature-flags, tenant-configuration | Unleash (via OpenFeature) | Custom-built flag/config service, custom rollout-approval workflow | Platform code calls the OpenFeature SDK, not Unleash's proprietary SDK |
| Audit and Compliance | immutable-audit-trail | immudb | A custom cryptographic append-only log implementation | Audit and Compliance Module's own write path only |
| Audit and Compliance | policy-engine | Open Policy Agent (reused) | A second, separate policy engine | Same OPA instance as Identity and Access, separately namespaced bundles |
| Audit and Compliance | compliance-tracking (tentative) | Eramba Community | A custom internal GRC tool | Standalone internal tool, no runtime Module dependency |
| Device Integration Gateway | hl7-integration-engine, astm-integration | Mirth Connect 4.5.2 (frozen, tentative) or Apache Camel | A full custom HL7/ASTM parsing and channel-routing engine | Independent Component (ADR 0006); frozen-OSS risk explicitly flagged |
| Device Integration Gateway | message-broker-queueing | RabbitMQ | A custom durable-queue implementation | Platform-wide Shared Technical Service, not per-Module |
| Notification Service | multi-channel-notification-engine, templating, delivery-tracking, whatsapp-integration | Novu | N separate vendor SDK integrations (Email/SMS/Push/WhatsApp) built and maintained individually | Independent Component (Constitution Section 11); license `Requires Legal Verification` |
| AI Operations Gateway | llm-gateway-orchestration | Portkey Gateway | A custom LLM-provider-abstraction and guardrail layer | Independent Component; full OSS release March 2026 |
| Analytics | bi-dashboards, embedded-analytics, reporting-engine | Apache Superset | A custom BI/dashboarding and white-label embedding system | White-Label embedding SDK boundary; Metabase rejected (OSS tier paywalls embedding) |
| Document Management | document-storage-versioning, document-control-workflow | Alfresco Community | A custom document-versioning + approval-workflow engine | Resolves Module 3's deferred `document-control` duplicate |
| Document Management | e-signature | Documenso | A custom e-signature/consent-capture flow | Sensitive-Operation-adjacent Feature |
| Scheduling and Encounters | appointment-scheduling-engine | Cal.com | A custom patient-facing booking engine | Patient-facing only; distinct from Workforce Management's staff Roster |
| Laboratory Execution | analyzer-middleware-integration | Mirth Connect / Apache Camel (reused) | N/A | Cross-Feature Dependency on Module 4's engine |
| Asset and Maintenance | asset-registry, preventive-maintenance-scheduling, calibration-management, spare-parts-tracking (superseded) | Atlas CMMS | A custom CMMS (asset registry, PM scheduling) | 1st non-Core-Domain whole-system Engine adoption; openMAINT credible fallback |
| Inventory | stock-management, warehouse-management, expiry-batch-tracking, barcode-scanning (partial), cold-chain-tracking | OpenBoxes | A custom healthcare-supply-chain inventory system | Cleanest license (EPL-1.0) of any Engine in the program; supersedes Atlas CMMS's tentative Parts module |
| Procurement | purchase-requisition-order, supplier-rfq, receiving-goods (PO matching only) | ERPNext (Buying module) | A custom requisition→RFQ→PO→approval chain | Explicitly does NOT use ERPNext's own stock module (proactive duplicate avoidance vs. OpenBoxes) |
| Supplier Management | supplier-registry-evaluation, contract-management | ERPNext (reused) | N/A | Cross-Module Cross-Feature Dependency, no new research |
| Billing | invoicing-engine, pricing-price-lists, collections-dunning | ERPNext (reused) | N/A | pricing-price-lists layered on, not duplicating, Module 12's catalog pricing |
| Payments and Treasury | cashbox-treasury-management | ERPNext (reused) | N/A | 4th Module reusing ERPNext |
| Insurance and Corporate Contracts | eligibility-verification, claims-management, corporate-contract-rates | openIMIS | A custom health-insurance/claims administration system | Digital Public Good; module-level adoption, not Core Domain |
| Accounting | general-ledger, expense-tracking, external-erp-integration | ERPNext (reused) | N/A | Resolves Wave 3's Native/Integration/Deferred open question concretely |
| Workforce Management | employee-records-hr, attendance-time-tracking, staff-scheduling-shifts, training-competency | Frappe HR | A custom HRMS | Same-vendor-family sibling to ERPNext; GPL-3.0 (same posture) |
| Payroll | payroll-calculation-engine | Frappe HR (reused) | N/A | 6th Feature reusing Frappe HR |
| CRM and Support | helpdesk-ticketing, call-center-crm, complaint-feedback-management | Frappe Helpdesk / Frappe CRM | A custom ticketing/CRM system | Same-vendor-family but AGPL-3.0 (license-drift finding vs. ERPNext/HR's GPL-3.0) |
| SaaS Commercial Operations | subscription-plan-management, usage-metering-entitlements, saas-billing | Kill Bill | A custom subscription/proration/invoicing engine | Explicitly distinct from ERPNext's patient/client billing (2 revenue domains); cleanest license alongside OpenBoxes |

**Program complete.** ERPNext is the program's broadest single-Engine
footprint (5 Modules: Procurement, Supplier Management, Billing,
Payments and Treasury, Accounting), followed by OPA (8 Features across
6 Modules) and Frappe HR (2 Modules: Workforce Management, Payroll).
