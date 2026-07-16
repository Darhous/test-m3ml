# Business Rules Catalog (Discovery, Phase 07)

**Status: Draft — Assumption-Driven Autonomous Run.** Refines Phase 05/06
structure into invariants and rules. Every Hotspot from Phase 03/05 is
either resolved at the *modeling* level (a rule/event is proposed) or left
explicitly Open at the *business* level (the real-world answer is still
unknown) — the two are kept distinct throughout.

## TestOrder (Order Management)

**Invariants:**
- An order must reference at least one valid `TestCatalogEntry`.
- Status transitions only: `Requested → Collected → Completed`,
  `Requested → Cancelled`, `Requested → Expired`.

**Resolves H3 (order expiry):** Proposed rule — an order in `Requested`
status expires automatically after a configurable window with no specimen
collected. **The window's actual value is Open** (no basis to invent a
number; logged to Open Questions).

**Sensitive Operation?** No (does not meet Constitution Section 21's
definition). Standard operational audit applies, not elevated controls.

## Specimen (Specimen Management)

**Invariants:**
- A Specimen references exactly one `TestOrder`.
- A `Rejected` Specimen is terminal — recollection creates a **new**
  Specimen instance referencing the same `TestOrder`, it does not resurrect
  the rejected one (preserves the immutability/audit value of the original
  rejection record).
- Status transitions: `Collected → [Transported] → Accessioned →
  QualityChecked → {Accepted | Rejected}`. (`Transported` only applies to
  home-collection specimens.)

**Resolves H7 (repeated-rejection escalation):** Proposed rule — after N
rejections for the same `TestOrder`, escalate to the ordering Doctor/
Support Staff. **N is Open** (no basis to invent a threshold).

**Resolves H8 (rejection taxonomy):** Used for modeling purposes
(Insufficient Volume, Hemolyzed, Clotted, Mislabeled, Wrong Container,
Contaminated) — **confidence remains Medium, not Confirmed**; real taxonomy
should be validated against this platform's actual accreditation
requirements.

**Sensitive Operation?** No (does not meet Constitution Section 21's
strict definition), but `SpecimenRejected` still requires standard
operational audit given its quality/compliance relevance
(Constitution Section 29, Quality Control relevance) — a lighter bar than
the Sensitive Operation elevated-controls requirement.

## TestResult (Test Processing and Result Verification) — Core, highest scrutiny

**Invariants:**
- A TestResult references exactly one **Accepted** Specimen (never a
  Rejected one) and one TestOrder.
- Status transitions: `Processing → Captured → Verified → Released`. A
  correction after `Released` never mutates the released record — it
  produces a new, linked `ResultCorrected` fact (resolves the Phase 05 gap;
  preserves Constitution Section 12 event immutability).

**Resolves H1 (verification authority) — partially:** Proposed rule — a
Result may only transition to `Verified` by an actor holding a distinct
**Result Verifier** Role (not the general Laboratory Staff/Lab Technician
Role). **This establishes the rule shape (a dedicated authorization gate
exists) without inventing the exact eligibility criteria** (e.g., which
test types require a Pathologist specifically) — that detail remains Open,
logged for real regulatory/operational input.

**Resolves H2 (processing failure) — at modeling level:** Proposed new
event `TestProcessingFailed`, between `TestProcessingStarted` and
`TestResultCaptured`. On failure, the Specimen may require reprocessing or
the Order may need escalation — **the actual recovery policy (retry vs.
recollect vs. manual override) is Open**.

**Sensitive Operations (Constitution Section 21, Confirmed definition
applied, not reinterpreted):** `ResultVerified`, `ResultReleased`, and the
new `ResultCorrected` are **all** Sensitive Operations — each requires
elevated authorization (Result Verifier Role gate) and an Audit Event
(Constitution Section 23). This is the highest-scrutiny rule set in the
entire catalog, consistent with this Subdomain's Core classification.

## Invoice / Claim (Billing and Claims)

**Invariants:**
- An Invoice's billable origin must trace to a `ResultReleased` event
  (`BillableEventIdentified`).
- Claim status transitions: `Submitted → Adjudicated → {Approved |
  Denied} → Settled`.

**Resolves H9 (claim denial):** Proposed new event `ClaimDenied`
(alternative terminal branch from `Adjudicated`), with an unspecified
downstream patient-notification/appeal rule — **process detail Open**,
gated entirely by `open-questions.md` #17 (billing/insurance model).

**Sensitive Operation?** No, under Constitution Section 21's strict
definition (financial, not medical/consent/cross-tenant-admin) — standard
financial audit applies (Finance/Compliance concern, distinct rule set from
Section 21's elevated bar).

## NotificationRequest (Notification and Communication)

**Rule:** notification payload content must be filtered through the
recipient's Data Scope and Consent state (Constitution Section 26) before
send — a notification is never a bypass around Section 21's authorization
model. **This rule is Required, not Open** — it follows directly from an
Accepted Constitution rule, not from assumption.

## DeviceImportRecord (Device and Equipment Integration)

**Rule:** a `DeviceImportRecord` may not be linked to a `TestResult` until
its `ProvenanceInfo` is fully populated (Constitution Section 24). **This
rule is Required, not Open.**

## Cross-Aggregate Policies (Process Managers)

| Policy | Coordinates | Trigger | Notes |
|---|---|---|---|
| Order Fulfillment Policy | TestOrder, Specimen, TestResult (by ID reference only) | `ResultReleased` | Also triggers `BillableEventIdentified` in Billing and Claims — the one confirmed cross-context event trigger in the model. |
| Recollection Policy | Specimen (old + new instance), TestOrder | `SpecimenRejected` | Implements the "new Specimen instance" invariant above. |
| Notification Trigger Policy | Specimen, TestResult, Billing and Claims → Notification and Communication | Various (`SpecimenRejected`, `ResultReleased`, `ClaimDenied`, etc.) | Confirms Notification's Generic/subscriber role from Phase 04/06. |

## Hotspot Resolution Summary (Phase 03 H1–H10, Phase 05 gaps)

| Hotspot | Modeling-Level Resolution | Business-Level Status |
|---|---|---|
| H1 — verification authority | Result Verifier Role gate established | **Open** — eligibility criteria unknown |
| H2 — processing failure | `TestProcessingFailed` event proposed | **Open** — recovery policy unknown |
| H3 — order expiry | Expiry rule proposed | **Open** — window duration unknown |
| H4 — failed home visit | `HomeVisitFailed` event proposed (new) | **Open** — retry policy unknown |
| H5 — chain-of-custody | Not resolved here | **Open** — deferred to Phase 08 |
| H6 — offline mode | Not resolved here | **Open** — pre-existing `open-questions.md` #6 |
| H7 — repeated rejection escalation | Escalation rule proposed | **Open** — threshold N unknown |
| H8 — rejection taxonomy | Used for modeling (Medium confidence) | **Open** — needs real validation |
| H9 — claim denial | `ClaimDenied` event proposed | **Open** — fully gated by #17 |
| H10 — billing model | Not resolved here | **Open** — pre-existing `open-questions.md` #17 |
| Phase 05 — `ResultCorrected` | Modeled as new immutable event | **Open** — confirm this is really needed |
| Phase 05 — chain-of-custody shape | Not resolved here | **Open** — same as H5 |

**No Hotspot was closed by assumption.** Every "modeling-level resolution"
proposes a *rule shape* consistent with DDD/Constitution practice; every
underlying *business fact* stays Open until the user confirms it.
