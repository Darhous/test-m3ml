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
| `tenant-provisioning` | Tenant Management | Pending |
| `organization-branch-hierarchy` | Organization Management, Branch Management | Pending |
| `multi-tenancy-isolation` | (Constitution Section 18/19, ADR 0005) | Pending |
| `feature-flags` | Feature Flags | Pending |
| `tenant-configuration` | Tenant Management | Pending |

## 3. Audit and Compliance (Platform Kernel)

| Feature | Source Capabilities | Status |
|---|---|---|
| `immutable-audit-trail` | Audit | Pending |
| `consent-management` | Consent | Pending |
| `policy-engine` | Policy Management | Pending |
| `compliance-tracking` | Compliance, Risk | Pending |
| `document-control` | Document Control | Pending |

## 4. Device Integration Gateway (Shared Infrastructure)

| Feature | Source Capabilities | Status |
|---|---|---|
| `hl7-integration-engine` | Device Integration | Pending |
| `astm-integration` | Device Integration | Pending |
| `device-protocol-adapters` | Analyzer Operations | Pending |
| `message-broker-queueing` | Device Integration (idempotency) | Pending |

## 5. Notification Service (Shared Infrastructure)

| Feature | Source Capabilities | Status |
|---|---|---|
| `multi-channel-notification-engine` | Notifications | Pending |
| `templating` | Notifications, Reminders | Pending |
| `delivery-tracking` | Notifications | Pending |
| `whatsapp-integration` | Notifications (Egypt-relevant, Wave 11) | Pending |

## 6. AI Operations Gateway (Shared Infrastructure)

| Feature | Source Capabilities | Status |
|---|---|---|
| `llm-gateway-orchestration` | AI | Pending |
| `prompt-audit-logging` | AI ↔ Audit | Pending |
| `ai-use-case-governance` | AI (Constitution Section 28) | Pending |
| `semantic-search` | Search | Pending |

## 7. Analytics (Cross-Cutting Service)

| Feature | Source Capabilities | Status |
|---|---|---|
| `bi-dashboards` | BI | Pending |
| `embedded-analytics` | Analytics, Reporting (enterprise) | Pending |
| `reporting-engine` | Reporting (enterprise) | Pending |
| `forecasting-engine` | Forecasting | Pending |

## 8. Document Management (Cross-Cutting Service)

| Feature | Source Capabilities | Status |
|---|---|---|
| `document-storage-versioning` | Document Control | Pending |
| `document-control-workflow` | Document Control | Pending |
| `e-signature` | (Inferred — Sensitive Operation adjacent) | Pending |

## 9. Patient Management (Business Module — Clinical)

| Feature | Source Capabilities | Status |
|---|---|---|
| `patient-registry-mpi` | Patient Identity | Pending |
| `patient-history-timeline` | Patient History | Pending |
| `patient-portal-ui` | (Confirmed — Portal routing) | Pending |
| `consent-linkage` | Consent ↔ Patient | Pending |

## 10. Practitioner and Clinic Management (Business Module — Clinical)

| Feature | Source Capabilities | Status |
|---|---|---|
| `practitioner-registry-credentialing` | Practitioner Management | Pending |
| `clinic-facility-directory` | (derived — Org/Branch ↔ Practitioner) | Pending |
| `referral-management` | Referrals | Pending |

## 11. Scheduling and Encounters (Business Module — Clinical)

| Feature | Source Capabilities | Status |
|---|---|---|
| `appointment-scheduling-engine` | Scheduling | Pending |
| `resource-calendar` | Scheduling | Pending |
| `encounter-tracking` | Clinical Relationship | Pending |
| `reminders-integration` | Reminders ↔ Notification | Pending |

## 12. Diagnostic Ordering (Business Module — Clinical, Core-adjacent)

| Feature | Source Capabilities | Status |
|---|---|---|
| `order-entry-cpoe` | Orders | Pending |
| `order-catalog-pricing` | Orders ↔ Pricing | Pending |
| `order-status-tracking` | Orders | Pending |

