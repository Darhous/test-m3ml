# 0011: Core Domain — Test Processing and Result Verification

## Status

**Proposed** — *not* Accepted. See "Why Proposed, Not Accepted" below. This
deliberately deviates from `docs/discovery/prompts/12_FINAL_DISCOVERY_BOOK.md`'s
default instruction to mark a Phase-11-validated finding `Accepted`; the
deviation is intentional and explained, not an oversight.

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
