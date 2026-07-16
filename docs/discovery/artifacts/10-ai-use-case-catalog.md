# AI Use-Case Catalog (Discovery, Phase 10)

**Status: Draft — Assumption-Driven Autonomous Run.** Every candidate below
is checked against Constitution Section 28's Permitted list before
inclusion, and against its Forbidden list before acceptance. No AI
provider, model, or vendor is named anywhere in this catalog.

## Accepted Candidates

| # | Use Case | Bounded Context | Permitted Category (Section 28) | Sensitivity | Human-in-the-Loop Touchpoint |
|---|---|---|---|---|---|
| 1 | Smart test-panel suggestion based on stated symptoms | Order Management | Clinical decision *support* | Medium | Doctor reviews and explicitly places the order; AI output is a suggestion only, never auto-submitted as `TestOrdered`. |
| 2 | Rejection-risk flagging before/during specimen collection | Specimen Management | Anomaly detection | Medium | Collector sees the flag as advisory; collection technique/decision remains theirs — AI never blocks or auto-rejects a specimen. |
| 3 | Result pattern flagging for verifier attention | Test Processing and Result Verification (**Core**) | Pattern detection | **High** | The `ResultVerified` gate (Phase 07, Result Verifier Role) is the HITL checkpoint — AI flags, a human verifies; this use case cannot exist independently of that already-mandatory gate. |
| 4 | Patient-friendly explanation of an already-released result | Test Processing and Result Verification | Patient-friendly explanations | Medium | Applies only *after* `ResultReleased` (a Sensitive Operation already completed by a human) — explanation is of a human-approved fact, does not itself approve anything. |
| 5 | Billing/claim anomaly flagging | Billing and Claims | Anomaly detection | Medium | Finance Staff reviews flagged items before any action; AI never auto-adjusts or auto-denies a claim. |
| 6 | Natural-language search across test catalog and order history | Order Management (cross-cutting) | Search | Low-Medium | Not applicable in the approval sense — but results must be filtered through the requester's Data Scope (Constitution Section 21) before display. |
| 7 | Device data-quality anomaly flagging (e.g., sensor drift) | Device and Equipment Integration | Anomaly detection | Medium | Laboratory Staff reviews flagged device imports before they proceed to `TestResult`'s `ProvenanceInfo` — an additional advisory layer on top of the Phase 08 ACL, not a replacement for it. |

## Candidates Requiring Further Design Before "Ready" (not rejected, not yet complete)

| # | Use Case | Issue | Status |
|---|---|---|---|
| 8 | AI-summarized patient notification content | Permitted under Section 28 ("Summarization," "patient-friendly explanations"), but free-form generation sent directly to a patient without any accuracy check is a real-world risk even though not on the literal Forbidden list. | **Not Ready** — proposed mitigation: template-bounded summarization (constrained phrasing) rather than fully free-form generation, or a lightweight review step; design not completed here. |

## Rejected Candidates (Forbidden-List Matches)

| # | Candidate | Forbidden-List Match | Reasoning |
|---|---|---|---|
| R1 | AI auto-verifies "straightforward"/normal results to speed up turnaround | "AI may not independently... approve a medical result... modify a verified medical result... send a final medical decision without human review" (Constitution Section 28) | Rejected outright, not softened or reworded. This is exactly the kind of plausible-sounding efficiency proposal Section 28 exists to block — flagged explicitly so it is not silently reconsidered in a later phase. |

## Explicitly Out-of-Section-28-Scope (logged, not decided here)

| Candidate | Note |
|---|---|
| AI auto-approves low-risk insurance claims without human review | Not a "final medical decision" — not covered by Section 28's Forbidden list. Not accepted or rejected here; this is a *financial*-automation governance question, logged for Phase 12's Risk Governance discussion rather than resolved under AI-Discovery's medical-governance lens. |

## AI Gateway Contract Shape (technology-agnostic sketch)

| Element | Content |
|---|---|
| Input | Request context type (per use case above), requesting Actor + Role, Data Scope context, sensitivity classification |
| Output | Suggestion/output + confidence indicator + rationale reference (not a final action) |
| Required audit fields (Constitution Section 23/28) | Prompt reference/version, model/version placeholder (no vendor named), cost tracking placeholder, evaluation-outcome placeholder, timestamp, requesting Actor |
| Human-in-the-Loop marker | Every response for a sensitive-classified use case (#1, #3, #4, #7) carries an explicit "requires human confirmation before action" flag in the contract itself — not left implicit in client behavior. |

## Data Minimization Notes (per use case, for any future external-provider call)

- **High/Medium-High minimization burden:** #3 (result patterns), #4
  (patient explanations), #8 (notification summaries) — all touch medical
  content directly; Constitution Section 28's policy-gate requirement
  applies in full before any external call.
- **Lower minimization burden:** #5 (billing anomaly on aggregate
  patterns), #6 (catalog search, non-PII), #7 (device signal quality,
  not patient-identifying by itself) — still require the same policy gate
  in principle, but the underlying data is less inherently sensitive.
- **No use case in this catalog is assumed to use an external provider** —
  this remains an SAD-level implementation choice; Discovery only confirms
  the governance gate applies whenever/if that choice is made.
