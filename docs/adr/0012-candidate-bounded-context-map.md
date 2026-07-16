# 0012: Candidate Bounded Context Map (8 Contexts)

## Status

**Proposed** — *not* Accepted, for the same reason as ADR 0011 (this
Discovery run was Assumption-Driven; see that ADR's "Why Proposed, Not
Accepted" section, which applies identically here and is not repeated in
full).

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
