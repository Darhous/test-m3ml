# Master Feature Catalog — Global Build-vs-Buy & Reuse Intelligence Program

**Purpose:** the complete, closed enumeration of every Feature in the
Healthcare Operations Platform, derived from Discovery (Wave 3 Enterprise
Capability Map — 100 capabilities, Wave 9 Bounded Contexts — 28 contexts,
Wave 10 Candidate Modules — 28 modules, Wave 5 Domain Events, Wave 6
Business Rules). Every Module and every Feature below is scoped — nothing
is unknown at the catalog level, even before its research files exist.
Features are grouped at *implementation grain* (buildable units), not a
1:1 restatement of the 100 capability rows — matching the worked example
in the program's own instructions (`inventory/` → `stock/`, `barcode/`,
`forecast/`, `expiry/`, `warehouse/`).

**Research Status legend:**
- `Researched` — full 13-file set exists under `docs/reuse/<module>/<feature>/`.
- `Pending` — scoped here, research not yet started.

**Total scope: 28 Modules, 106 Features.**

## Layer Classification (from Wave 10)

- **Platform Kernel:** Identity and Access, Tenant and Organization
  Management, Audit and Compliance.
- **Shared Infrastructure (Independent Components):** Device Integration
  Gateway, Notification Service, AI Operations Gateway.
- **Cross-Cutting Services:** Analytics, Document Management.
- **Business Modules:** the remaining 19 (Clinical, Laboratory, Financial,
  Supply Chain, Workforce, Customer Operations).
- **Commercial Module:** SaaS Commercial Operations.

## 1. Identity and Access (Platform Kernel)

| Feature | Source Capabilities (Wave 3) | Status |
|---|---|---|
| `authentication` | Security | Researched |
| `authorization-rbac-abac` | Security, Policy Management | Researched |
| `sso-oidc-oauth` | Security | Researched |
| `multi-factor-auth` | Security | Researched |
| `session-management` | Security | Researched |
| `user-group-management` | Security | Researched |
| `audit-hooks-integration` | Security ↔ Audit | Researched |

## 2. Tenant and Organization Management (Platform Kernel)

| Feature | Source Capabilities | Status |
|---|---|---|
| `tenant-provisioning` | Tenant Management | Researched |
| `organization-branch-hierarchy` | Organization Management, Branch Management | Researched |
| `multi-tenancy-isolation` | (Constitution Section 18/19, ADR 0005) | Researched |
| `feature-flags` | Feature Flags | Researched |
| `tenant-configuration` | Tenant Management | Researched |

## 3. Audit and Compliance (Platform Kernel)

| Feature | Source Capabilities | Status |
|---|---|---|
| `immutable-audit-trail` | Audit | Researched |
| `consent-management` | Consent | Researched |
| `policy-engine` | Policy Management | Researched |
| `compliance-tracking` | Compliance, Risk | Researched |
| `document-control` | Document Control | Researched |

## 4. Device Integration Gateway (Shared Infrastructure)

| Feature | Source Capabilities | Status |
|---|---|---|
| `hl7-integration-engine` | Device Integration | Researched |
| `astm-integration` | Device Integration | Researched |
| `device-protocol-adapters` | Analyzer Operations | Researched |
| `message-broker-queueing` | Device Integration (idempotency) | Researched |

## 5. Notification Service (Shared Infrastructure)

| Feature | Source Capabilities | Status |
|---|---|---|
| `multi-channel-notification-engine` | Notifications | Researched |
| `templating` | Notifications, Reminders | Researched |
| `delivery-tracking` | Notifications | Researched |
| `whatsapp-integration` | Notifications (Egypt-relevant, Wave 11) | Researched |

## 6. AI Operations Gateway (Shared Infrastructure)

| Feature | Source Capabilities | Status |
|---|---|---|
| `llm-gateway-orchestration` | AI | Researched |
| `prompt-audit-logging` | AI ↔ Audit | Researched |
| `ai-use-case-governance` | AI (Constitution Section 28) | Researched |
| `semantic-search` | Search | Researched |

## 7. Analytics (Cross-Cutting Service)

| Feature | Source Capabilities | Status |
|---|---|---|
| `bi-dashboards` | BI | Researched |
| `embedded-analytics` | Analytics, Reporting (enterprise) | Researched |
| `reporting-engine` | Reporting (enterprise) | Researched |
| `forecasting-engine` | Forecasting | Researched |

