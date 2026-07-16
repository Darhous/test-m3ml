# Command Catalog (Discovery, Phase 12)

**Status: Draft — extracted from `03-event-storming-board.md`'s
"Triggering Command" columns, consolidated into one index.** No new content
— pure extraction/organization for direct reference by a future SAD.

| Command | Raises Event | Actor | Bounded Context |
|---|---|---|---|
| Order Test | `TestOrdered` | Doctor / Patient | Order Management |
| Collect Specimen | `SpecimenCollected` | Laboratory Staff | Specimen Management |
| Request Home Visit | `HomeVisitRequested` | Patient | Specimen Management |
| Schedule Visit | `HomeVisitScheduled` | Support Staff / System | Specimen Management |
| Dispatch Collector | `CollectorDispatched` | System / Support Staff | Specimen Management |
| Collect Specimen In Field | `SpecimenCollectedAtHome` | Sample Collector | Specimen Management |
| Transport Specimen | `SpecimenTransportedToLab` | Sample Collector / Courier | Specimen Management |
| Accession Specimen | `SpecimenAccessioned` | Laboratory Staff | Specimen Management |
| Check Specimen Quality | `SpecimenQualityChecked` | Laboratory Staff | Specimen Management |
| Reject Specimen | `SpecimenRejected` | Laboratory Staff | Specimen Management |
| Schedule Recollection | `RecollectionScheduled` | Support Staff / Patient | Specimen Management |
| Start Processing | `TestProcessingStarted` | Laboratory Staff / Device | Test Processing and Result Verification |
| Capture Result | `TestResultCaptured` | Laboratory Staff / Device | Test Processing and Result Verification |
| Verify Result | `ResultVerified` | **Result Verifier Role only** (Phase 07) | Test Processing and Result Verification |
| Release Result | `ResultReleased` | System (gated on Verified) | Test Processing and Result Verification |
| *(proposed, Phase 05/07)* | `ResultCorrected` | **Result Verifier Role only** | Test Processing and Result Verification |
| *(proposed, Phase 07)* | `TestProcessingFailed` | System / Device | Test Processing and Result Verification |
| Send Notification | `PatientNotified` / `DoctorNotified` / rejection variants | System | Notification and Communication |
| Identify Billable Event | `BillableEventIdentified` | System | Billing and Claims |
| Generate Invoice | `InvoiceGenerated` | System / Finance Staff | Billing and Claims |
| Check Eligibility | `InsuranceEligibilityChecked` | Finance Staff / System | Billing and Claims |
| Submit Claim | `ClaimSubmitted` | Finance Staff | Billing and Claims |
| *(external-originated)* | `ClaimAdjudicated` | Insurance/Payer System | Billing and Claims |
| *(proposed, Phase 07)* | `ClaimDenied` | Insurance/Payer System | Billing and Claims |
| Settle Payment | `PatientBalanceSettled` | Patient / Finance Staff | Billing and Claims |
| *(proposed, Phase 08)* | `HomeVisitFailed` | System / Sample Collector | Specimen Management |

**Sensitive Operations (Constitution Section 21), commands requiring
elevated authorization:** Verify Result, and the proposed Result
Correction command — both gated to the Result Verifier Role exclusively
(Phase 07).
