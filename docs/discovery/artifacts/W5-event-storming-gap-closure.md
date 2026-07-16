# Event Storming Gap Closure (Wave 5)

**Status: Draft — Inferred — Industry Reference throughout.** Storms the
29 previously-missing/shallow domains from the user's list, grouped into
10 clusters matching Wave 3's capability categories for traceability.
**Retains** the Baseline's 26 Laboratory-Operations events
(`artifacts/03-event-storming-board.md`) unchanged.

## Unified Event Naming Convention (restated, not new — Constitution
Section 6/12/13, already Accepted)

Domain Events: past tense, Ubiquitous Language, no CRUD-style names (e.g.,
`PayrollDisbursed`, not `PayrollUpdated`). Integration Events (crossing
Bounded Context boundaries): `<Context>.<Concept><PastTenseVerb>` — this
Wave lists **Domain Events only**, consistent with the Baseline's own
Phase 03 scope; promoting any of these to Integration Events is Wave 9's
job, once Bounded Contexts are remapped, exactly as the Baseline did
(Phase 03 → Phase 06).

## Cluster A — Finance, Expenses, Treasury, Accounting

| Commands | Domain Events | Failure/Compensation | Policies | Actors |
|---|---|---|---|---|
| Record Expense, Approve Expense, Open/Close Cashbox, Post Journal Entry, Close Period, Reconcile Bank | `ExpenseRecorded`, `ExpenseApproved`, `CashboxOpened`, `CashboxClosed`, `JournalEntryPosted`, `PeriodClosed` | `ExpenseRejected`, `ReconciliationDiscrepancyFound` | Amount-based expense-approval routing (Open — threshold) | Accountant, Finance Manager, Cashier |

## Cluster B — Inventory, Procurement, Suppliers

| Commands | Domain Events | Failure/Compensation | Policies | Actors |
|---|---|---|---|---|
| Request Purchase, Approve Purchase Request, Issue Purchase Order, Receive Goods, Return Goods, Count Stock, Transfer Stock, Evaluate Supplier | `PurchaseRequested`, `PurchaseRequestApproved`, `PurchaseOrderIssued`, `GoodsReceived`, `GoodsReturned`, `StockCounted`, `StockTransferred`, `SupplierEvaluated` | `PurchaseOrderRejected`, `GoodsReceivingDiscrepancyFound`, `StockCountDiscrepancyFound` | Reorder-point trigger policy (Open, Wave 4) | Procurement Staff, Inventory Staff, Store Manager, Supplier *(external, via Partner pattern)* |

## Cluster C — HR, Attendance, Payroll, Training, Competency

| Commands | Domain Events | Failure/Compensation | Policies | Actors |
|---|---|---|---|---|
| Hire/Onboard/Transfer/Offboard Employee, Schedule Shift, Record Attendance, Request/Approve Leave, Calculate/Approve/Disburse Payroll, Complete Training, Assess Competency | `EmployeeHired`, `EmployeeOnboarded`, `EmployeeTransferred`, `EmployeeOffboarded`, `ShiftScheduled`, `AttendanceRecorded`, `LeaveRequested`, `LeaveApproved`, `PayrollCalculated`, `PayrollApproved`, `PayrollDisbursed`, `TrainingCompleted`, `CompetencyAssessed` | `PayrollDisbursementFailed`, `LeaveRequestRejected` | **Payroll requires dual-control approval** (Sensitive — flagged Wave 12, mirrors the Result Verifier Role pattern from Baseline Phase 07) | HR Staff, Payroll Staff, Employee, Manager |
| *(Timer)* Check credential expiry | `CredentialExpiringSoon` | — | Credential-expiry lead-time policy (Open) | System (scheduled) |

## Cluster D — Quality, CAPA, Maintenance, Assets

| Commands | Domain Events | Failure/Compensation | Policies | Actors |
|---|---|---|---|---|
| Identify Non-Conformance, Initiate/Assign/Complete/Verify CAPA, Schedule/Complete Maintenance, Register Asset, Complete Calibration | `NonConformanceIdentified`, `CAPAInitiated`, `CAPAActionAssigned`, `CAPACompleted`, `CAPAVerifiedEffective`, `MaintenanceScheduled`, `MaintenanceCompleted`, `AssetRegistered`, `CalibrationCompleted` | `CAPAOverdue`, `MaintenanceMissed` | CAPA closure-window escalation policy (Open — threshold) | Quality Staff, Medical Director, Device Engineer |
| *(Timer)* Check calibration due date | `CalibrationDue` | — | Calibration interval policy (Open, per-device-type) | System (scheduled) |

## Cluster E — CRM, Support, Complaints, Feedback

