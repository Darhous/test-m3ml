# 0011: Core Domain — Test Processing and Result Verification

## Status

**Accepted (Open Questions Resolution phase, 2026-07-18).** Previously
`Proposed — Amended (Gap Closure Wave 14, 2026-07-16)`. See "Amendment —
Open Questions Resolution Phase" below for the confirmation record, and
"Why Proposed, Not Accepted" (retained below, historical) for the
reasoning that governed this ADR before confirmation.

## Amendment — Open Questions Resolution Phase (2026-07-18): Confirmed Accepted

**This is the explicit user-review-and-promotion step this ADR's own
Verification section required** ("Once confirmed, this ADR's Status is
updated to Accepted via the normal Constitution Section 45 Amendment/
Section 39 ADR process"). It occurred via a dedicated, explicit
"Enterprise Architecture Decision Board — Open Questions Resolution"
instruction directing this Board to resolve `.claude/context/
open-questions.md` #14 as a required decision area, with the explicit
statement that "architectural questions must not remain unresolved."
This is recorded here as the confirmation event, not asserted as new
evidence.

**What changed and what did not:**

- **Confirmed as Core Domain: "Patient-to-Result Orchestration"** — the
  Gap Closure Wave 14 amendment's framing, unchanged from the Amendment
  section below.
- **The underlying evidence base has not changed.** It remains
  `Inferred — Industry Reference`, generated under Assumption-Driven
  Autonomous Run mode, not confirmed by a real domain expert or
  business stakeholder in a live session. Promotion to Accepted reflects
  the user's exercise of the confirmation authority this ADR always
  required, not a claim that the evidence itself became stronger.
- **Honest disclosure of a residual gap**: Wave 7's 6-alternative
  Decision Matrix (cited in the Gap Closure Wave 14 Amendment below)
  compared this framing against Diagnostic Operations, Laboratory
  Execution, Healthcare Operations Orchestration, Clinical Diagnostic
  Network, and Platform Tenant Operations — it did **not** include a
  direct, scored, head-to-head comparison against the **Specimen
  Management (Home Collection Logistics-differentiated) alternative**
  named below in "Alternatives Considered." That alternative was
  evaluated qualitatively (found credible, not ruled out on evidence)
  but never scored in the same matrix. This promotion accepts that gap
  rather than papering over it — the confirmation decision rests on (a)
  the accumulated weight of every independent architecture-phase review
  finding no *architectural* conflict with this framing (EARB, API
  Platform Part 2, the Certification Audit — see `docs/architecture-
  review/10-ADR-REVIEW.md` and `docs/api-platform/15-ADR-REVIEW.md`),
  and (b) this being the explicit, dedicated decision point the ADR's
  own Verification section named as sufficient, not on a claim that the
  Specimen Management alternative was formally out-scored.
- **Downstream effect**: the 7-Module REFERENCE+BUILD boundary table in
  `docs/architecture-review/10-ADR-REVIEW.md` (Patient Management,
  Diagnostic Ordering, Specimen Operations, Laboratory Execution, Result
  Verification and Reporting, plus Insurance and Corporate Contracts'
  correctly-external openIMIS boundary) is now confirmed, not
  conditional — those Modules' Build-vs-Buy reasoning no longer depends
  on a still-open Core Domain question.
- **This does not retroactively change any Technology Baseline entry,
  Reuse Intelligence decision, or API Platform document** — every prior
  phase's own finding was already "no architectural conflict regardless
  of which Core Domain framing wins," so nothing built on top of this
  ADR requires rework as a result of this promotion.

**Reversibility, stated explicitly per this ADR's own Revisit
Triggers**: if real stakeholder input later contradicts this framing —
in particular if it confirms Specimen Management/Home Collection as the
platform's actual competitive differentiator — the correction path is a
new superseding ADR through the same Constitution Section 45 process,
not a crisis. Nothing about this promotion is irreversible.

## Amendment — Gap Closure Wave 14 (2026-07-16)

**Disposition: Amend** (of the 5 governance-allowed outcomes — Retain-as-
Proposed / Amend / Supersede / Reject / Split — per the Gap Closure
program's ADR Rules). Not Retain-as-Proposed, because Gap Closure Wave 7
produced materially new evidence (a 6-alternative Core Domain Decision
Matrix, `docs/discovery/artifacts/W7-domain-classification-reevaluation.md`)
that the original Decision below did not have access to. Not Supersede,
because the underlying evidence trail (Phase 04's Subdomain clustering)
remains valid and directly feeds the amended proposal rather than being
replaced by an unrelated one. Not Reject, because Wave 7 did not find the
original proposal wrong, only narrower than the evidence now supports.
Not Split, because the amended proposal is still a single coherent Core
Domain claim, not two independent decisions.

**Amended proposed Core Domain: "Patient-to-Result Orchestration"** —
broadens the original "Test Processing and Result Verification" framing
to explicitly include the Patient and Doctor domains that Gap Closure
Wave 5 modeled as owned domains for the first time (closing Baseline Risk
#7), while still centering the same `TestProcessingStarted →
TestResultCaptured → ResultVerified → ResultReleased` event chain and the
same `TestResult` Aggregate as the original proposal's core. Wave 7's
Decision Matrix compared 6 alternatives (the original framing, this
amendment, Laboratory Execution, Healthcare Operations Orchestration,
Clinical Diagnostic Network, and Platform Tenant Operations) and found
this framing the best fit: broad enough to include Patient/Doctor as
first-class participants in the differentiating value chain (not just
cross-cutting Actors, per Baseline Risk #7), but explicitly narrower than
"Healthcare Operations Orchestration," which Wave 7 rejected as premature
given Wave 3's own evidence-imbalance finding (most of the 32-domain
expansion is `Inferred`, not evidenced to Core-Domain-defining depth).
"Clinical Diagnostic Network" was rejected outright for having no
supporting evidence anywhere in the program.

**This remains a Recommendation, not a Decision** — the same Assumption-
Driven evidentiary limits described in "Why Proposed, Not Accepted" below
apply identically to this amendment; Wave 7's Decision Matrix itself is
built on `Inferred — Industry Reference` evidence, not stakeholder
confirmation. The Specimen Management alternative documented in the
original "Alternatives Considered" section below remains a live,
unresolved competing hypothesis and is not superseded by this amendment.

## Context

Constitution Section 46 (Open Questions, item 14) and `.claude/context/
open-questions.md` item 14 have asked, since Constitution v1, "which
Bounded Context is the platform's Core Domain?" — explicitly left open
pending a dedicated DDD session. Discovery Phase 04 (Domain Discovery) ran
that session: it clustered the platform's 26 candidate Domain Events (Phase
03, Event Storming) into 11 candidate Subdomains and applied the DDD
Strategic Design/Distillation test (Core: differentiating; Supporting:
necessary but not differentiating; Generic: commodity) to each.

**Critical context this ADR cannot omit:** this entire Discovery run
executed in **Assumption-Driven Autonomous Run** mode, explicitly approved
by the user at Discovery Program start (`docs/discovery/reports/
00-discovery-program-status-report.md`) because no real stakeholder input
was available in this session. Every event, capability, and classification
feeding this proposal is tagged `Inferred — Industry Reference` in
`docs/discovery/artifacts/ASSUMPTION-REGISTER.md`, not confirmed by an
actual domain expert or business stakeholder.

## Decision

**Proposed:** the Core Domain is **Test Processing and Result
Verification** — the Bounded Context owning the `TestResult` Aggregate and
the `TestProcessingStarted → TestResultCaptured → ResultVerified →
ResultReleased` event chain.

**This is a Proposed decision, not an Accepted one**, pending user review
of the underlying Assumption Register — specifically the competing
alternative documented below.

## Alternatives Considered

- **Specimen Management (with Home Collection Logistics as the
  differentiator).** A credible, evidence-based alternative, explicitly
  documented in Phase 04's Domain Vision Statement discussion: if this
  platform's actual competitive strategy is convenience/access-led (a lab
  that makes home collection seamless and reliable) rather than
  clinical-accuracy-led, Specimen Management — specifically its Home
  Collection Logistics slice — could be Core instead. **This alternative
  was not ruled out by evidence; it was left unresolved because no real
  business-strategy input exists in this session** (Risk #6,
  `docs/discovery/artifacts/RISK-REGISTER.md`).
- **Order Management.** Rejected with higher confidence: test ordering is
  well-evidenced as necessary but not differentiating (Supporting) — every
  competing lab in the industry performs this function similarly; it does
  not carry the platform's distinguishing value.
- **Billing and Claims.** Rejected with high confidence: built on the
  weakest-evidenced Value Stream (VS4) in the entire Discovery run and is a
  textbook Generic/Supporting function (necessary, not differentiating) in
  virtually every healthcare business model.

## Why Proposed, Not Accepted

Constitution Section 39 requires an ADR before a decision is treated as
Accepted — that much is satisfied by this document existing. But
Constitution Section 3's No-Guessing Rule (`CLAUDE.md`) requires that
nothing be asserted as settled fact without either explicit user statement
or existing Confirmed context. The evidence behind this proposal is
`Inferred — Industry Reference`, generated without live stakeholder access,
under an explicitly user-approved *Discovery-execution* mode — but that
approval was for **how Discovery would run**, not a standing approval to
treat its *conclusions* as Accepted architecture. Marking this ADR
`Accepted` would let an assumption-driven finding silently graduate to
governing-rule status, exactly the failure mode this project's entire
Constitution and Context Store discipline exists to prevent. It is
`Proposed` until the user reviews this specific finding (and ideally
resolves the Specimen Management alternative) and explicitly promotes it.

## Positive Consequences (if ultimately Accepted)

- Concentrates deepest modeling investment where DDD Strategic Design
  practice suggests it belongs, per the evidence gathered.
- Resolves a question that has been open since Constitution v1, giving the
  future SAD a concrete starting hypothesis rather than an empty field.
- The competing alternative is documented, not lost — if the user's real
  answer is "actually, convenience is our differentiator," that
  redirection is a one-ADR change (superseding this one), not a
  from-scratch rediscovery.

## Negative Consequences

- If wrong, deepest early modeling investment could go to the wrong
  Subdomain, requiring rework once the correct Core Domain is confirmed.
- Leaves the platform's actual competitive strategy question unanswered —
  this ADR narrows the DDD classification exercise but cannot substitute
  for the business-strategy input that would truly settle it.

## Risks

- **Primary risk:** treating this Proposed ADR as if it were Accepted in a
  future SAD session, skipping the user-confirmation step. Mitigated by
  the explicit `Status: Proposed` and this document's own "Why Proposed"
  section — any reader consuming this ADR is told directly not to treat it
  as settled.

## Verification

- User reviews `docs/discovery/artifacts/ASSUMPTION-REGISTER.md` entries
  #10–11 and `RISK-REGISTER.md` #6, and either confirms this proposal,
  selects the Specimen Management alternative, or defers the question
  further.
- Once confirmed, this ADR's Status is updated to `Accepted` via the normal
  Constitution Section 45 Amendment/Section 39 ADR process — not by
  silently editing this file's Decision section (Constitution Section
  39's "never edit an Accepted ADR" rule extends in spirit to not silently
  editing a Proposed one into Accepted without the actual confirmation
  step happening).

## Revisit Triggers

- User provides real business-strategy input confirming or overriding this
  proposal.
- Real Event Storming with actual domain experts materially changes the
  Subdomain map from Phase 04's Inferred version.
- The Specimen Management alternative gains stronger evidence than this
  proposal.

## Revisit Triggers — Added by Gap Closure Wave 14 Amendment

- User confirms, narrows, or rejects the "Patient-to-Result Orchestration"
  reframing specifically (independent of the original Test Processing and
  Result Verification framing it broadens).
- Real workflow evidence for Patient/Doctor domains (currently `Inferred`,
  Gap Closure Wave 5) materially changes their relationship to the
  differentiating event chain.
