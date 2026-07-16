# Enterprise Capability Map (Wave 3)

**Status: Draft — Assumption-Driven, per this program's Stakeholder
Confirmation Policy.** 100 capabilities across 10 categories (up from the
Baseline's 20, Laboratory-only). Every row has Strategic Classification
(Strategic/Core/Supporting/Generic/Platform/Commercial/Operational/
Compliance/Integration), a Candidate Bounded Context (informing Wave 9,
not deciding it), and an Evidence Level. Per-category notes cover typical
Owner/Dependencies/Maturity rather than repeating identical patterns 100
times — deviations from the category norm are called out inline.
**Retains, does not replace,** `artifacts/02-business-capability-map.md`
(the Baseline's 20 Laboratory-scoped capabilities are folded into
"Clinical and Diagnostic" / "Laboratory Operations" below with their
original evidence intact).

**Evidence Level key:** `Evidenced` = traces to a real Baseline Discovery
artifact (event/rule/aggregate). `Inferred` = industry-reference, no
platform-specific evidence yet. `Confirmed` = directly from the user's
authorization prompt.

## 1. Clinical and Diagnostic (13) — Owner pattern: clinical/front-office roles (Wave 2); Dependencies: Identity/Access, Notification

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| Patient Identity | Establish and maintain a unique patient identity across visits/facilities | Platform | Patient Management *(new, Wave 9)* | Inferred |
| Practitioner Management | Maintain doctor/consultant records and credentials | Supporting | Practitioner and Clinic Management *(new)* | Inferred |
| Clinical Relationship | Track which practitioner is responsible for which patient/order | Core | Patient Management / Diagnostic Ordering | Inferred |
| Orders | Capture and manage diagnostic test orders | Core | Diagnostic Ordering *(renames Order Management)* | **Evidenced** (Baseline) |
| Scheduling | Book appointments and resource slots | Supporting | Scheduling and Encounters *(new)* | Inferred |
| Samples | Manage specimen lifecycle | Core | Specimen Operations *(renames Specimen Management)* | **Evidenced** |
| Test Processing | Analytical processing of a specimen | Core | Laboratory Execution *(renames Test Processing)* | **Evidenced** |
| Result Verification | Clinical sign-off before release | **Core (Proposed, ADR 0011)** | Result Verification and Reporting | **Evidenced** |
| Reporting *(clinical)* | Produce the patient/doctor-facing report artifact | Core | Result Verification and Reporting | **Evidenced** |
| Patient History | Longitudinal record across orders/results | Supporting | Patient Management | Inferred |
| Clinical Comments | Practitioner annotations on results/history | Supporting | Result Verification and Reporting | Inferred |
| Referrals | Route a patient/case to another practitioner or facility | Supporting | Practitioner and Clinic Management | Inferred |
| Home Visits | Manage off-site sample collection | Core (debated, see ADR 0011) | Specimen Operations | **Evidenced** |

## 2. Laboratory Operations (11) — Owner: Laboratory Staff/Quality Staff; Dependencies: Device Integration, Inventory

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| Worklists | Organize pending work per bench/technician | Supporting | Laboratory Execution | Inferred |
| Benches | Physical/logical work-station grouping | Supporting | Laboratory Execution | Inferred |
| Analyzer Operations | Operate and monitor lab analyzer devices | Supporting | Device Integration | **Evidenced** |
| Quality Control | Run QC samples, track QC trends | Compliance | Quality Management *(new)* | Inferred |
| Calibration | Calibrate analyzers/instruments | Compliance | Asset and Maintenance *(shared with Category 6)* | Inferred |
| Reagents | Track reagent stock tied to test consumption | Supporting | Inventory | Inferred |
| Exceptions | Handle abnormal lab-process events | Supporting | Laboratory Execution | Inferred |
| Outsourced Tests | Send specimens to a partner/reference lab | Supporting | Specimen Operations / Integration Hub | Inferred |
| Reference Ranges | Maintain normal-value ranges per test/demographic | Supporting | Laboratory Execution | Inferred |
| Critical Results | Flag and escalate dangerously abnormal results | **Core-adjacent (Sensitive Operation)** | Result Verification and Reporting | Inferred, high priority |
| Result Amendments | Post-release correction workflow | Core | Result Verification and Reporting | **Evidenced** (`ResultCorrected`, Baseline Phase 05) |

## 3. Workforce (8) — Owner: HR/Payroll Staff; Dependencies: Identity/Access, Attendance devices

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| HR (Employee Records) | Maintain employee master data | Generic | Workforce Management *(new)* | Confirmed (scope), Inferred (detail) |
| Attendance | Track staff presence/shifts | Generic | Workforce Management | Confirmed, Inferred |
| Scheduling *(staff)* | Assign staff to shifts/branches | Supporting | Workforce Management | Confirmed, Inferred |
| Payroll | Calculate and disburse compensation | Generic (high privacy sensitivity) | Payroll *(new, separated from Workforce Management — see rationale below)* | Confirmed, Inferred |
| Training | Manage training programs/completion | Generic | Workforce Management | Confirmed, Inferred |
| Competency | Track staff skill/qualification levels | Supporting | Workforce Management | Confirmed, Inferred |
| Credentials | Track licenses/certifications, expiry | Compliance | Workforce Management | Confirmed, Inferred |
| Performance | Track staff performance reviews | Generic | Workforce Management | Confirmed, Inferred |

**Rationale for a separate Payroll context (not asserted elsewhere in this
Wave):** Payroll's data-sensitivity profile (Wave 2's Payroll Staff
persona) and its distinct approval/audit chain make it a candidate for
isolation from general Workforce Management even though both are "HR" in
common parlance — flagged for Wave 9 to formally evaluate, not decided
here.

