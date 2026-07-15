# Playbook 09 — SaaS Platform Discovery

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 8 of 11 domain-content phases
**Depends On:** Playbook 06 (Bounded Contexts, so tenancy rules can be
applied per context), Playbook 07 (Business Rules, for tenant-scoping
implications)
**Produces For:** Playbook 11 (Validation checks tenancy findings against
Constitution Section 18–19), Playbook 12 (Final Discovery Book's platform
deployment/tenancy chapter)

---

## Purpose

Discover the concrete, platform-wide implications of the already-Accepted
Hybrid Tenant Isolation model (ADR 0005), SaaS First/On-Premise/Hybrid Ready
posture (ADR 0009), and Localization-First commitment (ADR 0010), narrowing
several still-open questions with real evidence rather than resolving them
by assumption.

## Scope

**In scope:** tenant/organization/branch data-shape implications per
Bounded Context, the shared-tier data-partitioning technique candidates
(`open-questions.md` #15), the tier-promotion path candidates
(`open-questions.md` #16), expected-scale evidence gathering
(`open-questions.md` #4), hosting-model detail narrowing
(`open-questions.md` #3), and localization implications per Bounded Context
(currency/timezone/language fields needed).

**Out of scope:** choosing an actual database product or cloud provider
(forbidden platform-wide, not just in this phase); finalizing Non-Functional
Budgets (Constitution Section 51 — this phase gathers evidence toward them,
Playbook 12/future SAD work sets them); AI-specific tenancy questions
(Playbook 10, if any arise, e.g., per-tenant AI policy).

## Inputs

- `docs/discovery/artifacts/06-bounded-contexts.md`
- `docs/discovery/artifacts/07-business-rules-catalog.md`
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 18 (Multi-Tenancy),
  Section 19 (Tenant Isolation), Section 32 (Localization), ADR 0005, ADR
  0009, ADR 0010
- `.claude/context/open-questions.md` items 1, 3, 4, 7, 8, 12, 15, 16

## Preconditions

- Playbook 06 and 07 marked complete.

## Required Skills

- `architecture-patterns` — for reasoning about tenancy data-shape patterns
  without selecting a specific database technology.
- `domain-driven-design` — to check whether any Bounded Context's tenancy
  handling reveals a boundary problem (e.g., a context that assumed
  single-tenant reasoning).

## Required Context Files

`open-questions.md`, `constraints.md`, `stakeholders.md`.

## Project Bindings (this project)

- This phase must not re-litigate Hybrid Tenant Isolation itself (ADR
  0005) — that decision is Accepted and out of scope for reversal here; the
  phase narrows its *open implementation details* only (Constitution
  Section 46 items 15–16).

## Execution Steps

1. For each Bounded Context from Playbook 06, confirm every tenant-scoped
   Aggregate carries an explicit Tenant identifier concept (Constitution
   Section 18) — flag any Aggregate from Playbook 05 that does not yet
   account for this.
2. Gather any available evidence (from the user, this conversation, or
   already-Confirmed context) toward `open-questions.md` #4 (expected
   scale) — record it as evidence, not as a finalized number; if no
   evidence exists, explicitly state so rather than estimating.
3. Narrow `open-questions.md` #15 (shared-tier data-partitioning technique)
   by listing the viable candidate techniques consistent with ADR 0005 and
   Constitution Section 3 (no database product chosen) — e.g., as
   categories like "tenant-identifier column with row-level enforcement" vs.
   "per-tenant schema within the shared database" — without naming a
   specific database product's feature.
4. Narrow `open-questions.md` #16 (tier-promotion path) by documenting what
   triggers a tenant's move from shared to dedicated tier, consistent with
   Constitution Section 55's Evolution Strategy evidence-based-trigger
   principle (no arbitrary numeric threshold invented).
5. Narrow `open-questions.md` #3 (hosting model detail) only to the extent
   the business/user provides real input in this phase — otherwise leave
   it explicitly `Open`.
6. For each Bounded Context, confirm no hardcoded locale/currency/timezone
   assumption exists in the candidate Aggregates from Playbook 05
   (Constitution Section 32) — flag any that do.
7. Cross-check every finding against ADR 0005/0009/0010's Revisit Triggers
   — if a finding would trigger a revisit (e.g., a regulatory requirement
   the two-tier model cannot satisfy), flag it explicitly rather than
   quietly reinterpreting the ADR.

## Deliverables

- Per-Context tenancy data-shape confirmation (or flagged gaps).
- Narrowed (not necessarily fully answered) positions on `open-questions.md`
  #3, #4, #15, #16.
- Localization gap list per Bounded Context.

## Produced Artifacts

- `docs/discovery/artifacts/09-tenancy-analysis.md`
- `docs/discovery/artifacts/09-localization-analysis.md`
- `docs/discovery/reports/09-saas-platform-report.md` (evidence gathered,
  remaining gaps, any ADR Revisit Trigger flags)

## Required Diagrams

- Updated Tenant Isolation diagram (Mermaid `flowchart`) reflecting real
  Bounded Contexts instead of the Constitution's illustrative Tenant A/B/C
  example, stored under `docs/discovery/diagrams/`.

## Review Checklist

- [ ] Every tenant-scoped Aggregate confirmed to carry an explicit Tenant
      identifier concept.
- [ ] `open-questions.md` items 3/4/15/16 each have either new evidence
      recorded or an explicit "no new evidence available" note.
- [ ] No database product, cloud provider, or specific technology named
      anywhere in this phase's output.
- [ ] No ADR 0005/0009/0010 Revisit Trigger condition is quietly ignored.

## Quality Gates

- **No-Guessing Gate:** every narrowing of an Open Question cites its
  evidence source (user statement, existing Confirmed context, or explicit
  "still no evidence") — no narrowing is asserted without a cited source.
- **ADR Non-Reversal Gate:** confirmed that no output of this phase
  contradicts ADR 0005/0009/0010's actual Decision text.

## Exit Criteria

- Tenancy data-shape confirmed or gapped for every Bounded Context.
- Open Questions 3/4/15/16 updated with real findings or explicit
  "still open, no new evidence."

## Files To Update

- `.claude/context/open-questions.md` — items 3, 4, 15, 16 updated with
  Discovery findings (still `Open` unless definitively answered).
- `.claude/context/constraints.md` — if a genuinely new Confirmed
  scale/tenancy constraint emerges from user input during this phase.

## ADR Impact

If the shared-tier data-partitioning *category* (not a specific product)
becomes decided with confidence during this phase, Playbook 12 may author a
new ADR narrowing ADR 0005 (a refinement, not a reversal — per ADR 0005's
own Revisit Triggers section). This playbook flags the candidate; it does
not author the ADR.

## Common Mistakes

- Naming an actual database product or cloud service while trying to
  describe a data-partitioning "category" — the category must stay
  abstract (e.g., "per-tenant schema" is fine; "using Vendor X's row-level
  security feature" is not).
- Treating a single stakeholder's guess about scale as if it were measured
  evidence.
- Re-opening ADR 0005/0009/0010's core decision instead of narrowing their
  already-open implementation details.
- Forgetting to check Aggregates for hardcoded locale assumptions because
  "localization was already decided" — the ADR fixed the *commitment*, not
  the per-Aggregate implementation detail, which is this phase's job to
  verify.

## Self Review

For each Open Question narrowed in this phase, re-read the recorded
evidence and confirm it would survive being shown to the user as "here is
exactly what you told us, restated" — not an inference dressed as a
finding.

## Stop Conditions

- A stakeholder requirement surfaces that ADR 0005/0009/0010 cannot
  satisfy even after narrowing (a genuine Revisit Trigger firing) — stop,
  do not silently work around it; escalate per Constitution Section 44/45.
- Evidence gathering for `open-questions.md` #4 (scale) would require
  guessing numbers with no real source — explicitly decline and record
  "still open," per the No-Guessing Rule.