## 8. Document Management (Cross-Cutting Service)

| Feature | Source Capabilities | Status |
|---|---|---|
| `document-storage-versioning` | Document Control | Researched |
| `document-control-workflow` | Document Control | Researched |
| `e-signature` | (Inferred — Sensitive Operation adjacent) | Researched |

## 9. Patient Management (Business Module — Clinical)

| Feature | Source Capabilities | Status |
|---|---|---|
| `patient-registry-mpi` | Patient Identity | Researched |
| `patient-history-timeline` | Patient History | Researched |
| `patient-portal-ui` | (Confirmed — Portal routing) | Researched |
| `consent-linkage` | Consent ↔ Patient | Researched |

## 10. Practitioner and Clinic Management (Business Module — Clinical)

| Feature | Source Capabilities | Status |
|---|---|---|
| `practitioner-registry-credentialing` | Practitioner Management | Researched |
| `clinic-facility-directory` | (derived — Org/Branch ↔ Practitioner) | Researched |
| `referral-management` | Referrals | Researched |

## 11. Scheduling and Encounters (Business Module — Clinical)

| Feature | Source Capabilities | Status |
|---|---|---|
| `appointment-scheduling-engine` | Scheduling | Researched |
| `resource-calendar` | Scheduling | Researched |
| `encounter-tracking` | Clinical Relationship | Researched |
| `reminders-integration` | Reminders ↔ Notification | Researched |

## 12. Diagnostic Ordering (Business Module — Clinical, Core-adjacent)

| Feature | Source Capabilities | Status |
|---|---|---|
| `order-entry-cpoe` | Orders | Researched |
| `order-catalog-pricing` | Orders ↔ Pricing | Researched |
| `order-status-tracking` | Orders | Researched |

## 13. Specimen Operations (Business Module — Clinical, Core)

| Feature | Source Capabilities | Status |
|---|---|---|
| `specimen-accessioning` | Samples | Researched |
| `barcode-labeling` | Samples (derived) | Researched |
| `chain-of-custody` | Samples, Outsourced Tests | Researched |
| `home-collection-logistics` | Home Visits | Researched (architecturally unblocked 2026-07-18; Build-vs-Buy classification pending implementation-level micro-assessment — see `10-final-decision.md`) |

## 14. Laboratory Execution (Business Module — Core)

| Feature | Source Capabilities | Status |
|---|---|---|
| `worklist-management` | Worklists, Benches | Researched |
| `analyzer-middleware-integration` | Analyzer Operations | Researched |
| `quality-control-tracking` | Quality Control | Researched |
| `calibration-tracking` | Calibration | Researched |

## 15. Result Verification and Reporting (Business Module — **Core Domain**)

| Feature | Source Capabilities | Status |
|---|---|---|
| `result-review-verification-workflow` | Result Verification | Researched |
| `clinical-report-generation` | Reporting (clinical) | Researched |
| `critical-result-escalation` | Critical Results | Researched |
| `result-amendment-workflow` | Result Amendments | Researched |

## 16. Quality Management (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `capa-management` | (derived — Complaints → CAPA link) | Researched |
| `complaint-management` | Complaints | Researched |
| `nonconformance-tracking` | Exceptions | Researched |
| `accreditation-tracking` | Quality Control (compliance) | Researched |

## 17. Asset and Maintenance (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `asset-registry` | Asset Registry | Researched |
| `preventive-maintenance-scheduling` | Maintenance, Downtime | Researched |
| `calibration-management` | Calibration (asset-level) | Researched |
| `spare-parts-tracking` | Spare Parts, Service Contracts | Researched (tentative, pending Module 18 reconciliation) |

## 18. Inventory (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `stock-management` | Inventory, Receiving, Stock Transfers | Researched |
| `warehouse-management` | Warehousing | Researched |
| `expiry-batch-tracking` | Expiry, Waste | Researched |
| `barcode-scanning` | (derived — Reagents/Consumption) | Researched |
| `cold-chain-tracking` | Cold Chain (Egypt-relevant, Wave 11) | Researched |

## 19. Procurement (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `purchase-requisition-order` | Procurement | Researched |
| `supplier-rfq` | Procurement (derived) | Researched |
| `receiving-goods` | Receiving ↔ Procurement | Researched |

