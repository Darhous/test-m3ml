# 0012: Candidate Bounded Context Map (8 Contexts)

## Status

**Proposed — Amended (Gap Closure Wave 14, 2026-07-16).** Still *not*
Accepted, for the same reason as ADR 0011 (this Discovery run was
Assumption-Driven; see that ADR's "Why Proposed, Not Accepted" section,
which applies identically here and is not repeated in full). See the
"Amendment — Gap Closure Wave 14" section below for the current form of
this proposal.

## Amendment — Gap Closure Wave 14 (2026-07-16)

**Disposition: Amend** (of the 5 governance-allowed outcomes — Retain-as-
Proposed / Amend / Supersede / Reject / Split). Not Retain-as-Proposed,
because Gap Closure Wave 9 produced a materially larger evidence base (29
previously-missing domains stormed in Wave 5, 100 capabilities in Wave 3)
that the original 8-context map did not have access to. Not Supersede,
because all 8 original contexts survive into the amended map unchanged in
substance — this is a genuine expansion, not a replacement of the
original reasoning. Not Reject, because Wave 9 found no defect in the
original 8; it found them incomplete relative to the now much larger
evidence base. Not Split, because the amended proposal is presented as one
coherent, internally-tiered map, not two independent decisions.

**Amended proposal: a Hybrid Modeled/Recognized 28-context map**, per
`docs/discovery/artifacts/W9-bounded-context-remapping.md`'s 3-option
Decision Matrix (full uniform adoption of all 28 vs. keep the original 8
vs. this Hybrid). The original 8 contexts (renamed/refined where Wave 8's
Ubiquitous Language work required it) plus 1 additional context justified
by direct Event Storming evidence (Wave 5) form the **Modeled tier (9
contexts)** — carrying the same Evidenced confidence as the original ADR.
The remaining **19 contexts are Recognized-tier** — named and boundary-
sketched from the Wave 3/5 capability and event evidence, but explicitly
lower-confidence (`Inferred`, not `Evidenced`) and not yet subjected to
the same depth of tactical modeling (Aggregates, invariants) the original
8 received in Phase 05. A 29th candidate (Integration Hub) was considered
and rejected on evidence grounds (no distinct event chain or capability
cluster justifies it as separate from Device and Equipment Integration).
The acyclic Module Dependency graph property is re-verified as holding
across all 28 contexts, not just the original 8. Full per-context
justification is in the Wave 9 artifact, not repeated here.