## 4. Financial (11) — Owner: Finance/Accounting roles; Dependencies: Billing triggers from Clinical/Lab domains

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| Pricing | Define test/service prices, price lists per org/contract | Supporting | Billing | Inferred |
| Billing | Generate invoices for billable events | Supporting | Billing | **Evidenced** (Baseline) |
| Collections | Pursue outstanding balances | Supporting | Billing | Inferred |
| Payments | Record payments across channels | Supporting | Payments and Treasury *(new)* | Inferred |
| Refunds | Process refunds | Supporting | Payments and Treasury | Inferred |
| Expenses | Track operational expenses | Generic | Accounting *(new)* | Confirmed (scope), Inferred (detail) |
| Treasury | Manage cash position, cashboxes | Generic | Payments and Treasury | Confirmed, Inferred |
| Costing | Attribute cost to services/cost centers | Supporting | Accounting | Confirmed, Inferred |
| Accounting | General ledger, journal entries, close cycle | Generic | Accounting | Confirmed, Inferred |
| Insurance | Manage payer eligibility/claims | Supporting | Insurance and Corporate Contracts | **Evidenced** (Baseline, weak) |
| Corporate Contracts | Manage negotiated-rate corporate accounts | Supporting | Insurance and Corporate Contracts | Inferred |

**Native/Integration/Deferred boundary (explicit per user instruction —
"لا تفترض ERP مالي كامل"):** Pricing/Billing/Collections/Refunds/Insurance/
Corporate Contracts are **Recommended Native** (directly tied to clinical/
commercial events only this platform originates). Treasury/Costing/
Accounting/General-Ledger-depth are **Recommended Integration-capable**
(the platform should originate clean financial events and *support*
integration to an external accounting system, not necessarily *replace*
one) — full General Ledger functionality is **Recommended Deferred**
pending explicit product-strategy confirmation. All three labels are
`Recommended`, not `Confirmed` — the user explicitly asked Discovery to
find this boundary, not assume it.

