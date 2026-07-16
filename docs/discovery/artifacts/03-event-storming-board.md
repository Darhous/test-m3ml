# Event Storming Board (Discovery, Phase 03)

**Status: Draft — Assumption-Driven Autonomous Run.** All events/commands/
actors below are `Inferred — Industry Reference` unless cited to a
Confirmed source. Naming follows Constitution Section 6/12/13 (past tense,
Ubiquitous Language, no CRUD-style names).

## VS1 — Walk-in Test Order to Verified Result Delivery

| # | Event | Triggering Command | Actor | External System |
|---|---|---|---|---|
| 1 | `TestOrdered` | Order Test | Doctor / Patient | — |
| 2 | `SpecimenCollected` | Collect Specimen | Laboratory Staff (Phlebotomist) | — |
| 3 | `SpecimenAccessioned` | Accession Specimen | Laboratory Staff | — |
| 4 | `SpecimenQualityChecked` (pass branch) | Check Specimen Quality | Laboratory Staff | — |
| 5 | `TestProcessingStarted` | Start Processing | Laboratory Staff | Lab Analyzer Device (candidate) |
| 6 | `TestResultCaptured` | Capture Result | Laboratory Staff / Device | Lab Analyzer Device (candidate) |
| 7 | **`ResultVerified`** (Pivotal) | Verify Result | Pathologist / authorized Laboratory Staff | — |
| 8 | **`ResultReleased`** (Pivotal) | Release Result | Laboratory Staff / System | — |
| 9 | `PatientNotified` / `DoctorNotified` | Send Notification | System | Notification channel (candidate) |
| 10 | `ReportViewed` (terminal, optional) | View Report | Patient / Doctor | — |

**Hotspots (VS1):**
- H1 — Who is authorized to perform `ResultVerified` likely varies by test
  type/regulatory requirement (Pathologist for some, senior Lab Technician
  for others) — not resolved here, candidate Sensitive Operation for
  Phase 07.
- H2 — No event exists yet for a processing/equipment failure mid-run
  (between `TestProcessingStarted` and `TestResultCaptured`) — flagged as a
  missing event candidate, not invented.
- H3 — Is there a time-bound expiry on `TestOrdered` if the patient never
  shows up for collection? Unresolved.

## VS2 — Home Sample Collection to Verified Result Delivery

| # | Event | Triggering Command | Actor | External System |
|---|---|---|---|---|
| 1 | `HomeVisitRequested` | Request Home Visit | Patient | — |
| 2 | `HomeVisitScheduled` | Schedule Visit | Support Staff / System | — |
| 3 | `CollectorDispatched` | Dispatch Collector | System / Support Staff | — |
| 4 | `SpecimenCollectedAtHome` | Collect Specimen In Field | Sample Collector | Portable collection device (candidate) |
| 5 | `SpecimenTransportedToLab` | Transport Specimen | Sample Collector / Courier | — |
| — | *(converges with VS1 #3, `SpecimenAccessioned`)* | | | |

**Hotspots (VS2):**
- H4 — No event exists for a failed home visit (patient no-show, wrong
  address) — missing event candidate, not invented.
- H5 — No explicit chain-of-custody handoff event between collector and
  lab during transport — candidate missing event
  (`SpecimenHandedOffToLab`), flagged for Phase 05/07, not added to the
  board as confirmed here.
- H6 — Directly relevant to `open-questions.md` #6 (Offline Mode): if the
  collector's device cannot sync in real time, when does
  `SpecimenCollectedAtHome` actually get recorded platform-side? Left
  explicitly unresolved.

## VS3 — Specimen Rejected and Recollected

| # | Event | Triggering Command | Actor | External System |
|---|---|---|---|---|
| 1 | `SpecimenQualityChecked` (fail branch) | Check Specimen Quality | Laboratory Staff | — |
| 2 | **`SpecimenRejected`** (Pivotal) | Reject Specimen | Laboratory Staff | — |
| 3 | `PatientNotifiedOfRejection` / `DoctorNotifiedOfRejection` | Send Notification | System | Notification channel |
| 4 | `RecollectionScheduled` | Schedule Recollection | Support Staff / Patient | — |
| — | *(re-enters VS1 #2 or VS2 #1, Collection)* | | | |

**Hotspots (VS3):**
- H7 — No escalation event exists for repeated rejections of the same
  order (e.g., informing the doctor after N failed attempts) — missing
  event candidate.
- H8 — Rejection reason taxonomy is `Inferred — Industry Reference`
  (candidates: Insufficient Volume, Hemolyzed, Clotted, Mislabeled, Wrong
  Container, Contaminated) — not confirmed for this platform.

## VS4 — Insurance Claim Billing Cycle

| # | Event | Triggering Command | Actor | External System |
|---|---|---|---|---|
| 1 | `BillableEventIdentified` | Identify Billable Event | System (triggered by `ResultReleased`) | — |
| 2 | `InvoiceGenerated` | Generate Invoice | System / Finance Staff | — |
| 3 | `InsuranceEligibilityChecked` | Check Eligibility | Finance Staff / System | Insurance/Payer system (candidate) |
| 4 | `ClaimSubmitted` | Submit Claim | Finance Staff | Insurance/Payer system (candidate) |
| 5 | **`ClaimAdjudicated`** (Pivotal — external-system-originated) | *(none — originates from the external Payer, not an internal command)* | Insurance/Payer system | Insurance/Payer system (candidate) |
| 6 | `PatientBalanceSettled` | Settle Payment | Patient / Finance Staff | — |

**Hotspots (VS4):**
- H9 — No `ClaimRejected`/`ClaimDenied` event modeled yet for an adverse
  adjudication outcome — missing event candidate.
- H10 — The entire value stream rests on `open-questions.md` #17
  (billing/insurance model), still Open — this is the least reliable part
  of the board.

## Cross-Value-Stream Actor Inventory (candidate Roles)

Patient, Doctor, Laboratory Staff (candidate sub-roles: Phlebotomist/
Sample Collector, Lab Technician, Pathologist/Result Verifier — not yet
split as formal Roles, per `stakeholders.md`'s own note that finer role
splitting is a later exercise), Support Staff, Finance Staff, System
(automated actor, for system-triggered commands).

## Cross-Value-Stream External System Inventory (candidate)

Lab Analyzer Device, Portable Collection Device, Notification Channel
(channel-agnostic), Insurance/Payer System. None of these name a specific
vendor/product — all are integration *categories*, consistent with
Constitution's technology-neutral posture.

## Pivotal Events (candidates, for Phase 04/06)

`ResultVerified`, `ResultReleased`, `SpecimenAccessioned`,
`SpecimenRejected`, `ClaimAdjudicated` — each marks a handoff between
stakeholder groups or a significant state transition. These are inputs to
Phase 04's Subdomain clustering and Phase 06's Bounded Context boundary
decisions — not decided here.