## 20. Supplier Management (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `supplier-registry-evaluation` | Supplier Management | Researched |
| `contract-management` | Service Contracts (derived) | Researched |

## 21. Billing (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `invoicing-engine` | Billing | Researched |
| `pricing-price-lists` | Pricing | Researched |
| `collections-dunning` | Collections | Researched |

## 22. Payments and Treasury (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `payment-gateway-abstraction` | Payments | Researched |
| `cashbox-treasury-management` | Treasury | Researched |
| `refund-processing` | Refunds | Researched |

## 23. Insurance and Corporate Contracts (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `eligibility-verification` | Insurance | Researched |
| `claims-management` | Insurance | Researched |
| `corporate-contract-rates` | Corporate Contracts | Researched |

## 24. Accounting (Business Module, Integration-leaning per Wave 3)

| Feature | Source Capabilities | Status |
|---|---|---|
| `general-ledger` | Accounting, Costing | Researched |
| `expense-tracking` | Expenses | Researched |
| `external-erp-integration` | (the Native/Integration/Deferred boundary itself) | Researched — resolves to Integration (ERPNext) |

## 25. Workforce Management (Business Module — Generic)

| Feature | Source Capabilities | Status |
|---|---|---|
| `employee-records-hr` | HR (Employee Records) | Researched |
| `attendance-time-tracking` | Attendance | Researched |
| `staff-scheduling-shifts` | Scheduling (staff) | Researched |
| `training-competency` | Training, Competency, Credentials, Performance | Researched |

## 26. Payroll (Business Module — Generic, high sensitivity)

| Feature | Source Capabilities | Status |
|---|---|---|
| `payroll-calculation-engine` | Payroll | Researched |
| `payroll-approval-dual-control` | Payroll (Sensitive-Operation-grade, Wave 6) | Researched |

## 27. CRM and Support (Business Module — Generic)

| Feature | Source Capabilities | Status |
|---|---|---|
| `helpdesk-ticketing` | Support | Researched |
| `call-center-crm` | CRM, Call Center | Researched |
| `complaint-feedback-management` | Complaints, Feedback | Researched |
| `campaign-management` | Campaigns, Retention | Researched |

## 28. SaaS Commercial Operations (Commercial Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `subscription-plan-management` | Plans, Subscriptions | Researched |
| `usage-metering-entitlements` | Entitlements, Metering, Usage | Researched |
| `white-label-branding` | White Label | Researched |
| `saas-billing` | SaaS Billing | Researched |

**All 28 Modules / 106 Features researched — program complete.**

## Out-of-Scope-for-Now (Wave 10's "Optional Add-ons")

Predictive Maintenance, advanced BI/Forecasting beyond basic Analytics,
Marketplace Readiness/Partner Management — not yet justified by real
demand per Wave 10; not researched in this program's first pass. Carried
here so they are not lost, not because they are committed.

## Program Execution Note

Given the true scope (28 modules × 106 features × 13 files = ~1,378
individual documents, each requiring genuine live research), this program
executed as a **multi-session Module-by-module marathon**, identical in
discipline to the preceding Discovery Gap Closure's Wave structure: one
Module fully researched and committed at a time, in priority order (see
`MASTER_EXECUTIVE_SUMMARY.md` for the priority rationale), continuing
across sessions until the Stop Conditions were met.

**Status update (Enterprise Architecture Certification Audit, 2026-07-18):**
all 106/106 Features are now `Researched` (105 fully decided, 1 —
`home-collection-logistics` — researched, at that time explicitly
blocked, see its own `10-final-decision.md`), matching
`MASTER_COMPLETION_REPORT.md` and `MASTER_DECISION_REGISTER.md`.

**Further update (Pre-SAD Baseline Correction, 2026-07-18, same day):**
`home-collection-logistics`'s architectural blocker (`open-questions.md`
#6, Offline Mode) is now resolved — 106/106 Features have 0 architectural
blockers. Its Build-vs-Buy classification remains pending a scoped,
implementation-level micro-assessment, distinct from an architectural
open question. See `docs/certification/25-PRE-SAD-CLEAN-CLOSURE.md`.

This catalog's Status column previously lagged 44 Features behind
actual completion (a stale-index defect found and corrected during the
Certification Audit — see `docs/certification/09-SAFE-FIXES-APPLIED.md`);
it is now the accurate single source of truth for what remains.
