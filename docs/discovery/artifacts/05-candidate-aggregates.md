# Candidate Aggregates (Discovery, Phase 05)

**Status: Draft — Candidate pass, Assumption-Driven Autonomous Run.** Per
Playbook 05's own ordering note, these are candidates ahead of formal
Bounded Context boundary-drawing (Phase 06), not final tactical designs.

## Subdomain 1 — Order Management (Supporting)

| Element | Type | Notes |
|---|---|---|
| **TestOrder** | Aggregate Root / Entity | Identity: OrderID. Entity test passed: same order even as its status changes (Requested→Collected→Cancelled→Expired). |
| OrderedTestList | Value Object | List of Test Catalog references + panel info. |
| OrderingActorRef | Value Object | Reference (by ID) to the ordering Doctor or Patient — not embedded. |
| **TestCatalogEntry** | Aggregate Root / Entity (separate Aggregate) | Identity: TestCode. Reference-data aggregate, low change frequency. |
| SpecimenRequirement | Value Object | Part of TestCatalogEntry. |

**Consistency rationale:** TestOrder's own state transitions must be
immediately consistent (an order cannot be simultaneously Cancelled and
Collected); it does not need to embed Specimen or Result data — those are
referenced by ID once they exist (see Subdomains 2–3).

**Events raised:** `TestOrdered`.

## Subdomain 2 — Specimen Management (Supporting, debated)

| Element | Type | Notes |
|---|---|---|
| **Specimen** | Aggregate Root / Entity | Identity: SpecimenID. Entity test passed: same specimen through Collected→Transported→Accessioned→QualityChecked→Accepted/Rejected. |
| CollectionDetails | Value Object | Who collected, when, where (branch or home-visit). |
| RejectionReason | Value Object | Reason code (Insufficient Volume, Hemolyzed, Clotted, Mislabeled, Wrong Container, Contaminated — Inferred taxonomy from Phase 03) + free-text note. |
| ChainOfCustodyRecord | Value Object — **candidate, not yet evidenced** | Corresponds to Hotspot H5 (Phase 03) — flagged as needed, not yet designed in detail. |

**Consistency rationale:** a Specimen's QC/rejection state must be
immediately consistent (cannot be simultaneously Accepted and Rejected).
References TestOrder by ID (a Specimen exists to satisfy an Order, but is
not embedded inside it — different lifecycle, different actors).

**Events raised:** `SpecimenCollected`, `HomeVisitRequested`,
`HomeVisitScheduled`, `CollectorDispatched`, `SpecimenCollectedAtHome`,
`SpecimenTransportedToLab`, `SpecimenAccessioned`,
`SpecimenQualityChecked`, `SpecimenRejected`.

## Subdomain 3 — Test Processing and Result Verification (Core)

| Element | Type | Notes |
|---|---|---|
| **TestResult** | Aggregate Root / Entity | Identity: ResultID. Entity test passed: same result through Captured→Verified→Released→(possibly Corrected). This is the Core Domain's central Aggregate — smallest, most tightly guarded consistency boundary in the model. |
| ResultValue | Value Object | Measurement + unit + reference range. |
| VerificationRecord | Value Object | Who verified (Role reference), when — feeds Constitution Section 21/23 Sensitive-Operation/Audit requirements directly. |
| ProvenanceInfo | Value Object — **candidate** | Source (manual entry vs. device), device reference, raw-payload reference — required by Constitution Section 24 wherever a Result originates from a device. |

**Consistency rationale:** verification and release are the two most
tightly guarded transitions in the entire model (Constitution Section 21's
"Sensitive Operations Require Elevated Controls" applies directly) — kept
in one small Aggregate so no other Aggregate can partially mutate a
Result's clinical state. References Specimen and TestOrder by ID.

**Events raised:** `TestProcessingStarted`, `TestResultCaptured`,
`ResultVerified`, `ResultReleased`.

**Newly identified gap (not on the Phase 03 board):** no event exists yet
for a post-release correction. DDD practice (and the Constitution's own
Section 12 illustrative example) suggests a `ResultCorrected` event,
distinct from mutating `ResultVerified`/`ResultReleased` in place (events
are immutable facts, Constitution Section 12). **Flagged as a candidate
missing event, not added to the Phase 03 board retroactively** — logged in
`OPEN-QUESTIONS-REGISTER.md` for Phase 07.

## Subdomain 4 — Notification and Communication (Generic)

