# Expanded Value Streams and Customer Journeys (Wave 4)

**Status: Draft — Inferred unless noted.** Retains the Baseline's 4 Value
Streams (VS1–VS4, `artifacts/02-value-streams.md`) unchanged and adds 16
new enterprise-wide streams, reaching the user's 20 named streams (2 of
the user's names map directly onto already-documented Baseline streams,
noted below rather than duplicated).

## Retained from Baseline (cross-referenced, not redone)

| User's Name | Maps To | Note |
|---|---|---|
| Patient-to-Result | VS1 + VS2 + VS3 (combined umbrella) | The Baseline already traced this at finer granularity (3 separate streams for walk-in/home/rejection); retained as-is, not collapsed. |
| Home-Visit-Request-to-Sample-Delivery | VS2 | Direct match, already fully traced. |

## New Value Streams (16)

| # | Value Stream | Trigger | Outcome | Key Actors | Domains Involved | Bottleneck/Risk |
|---|---|---|---|---|---|---|
| 1 | Doctor-to-Diagnosis-Support | Doctor requests clinical decision support on a case | Doctor receives AI-assisted, human-verified insight | Doctor, Result Verifier, AI Operations | Clinical, AI Operations | AI Gateway must never bypass human review (ADR 0007) |
| 2 | Order-to-Cash | A billable clinical event occurs | Payment collected, revenue recognized | Finance Manager, Cashier, Patient | Clinical, Financial | Weakest-evidenced domain (Billing, Baseline VS4) |
| 3 | Lead-to-Customer | A prospective corporate/individual customer is identified | Customer onboarded with active contract | SaaS Commercial Team, Corporate Client | CRM and Support, SaaS Commercial | No CRM capability existed before Wave 3 |
| 4 | Contract-to-Revenue | A corporate/insurance contract is signed | Contract-linked billing flows correctly | Finance Manager, Corporate Client, Insurance User | Insurance and Corporate Contracts, Financial | Contract-specific pricing rules undesigned (Wave 6) |
| 5 | Request-to-Procure | Inventory falls below threshold or a need is identified | A purchase request is raised and approved | Inventory Staff, Procurement Staff | Inventory, Procurement | Threshold/reorder-point policy undesigned |
| 6 | Purchase-to-Pay | A purchase order is issued | Supplier is paid for delivered goods | Procurement Staff, Accountant, Supplier | Procurement, Accounting | Native-vs-Integration boundary (Wave 3) affects how far this streams natively |
| 7 | Stock-to-Consumption | Stock is received | Stock is consumed by a test/procedure and depleted correctly | Inventory Staff, Laboratory Staff | Inventory, Laboratory Execution | Test-level consumption linkage undesigned |
| 8 | Hire-to-Retire | A candidate is hired | Employee lifecycle fully managed through offboarding | HR Staff, Employee | Workforce Management | Entirely new domain — 0 Evidenced capabilities (Wave 3) |
| 9 | Time-to-Payroll | Attendance/time data is captured | Payroll is accurately calculated and disbursed | Payroll Staff, Employee | Attendance, Payroll | Highest privacy sensitivity of any stream (Wave 2 finding) |
| 10 | Incident-to-Resolution | An operational incident is reported (not a patient complaint) | Incident resolved, root cause tracked | Support Operations, Platform Operator | CRM and Support, Platform Administration | No incident taxonomy exists yet |
| 11 | Device-to-Maintenance | A device shows a fault or reaches a maintenance interval | Device restored to service, downtime tracked | Device Engineer, Asset/Maintenance | Device Integration, Asset and Maintenance | Predictive-maintenance AI use case is speculative (Wave 3, Category 6) |
| 12 | Complaint-to-Closure | A patient/customer complaint is lodged | Complaint resolved and closed with an audit trail | Customer Support, Quality Staff | CRM and Support, Quality Management | Overlaps Quality's CAPA process (#19) — relationship undesigned |
| 13 | Subscription-to-Renewal | A tenant's subscription approaches renewal | Subscription renewed or churned with reason tracked | SaaS Commercial Team, Tenant Administrator | SaaS Commercial Operations | No entitlement/usage metering mechanism chosen (Wave 1, deferred to SAD) |
| 14 | Tenant-to-Go-Live | A new tenant contract is signed | Tenant is fully provisioned and operational | Platform Operator, Tenant Administrator | Tenant and Organization Management | This is the stream Wave 1's "Success Outcome #1" example described |
| 15 | Partner-to-Integration | A partner agreement is signed | Partner's API integration is live and stable | Partner, Integration Engineer | Partner and Marketplace Operations, Integration Hub | Builds on the already-Evidenced Insurance/Payer ACL pattern (Baseline Phase 08) |
| 16 | Data-to-Insight | Operational data accumulates across domains | A decision-maker receives an actionable report/dashboard | Finance Manager, Laboratory Management, Analytics | Analytics, every source domain | Cross-domain data model doesn't exist yet (depends on Wave 9) |
| 17 | AI-Request-to-Human-Approved-Outcome | Any AI Gateway request is made | A human-approved outcome is reached (or the request is safely rejected) | Any persona interacting with AI, Result Verifier / relevant approver | AI Operations, requesting domain | This is the *generalized* form of the Baseline's Pattern A (Phase 10) — applies platform-wide, not just to results |
| 18 | Quality-Issue-to-CAPA | A quality non-conformance is identified | Corrective and Preventive Action (CAPA) is completed and closed | Quality Staff, Medical Director | Quality Management | Entirely new domain — CAPA methodology not previously modeled anywhere |

**Count check:** 2 retained (mapped) + 18 new = 20, matching the user's
list exactly (the user listed 20 names; two map onto already-traced
Baseline streams as shown above, so 18 required genuinely new tracing,
listed as #1–18 above).

## Cross-Cutting Finding

**7 of the 18 new streams (#3, #8, #9, #10, #13, #16, #18) touch domains
with zero prior Evidenced capabilities** (CRM, Workforce, Analytics,
Quality Management, SaaS Commercial, Platform Administration) — confirming
Wave 3's evidence-distribution finding from an independent angle (value
streams, not capabilities).

## Explicitly Not Traced Further

Detailed step-by-step stage breakdowns (matching VS1–VS4's fuller
treatment) are deferred to Wave 5 (Event Storming), which will storm each
of these 18 streams to the same depth VS1–VS4 received in the Baseline —
tracing every stream to full event-level detail here would duplicate
Wave 5's work.
