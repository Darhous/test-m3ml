# Value Stream Inventory (Discovery, Phase 02)

**Status: Draft — Assumption-Driven Autonomous Run.** All four value
streams are `Inferred — Industry Reference` unless otherwise cited; none
represent a real, confirmed workflow of this specific platform yet. Each
is scoped tightly enough to be storm-walked in Phase 03.

## VS1 — Walk-in Test Order to Verified Result Delivery

**Trigger:** a doctor (or self-requesting patient, where permitted) orders
a laboratory test at an Organization Branch.
**Value delivered:** the patient/doctor receives a clinically verified,
trustworthy result they can act on.
**Stakeholders involved:** Patient, Referring Doctor, Laboratory Staff,
Laboratory Management, Organization Administrators.
**Step outline:** order captured → specimen collected at branch → specimen
accessioned → test processed → result captured → result verified by
qualified staff → result released → patient/doctor notified → report
available via Portal.

## VS2 — Home Sample Collection to Verified Result Delivery

**Trigger:** a patient requests sample collection outside a branch (home/
remote visit).
**Value delivered:** same clinical value as VS1, with added convenience/
access for patients who cannot visit a branch.
**Stakeholders involved:** Patient, Device Integration Teams (if a
portable device is used at the visit), Laboratory Staff, Support Teams
(scheduling the visit).
**Step outline:** order + home-visit request captured → visit scheduled →
collector dispatched → specimen collected in the field → specimen
transported and accessioned → (converges with VS1 from accessioning
onward).
**Note:** `open-questions.md` #6 (Offline Mode) is directly relevant here —
a field collector may operate with intermittent connectivity; this is
flagged, not resolved, at this phase.

## VS3 — Specimen Rejected and Recollected

**Trigger:** an accessioned specimen fails a quality check (e.g.,
insufficient volume, hemolyzed, mislabeled — standard lab QC criteria).
**Value delivered:** prevents an unreliable result from ever reaching a
patient/doctor; value is risk-avoidance, not a positive deliverable in the
usual sense.
**Stakeholders involved:** Laboratory Staff, Patient, Referring Doctor,
Support Teams (coordinating recollection).
**Step outline:** specimen received → QC check fails → specimen rejected
with a reason code → patient/doctor notified → recollection scheduled →
re-enters VS1/VS2 from collection onward.

## VS4 — Insurance Claim Billing Cycle

**Trigger:** a completed, billable test order needs to be invoiced and, where
applicable, claimed against an insurer/payer.
**Value delivered:** the Organization is paid for services rendered; the
patient's out-of-pocket responsibility is correctly determined.
**Stakeholders involved:** Finance Teams, Insurance Users, Patient,
Organization Administrators.
**Step outline:** billable event identified (e.g., result released) →
invoice generated → insurance eligibility/coverage determined → claim
submitted where applicable → claim adjudicated → patient balance (if any)
settled.
**Note:** this value stream is the least detailed of the four — insurance/
billing model specifics are not stated anywhere in Confirmed context and
are logged as an Open Question, not invented in detail.

## Explicitly Not Traced (Open, for a future Discovery iteration)

- A hospital/clinic-specific value stream (depends on `open-questions.md`
  #9, still Open).
- A supplier/procurement value stream (Inventory & Reagent Management
  capability exists in the map, but no value stream was traced for it in
  this pass — flagged as a gap for a future Discovery iteration, not
  fabricated here).