| Commands | Domain Events | Failure/Compensation | Policies | Actors |
|---|---|---|---|---|
| Capture Lead, Onboard Customer, Open/Escalate/Close Support Case, Lodge/Investigate/Resolve Complaint | `LeadCaptured`, `CustomerOnboarded`, `SupportCaseOpened`, `SupportCaseEscalated`, `SupportCaseClosed`, `ComplaintLodged`, `ComplaintInvestigated`, `ComplaintResolved`, `FeedbackReceived` | `ComplaintEscalatedToRegulator` *(candidate — ties to the undesigned Regulator persona, Wave 2)* | Complaint-to-CAPA escalation policy (Open — relationship between Cluster E and Cluster D undesigned, per Wave 4's finding) | Call Center Agent, Customer Support, Quality Staff |

## Cluster F — SaaS Subscriptions, Tenant Onboarding

| Commands | Domain Events | Failure/Compensation | Policies | Actors |
|---|---|---|---|---|
| Request/Provision/Configure/Activate Tenant, Start/Renew/Cancel Subscription, Grant Entitlement, Meter Usage, Upgrade/Downgrade Plan | `TenantRequested`, `TenantProvisioned`, `TenantConfigured`, `TenantActivated`, `SubscriptionStarted`, `SubscriptionRenewed`, `SubscriptionCancelled`, `EntitlementGranted`, `UsageMetered`, `PlanUpgraded`, `PlanDowngraded` | `TenantProvisioningFailed`, `SubscriptionPaymentFailed` | Entitlement-enforcement policy (feature flags per plan, Constitution Section 48 Feature Flag Policy already Accepted — applied here) | Platform Operator, Tenant Administrator, SaaS Commercial Team |

## Cluster G — Patient, Doctor, Clinic Operations (as owned domains, not just Actors)

| Commands | Domain Events | Failure/Compensation | Policies | Actors |
|---|---|---|---|---|
| Register/Update Patient, Register Practitioner, Verify Practitioner Credential, Book/Reschedule/Cancel Appointment, Start/Complete Encounter | `PatientRegistered`, `PatientProfileUpdated`, `PractitionerRegistered`, `PractitionerCredentialVerified`, `ClinicalRelationshipEstablished`, `AppointmentBooked`, `AppointmentRescheduled`, `AppointmentCancelled`, `EncounterStarted`, `EncounterCompleted` | `AppointmentNoShow`, `PractitionerCredentialVerificationFailed` | Appointment no-show policy (Open) | Reception, Patient, Doctor, Clinic Administrator |

**Significant finding:** this is the first time "Patient" and "Doctor" are
modeled as **owned domains with their own lifecycle events**, not just
cross-context Actors — directly closing the gap Baseline Risk #7 flagged
("Patient and Doctor have no distinct Bounded Context").

## Cluster H — Insurance, Corporate Contracts

| Commands | Domain Events | Failure/Compensation | Policies | Actors |
|---|---|---|---|---|
| Negotiate/Sign/Activate/Renew/Terminate Contract | `ContractNegotiated`, `ContractSigned`, `ContractActivated`, `ContractRenewed`, `ContractTerminated`, `CorporateInvoiceGenerated` | `ContractRenewalDeclined` | Corporate-rate pricing policy (Open) | Finance Manager, Corporate Client, Insurance User |

*(`EligibilityVerified`/`ClaimSubmitted`/`ClaimAdjudicated`/`ClaimDenied`
already exist from Baseline Phase 03/07 — not repeated here.)*

## Cluster I — Analytics, AI Operations

| Commands | Domain Events | Failure/Compensation | Policies | Actors |
|---|---|---|---|---|
| Generate Report/Forecast, Submit AI Request, Review Model Performance | `ReportGenerated`, `ForecastGenerated`, `AIRequestSubmitted`, `AISuggestionProduced`, `AISuggestionApproved`, `AISuggestionRejected`, `ModelPerformanceReviewed` | `AIRequestRejectedByPolicy` *(generalizes the Baseline's R1 rejected-candidate pattern, Phase 10, platform-wide)* | AI Gateway governance policy (already Accepted, Constitution Section 28) | Any persona (requester), AI Operations |

## Cluster J — Notifications, Home Visits, Device Operations (gap-fill only — most events already Evidenced)

| Gap Found | Domain Event Added | Cluster |
|---|---|---|
| No delivery-failure event existed for notifications | `NotificationDeliveryFailed` | Notification and Communication |
| Calibration-due timer (Cluster D) directly affects device availability | Cross-reference only, no new event | Device Integration ↔ Asset and Maintenance |

## Domain vs. Integration Event Discipline Check

Every event listed above is a **Domain Event** (internal to its owning
cluster/context). None are promoted to Integration Events in this Wave —
that promotion (deliberate translation, per Constitution Section 12)
happens only once Wave 9 fixes the actual Bounded Context boundaries these
clusters will live in. This mirrors exactly how the Baseline handled the
same distinction (Phase 03 raw events → Phase 06 formal Integration Events).

## Summary

**~75 new Domain Events** across 10 clusters (exact count: Cluster A 6,
B 8, C 15, D 11, E 9, F 11, G 10, H 6, I 7, J 1 = 84), plus 2 Timer-driven
events (`CredentialExpiringSoon`, `CalibrationDue`). Combined with the
Baseline's 26 (+4 gap-identified) events, the platform's total Domain
Event catalog now stands at **~114 events** across 18 clusters/domains
(8 Baseline Bounded Contexts + 10 new clusters).