**This remains a Recommendation, not a Decision** — both tiers rest on
evidence gathered under the same Assumption-Driven Autonomous Run mode as
the original ADR; the Recognized tier in particular should not be read as
equivalent in confidence to the Modeled tier or to the original 8. The
Patient/Doctor context gap (original ADR's Negative Consequences, Risk
#7) is closed by this amendment — Wave 5 modeled both as owned domains,
and Wave 9 gives each a dedicated Recognized-tier context — but that
closure is itself `Inferred`, not stakeholder-confirmed.

## Context

Constitution Section 2/46 and `.claude/context/module-catalog.md` have,
since Constitution v1, deliberately held only 16 high-level *categories* —
explicitly not a final Module/Bounded-Context list, pending a dedicated DDD
session. Discovery Phases 04–06 ran that session in sequence (Subdomain
clustering → candidate tactical modeling → formal boundary-drawing),
producing 8 Bounded Contexts, an 11-relationship Context Map with every
relationship pattern-labeled, and a confirmed acyclic Module Dependency
graph (`docs/discovery/artifacts/06-bounded-contexts.md`,
`06-context-map.md`).

## Decision

**Proposed:** the platform's Bounded Contexts are Order Management,
Specimen Management, Test Processing and Result Verification (Core, ADR
0011), Notification and Communication, Billing and Claims, Device and
Equipment Integration, and Core Platform (split internally into Identity/
Access and Organization/Branch) — 8 contexts total, with the Context Map
and Module Ownership draft exactly as recorded in
`docs/discovery/artifacts/06-bounded-contexts.md`.

## Alternatives Considered

- **Merge Specimen Management into Test Processing and Result
  Verification** (treat lab-internal work as one context). Rejected in
  Phase 06 on the evidence that they carry different Core/Supporting
  classifications and different primary actor groups, with
  `SpecimenAccessioned` marking a genuine responsibility handoff — but this
  remains the single most consequential judgment call in the whole Context
  Map and is flagged (Risk #8) as worth re-examination once real business
  input exists.
- **A Shared Kernel for Organization/Branch reference data**, given its use
  by every context. Explicitly considered and rejected in favor of Open
  Host Service + Published Language (Phase 06), consistent with
  Constitution Section 7's caution to keep Shared Kernel rare and
  small — not adopted, so this alternative does not itself require an ADR.
- **Treating `module-catalog.md`'s 16 categories as the final answer
  as-is.** Rejected — Discovery evidence (Phases 03–06) showed the
  "Laboratory Modules" category was too coarse (splits into 3 contexts with
  different Core/Supporting classifications) and "Insurance Modules"
  arguably folds into "Billing and Claims" pending `open-questions.md`
  #17 — documented as divergence, not silently imposed.

## Why Proposed, Not Accepted

Identical reasoning to ADR 0011: every Subdomain/Context boundary here
traces to `Inferred — Industry Reference` evidence (Assumption Register
entries #1–24), not real stakeholder confirmation. Additionally, this
proposal is **explicitly not** a final Module Catalog — Constitution
Section 2/46 and `module-catalog.md`'s own governing rule require it to
stay non-final regardless of this ADR's status, per the explicit labeling
already applied in Phase 06/12 ("Discovery Candidates — not a final Module
Catalog").

## Positive Consequences (if ultimately Accepted)

- Gives the future SAD a concrete, internally-consistent starting
  structure (acyclic dependency graph, fully-labeled Context Map) instead
  of 16 unstructured categories.
- The two Independent Components already Accepted in the Constitution
  (Notification Service, Device Integration Gateway — Section 11) map
  cleanly onto 2 of these 8 contexts, a positive cross-consistency signal
  found during Phase 06, not engineered to fit.

## Negative Consequences

- If the Specimen Management/Test Processing split (or any other boundary)
  proves wrong once real input exists, contexts already built against this
  map would need boundary rework, not just a rule update — the most
  expensive kind of correction in DDD practice.
- Patient and Doctor remain without an owned context (Risk #7) — this
  proposal may be incomplete, not just imprecise.

## Risks

- Same primary risk as ADR 0011: this Proposed ADR being mistaken for
  settled architecture. Mitigated identically (explicit Status, explicit
  "Why Proposed" section).
- The Specimen/Test-Processing boundary (Risk #8) and the missing Patient/
  Doctor context (Risk #7) are the two highest-value items for the user to
  scrutinize specifically, not the map as a whole uniformly.

## Verification

- User reviews `docs/discovery/artifacts/06-bounded-contexts.md` in full,
  with particular attention to the Specimen/Test-Processing split
  rationale and the Patient/Doctor gap, before this ADR is promoted to
  Accepted.
- Once confirmed (in whole or with amendments), promote via Constitution
  Section 45, and update `.claude/context/module-catalog.md` from
  "Discovery Candidates" to a real Module Catalog entry set at that time —
  not automatically upon this ADR's authoring.

## Revisit Triggers

- User confirms, amends, or rejects the Context Map, in whole or in part.
- Real Event Storming with actual domain experts changes Phase 03's event
  chronology materially.
- Phase 07's flagged Patient/Doctor context gap (Risk #7) proves to need
  its own Bounded Context once real workflow detail exists.

## Revisit Triggers — Added by Gap Closure Wave 14 Amendment

- User confirms, narrows, or rejects the Hybrid Modeled/Recognized tiering
  specifically, or any individual Recognized-tier context.
- Any Recognized-tier context receives real Event Storming evidence
  (moving it toward Modeled-tier confidence) or is found to have no
  distinct justification on closer review (candidate for merge/removal).
- ADR-0011's Core Domain amendment ("Patient-to-Result Orchestration")
  is confirmed or rejected by the user — a rejection could change which
  context(s) this map treats as Core.