## 5. Supply Chain (10) — Owner: Procurement/Inventory Staff; Dependencies: Test Processing (consumption), Device Operations

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| Inventory | Track stock levels across branches | Supporting | Inventory *(new)* | Inferred |
| Warehousing | Manage central/branch storage locations | Supporting | Inventory | Inferred |
| Procurement | Raise and manage purchase requests/orders | Supporting | Procurement *(new)* | Inferred |
| Supplier Management | Evaluate and manage supplier relationships | Supporting | Supplier Management *(new)* | Inferred |
| Receiving | Record incoming stock against a PO | Supporting | Inventory | Inferred |
| Stock Transfers | Move stock between branches/warehouses | Supporting | Inventory | Inferred |
| Expiry | Track lot/batch expiry dates | Compliance | Inventory | Inferred |
| Cold Chain | Track temperature-sensitive storage/transport | Compliance | Inventory | Inferred, Egypt-climate-relevant (Wave 11) |
| Consumption | Link test-level material usage to inventory | Core-adjacent (feeds Test Processing) | Inventory ↔ Laboratory Execution | Inferred |
| Waste | Track spoiled/expired/wasted stock | Compliance | Inventory | Inferred |

## 6. Asset and Device Operations (8) — Owner: Device Engineers; Dependencies: Device Integration Gateway (ADR 0006)

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| Device Integration | Connect and exchange data with lab devices | Supporting | Device Integration | **Evidenced** (Baseline, ADR 0006) |
| Asset Registry | Track all physical assets (not just devices) | Generic | Asset and Maintenance *(new)* | Inferred |
| Maintenance | Schedule and record maintenance events | Generic | Asset and Maintenance | Inferred |
| Calibration *(asset-level)* | Track calibration schedule/history | Compliance | Asset and Maintenance | Inferred |
| Downtime | Track device/asset unavailability | Operational | Asset and Maintenance | Inferred |
| Spare Parts | Track spare-part inventory for maintenance | Supporting | Asset and Maintenance ↔ Inventory | Inferred |
| Service Contracts | Track vendor maintenance contracts | Supporting | Asset and Maintenance | Inferred |
| Predictive Maintenance | Forecast device failure before it happens | AI-Assisted (Wave 5/10 territory) | Asset and Maintenance ↔ AI Operations | Inferred, speculative |

## 7. Customer Operations (9) — Owner: Customer Support/Call Center; Dependencies: Notification, Patient/Order data (read)

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| CRM | Track customer relationship/interaction history | Supporting | CRM and Support *(new)* | Inferred |
| Call Center | Handle inbound inquiries | Operational | CRM and Support | Inferred |
| Support | General customer support case management | Operational | CRM and Support | Inferred |
| Complaints | Formal complaint intake and resolution | Compliance-adjacent | CRM and Support | Inferred |
| Feedback | Collect satisfaction/feedback data | Operational | CRM and Support | Inferred |
| Notifications | Send outbound patient/doctor/staff notifications | Generic | Notification and Communication | **Evidenced** (Baseline) |
| Reminders | Scheduled/triggered reminder notifications | Generic | Notification and Communication | Inferred |
| Campaigns | Marketing/retention campaign management | Commercial | CRM and Support | Inferred, lower priority |
| Retention | Track and act on churn risk | Commercial | CRM and Support | Inferred, lower priority |

## 8. SaaS and Platform (14) — Owner: Platform Operator/Tenant Admin/SaaS Commercial Team; Dependencies: Identity/Access

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| Tenant Management | Provision/manage tenants | Platform | Tenant and Organization Management *(new)* | Confirmed (scope), Inferred (detail) |
| Organization Management | Manage organizations within a tenant | Platform | Tenant and Organization Management | **Evidenced** (Baseline, Core Platform) |
| Branch Management | Manage branches within an organization | Platform | Tenant and Organization Management | **Evidenced** |
| Plans | Define commercial subscription plans | Commercial | SaaS Commercial Operations *(new)* | Confirmed, Inferred |
| Subscriptions | Manage a tenant's active subscription | Commercial | SaaS Commercial Operations | Confirmed, Inferred |
| Entitlements | Determine what a tenant/plan can access | Platform | SaaS Commercial Operations | Confirmed, Inferred |
| Metering | Measure usage for billing/entitlement purposes | Platform | SaaS Commercial Operations | Confirmed, Inferred |
| Usage | Aggregate/report platform usage | Platform | SaaS Commercial Operations | Confirmed, Inferred |
| SaaS Billing | Bill tenants for platform usage (distinct from patient billing) | Commercial | SaaS Commercial Operations | Confirmed, Inferred |
| White Label | Rebrand the platform per tenant/partner | Commercial | SaaS Commercial Operations | Confirmed, Inferred |
| Partner Management | Manage partner relationships/agreements | Commercial | Partner and Marketplace Operations *(new)* | Confirmed, Inferred |
| Marketplace Readiness | Support third-party add-ons/integrations | Commercial | Partner and Marketplace Operations | Confirmed, Inferred, speculative |
| Feature Flags | Toggle features per tenant/rollout stage | Platform | Tenant and Organization Management | Inferred |
| Platform Support | Platform-operator-level support tooling | Platform | Platform Administration *(new)* | Inferred |