## 13. Specimen Operations (Business Module — Clinical, Core)

| Feature | Source Capabilities | Status |
|---|---|---|
| `specimen-accessioning` | Samples | Researched |
| `barcode-labeling` | Samples (derived) | Researched |
| `chain-of-custody` | Samples, Outsourced Tests | Researched |
| `home-collection-logistics` | Home Visits | Researched (blocked — see `10-final-decision.md`) |

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
| `supplier-registry-evaluation` | Supplier Management | Pending |
| `contract-management` | Service Contracts (derived) | Pending |

## 21. Billing (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `invoicing-engine` | Billing | Pending |
| `pricing-price-lists` | Pricing | Pending |
| `collections-dunning` | Collections | Pending |

## 22. Payments and Treasury (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `payment-gateway-abstraction` | Payments | Pending |
| `cashbox-treasury-management` | Treasury | Pending |
| `refund-processing` | Refunds | Pending |

## 23. Insurance and Corporate Contracts (Business Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `eligibility-verification` | Insurance | Pending |
| `claims-management` | Insurance | Pending |
| `corporate-contract-rates` | Corporate Contracts | Pending |

## 24. Accounting (Business Module, Integration-leaning per Wave 3)

| Feature | Source Capabilities | Status |
|---|---|---|
| `general-ledger` | Accounting, Costing | Pending |
| `expense-tracking` | Expenses | Pending |
| `external-erp-integration` | (the Native/Integration/Deferred boundary itself) | Pending |

## 25. Workforce Management (Business Module — Generic)

| Feature | Source Capabilities | Status |
|---|---|---|
| `employee-records-hr` | HR (Employee Records) | Pending |
| `attendance-time-tracking` | Attendance | Pending |
| `staff-scheduling-shifts` | Scheduling (staff) | Pending |
| `training-competency` | Training, Competency, Credentials, Performance | Pending |

## 26. Payroll (Business Module — Generic, high sensitivity)

| Feature | Source Capabilities | Status |
|---|---|---|
| `payroll-calculation-engine` | Payroll | Pending |
| `payroll-approval-dual-control` | Payroll (Sensitive-Operation-grade, Wave 6) | Pending |

## 27. CRM and Support (Business Module — Generic)

| Feature | Source Capabilities | Status |
|---|---|---|
| `helpdesk-ticketing` | Support | Pending |
| `call-center-crm` | CRM, Call Center | Pending |
| `complaint-feedback-management` | Complaints, Feedback | Pending |
| `campaign-management` | Campaigns, Retention | Pending |

## 28. SaaS Commercial Operations (Commercial Module)

| Feature | Source Capabilities | Status |
|---|---|---|
| `subscription-plan-management` | Plans, Subscriptions | Pending |
| `usage-metering-entitlements` | Entitlements, Metering, Usage | Pending |
| `white-label-branding` | White Label | Pending |
| `saas-billing` | SaaS Billing | Pending |

## Out-of-Scope-for-Now (Wave 10's "Optional Add-ons")

Predictive Maintenance, advanced BI/Forecasting beyond basic Analytics,
Marketplace Readiness/Partner Management — not yet justified by real
demand per Wave 10; not researched in this program's first pass. Carried
here so they are not lost, not because they are committed.

## Program Execution Note

Given the true scope (28 modules × 106 features × 13 files = ~1,378
individual documents, each requiring genuine live research), this program
executes as a **multi-session Module-by-module marathon**, identical in
discipline to the preceding Discovery Gap Closure's Wave structure: one
Module fully researched and committed at a time, in priority order (see
`MASTER_EXECUTIVE_SUMMARY.md` for the priority rationale), continuing
across sessions until the Stop Conditions are met. This catalog is the
single source of truth for what remains — `Pending` rows are the honest,
un-hidden backlog, not a silently-dropped scope.