| Element | Type | Notes |
|---|---|---|
| **NotificationRequest** | Aggregate Root / Entity | Identity: NotificationID. States: Queued→Sent→Delivered/Failed. |
| RecipientRef | Value Object | Reference to Patient/Doctor by ID. |
| ChannelPreference | Value Object — **candidate** | Channel is still Open (`open-questions.md` #10). |

**Modeling depth note:** per DDD Strategic Design guidance for Generic
Subdomains ("build, but don't over-engineer... thin adapter"), this
Aggregate is deliberately shallow — deep tactical investment belongs in the
Core Subdomain (3), not here.

**Events raised:** `PatientNotified`, `DoctorNotified`,
`PatientNotifiedOfRejection`, `DoctorNotifiedOfRejection`.

## Subdomain 5 — Billing and Claims (Supporting, weak VS4 evidence)

| Element | Type | Notes |
|---|---|---|
| **Invoice** | Aggregate Root / Entity | Identity: InvoiceID. States: Generated→Settled. |
| LineItem | Value Object | Part of Invoice. |
| **Claim** | Aggregate Root / Entity (separate Aggregate) | Identity: ClaimID. States: Submitted→Adjudicated→(Approved/Denied)→Settled. Kept separate from Invoice — different lifecycle, externally-driven transition (`ClaimAdjudicated` originates from the Payer, not an internal command), referenced from Invoice by ID rather than embedded. |

**Events raised:** `BillableEventIdentified`, `InvoiceGenerated`,
`InsuranceEligibilityChecked`, `ClaimSubmitted`, `ClaimAdjudicated`,
`PatientBalanceSettled`.

**Newly identified gap:** no `ClaimDenied`/`ClaimRejected` event exists yet
(same gap as Phase 03 Hotspot H9) — Claim's state machine needs this
branch; not designed in detail here, flagged for Phase 07.

## Subdomain 6 — Identity and Access (Generic)

**Not tactically modeled here.** Already governed at the Constitution/
Context Store level (`User`, `Role`, `Permission`, `Policy`, `Data Scope`
are already-Draft glossary terms; Core Platform ownership is already
Accepted, Constitution Section 10). Re-deriving tactical structure here
would duplicate, not add, information.

## Subdomain 7 — Device and Equipment Integration (Supporting)

| Element | Type | Notes |
|---|---|---|
| **DeviceImportRecord** | Aggregate Root / Entity — **candidate** | Identity: ImportID. Holds raw payload reference + provenance (device ID, adapter, timestamp) per Constitution Section 24. Feeds `ProvenanceInfo` in Subdomain 3's TestResult via an Anti-Corruption Layer (not embedded directly) — the ACL boundary itself is Phase 06/08's job to design; this candidate Aggregate only marks that the data must land somewhere before crossing into the Core Subdomain. |

## Subdomain 8 — Organization and Branch Management (Generic)

**Not tactically modeled in depth here.** `Organization` and `Branch` are
already-Draft glossary concepts; this Subdomain's role in Discovery is
primarily as a Data Scope dimension (Constitution Section 18/21), not a
rich behavioral model.

## Subdomains 9–11 — Inventory and Reagent Management, Quality Control and
## Accreditation Compliance, Staff and Operations Management

**No candidate Aggregates drafted.** Per Phase 04's own caveat, these three
Subdomains have no Event Storming evidence (Phase 03's traced Value
Streams never touched them). Drafting Aggregates here with zero event
evidence would mean inventing structure, which the No-Guessing Rule and
Playbook 05's own Common Mistakes section forbid. This is logged as an
**explicit gap**, not a "no Aggregates needed" architectural finding — a
future Discovery iteration (or real stakeholder input) is needed before
these Subdomains can be tactically modeled.

## Cross-Subdomain Overlap List (for Phase 06)

| Overlap / Boundary Question | Notes |
|---|---|
| Specimen Management vs. Test Processing and Result Verification | Sequentially adjacent (Specimen feeds into Result via `SpecimenAccessioned`→processing), but classified differently (Supporting vs. Core) in Phase 04. This classification difference is itself evidence they should likely be **separate** Bounded Contexts even though tightly sequenced — Phase 06 must decide formally, not this phase. |
| Device and Equipment Integration → Test Processing and Result Verification | `DeviceImportRecord` (Subdomain 7) supplies `ProvenanceInfo` to `TestResult` (Subdomain 3) — this crossing needs an explicit Anti-Corruption Layer per Constitution Section 6/24; Phase 06 must assign the Context Mapping pattern. |
| Order Management vs. Specimen Management vs. Billing and Claims | All three reference `TestOrder`/`Specimen` by ID from different angles (an Order is referenced by a Specimen; a billable event is "identified" from `ResultReleased`, which itself references an Order transitively) — no embedding found, so no forced-merge overlap, but Phase 06 should confirm the reference chain doesn't imply a hidden coupling. |
| Notification and Communication | Referenced by (not embedding) Specimen Management, Test Processing, and Billing and Claims (each raises notification-triggering events) — confirms Generic/cross-cutting classification from Phase 04, not a boundary conflict. |