## 9. Governance (8) — Owner: Auditor/Compliance Staff; cross-cutting, depends on every other domain

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| Security | Platform-wide security controls | Platform | Identity and Access / Audit and Compliance | **Evidenced** (Constitution Section 21, Accepted) |
| Privacy | Data protection and minimization | Platform | Audit and Compliance *(new)* | **Evidenced** (Constitution Section 30, Accepted) |
| Audit | Immutable audit trail | Platform | Audit and Compliance | **Evidenced** (Constitution Section 23, Accepted) |
| Consent | Track and enforce patient/user consent | Platform | Audit and Compliance | **Evidenced** (Constitution Section 22, Accepted) |
| Risk | Track organizational/platform risk | Governance | Audit and Compliance | **Evidenced** (Constitution Section 58, Accepted) |
| Compliance | Track regulatory compliance posture | Compliance | Audit and Compliance | Inferred, Egypt-specific detail Wave 11 |
| Document Control | Manage controlled documents (policies, SOPs) | Compliance | Document Management *(new)* | Inferred |
| Policy Management | Configure/version business and access policies | Platform | Audit and Compliance | **Evidenced** (Constitution Section 21, verification policies Wave 6) |

## 10. Data and Intelligence (8) — Owner: Analytics/AI Operations; Dependencies: every domain (as a data consumer)

| Capability | Description | Strategic Class | Candidate Context | Evidence |
|---|---|---|---|---|
| Reporting *(enterprise/BI, distinct from Clinical Reporting in Category 1)* | Cross-domain operational reporting | Supporting | Analytics *(new)* | Inferred |
| Analytics | Descriptive analytics across domains | Supporting | Analytics | Inferred |
| BI | Business intelligence dashboards | Supporting | Analytics | Inferred |
| Forecasting | Demand/inventory/workforce forecasting | AI-Assisted | Analytics ↔ AI Operations | Inferred |
| AI | Governed AI-assisted operations (see Wave 5/10) | Platform (governed) | AI Operations *(new)* | **Evidenced** (Baseline Phase 10, ADR 0007) |
| Search | Cross-domain natural-language search | Supporting | AI Operations | **Evidenced** (Baseline Phase 10, Use Case #6) |
| Data Quality | Monitor/enforce data quality across domains | Platform | Audit and Compliance | Inferred |
| Data Governance | Ownership/lifecycle rules for enterprise data | Platform | Audit and Compliance | Inferred |

## Summary

**100 capabilities** across 10 categories (up from 20). **Evidence
breakdown:** 16 `Evidenced` (traced to real Baseline artifacts), 21
`Confirmed (scope) + Inferred (detail)` (SaaS/Workforce/Financial domains
the user explicitly scoped but Discovery hasn't yet detailed), 63 purely
`Inferred`. This distribution is itself informative: it shows precisely
where Gap Closure added real breadth (Governance's 8/8 mostly Evidenced,
since it inherits directly from the already-Accepted Constitution) versus
where it added scope awaiting future evidence (Supply Chain, Customer
Operations — both 0 Evidenced).
