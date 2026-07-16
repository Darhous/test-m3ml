# Phase 04 — Domain Discovery Report

**Execution mode:** Assumption-Driven Autonomous Run.
**Skills applied:** `domain-driven-design` (Strategic Design/Distillation),
`doc-coauthoring` (reader test).

## Executive Summary

Clustered Phase 02/03 output into 11 candidate Subdomains (1 Core, 7
Supporting, 3 Generic), proposed "Test Processing and Result Verification"
as the answer to Open Question #14 (Core Domain) with an explicitly-flagged
competing alternative, and documented divergence from `module-catalog.md`'s
16 existing categories rather than silently overwriting them.

## Findings

- 8 of 11 Subdomains have Strong/Medium evidence (traced to real Event
  Storming events); 3 (Inventory, QC/Accreditation, Staff/Operations) rest
  on Phase 02 capability names alone — explicitly flagged as low-confidence.
- The "Laboratory Modules" category in `module-catalog.md` appears too
  coarse — evidence splits it into 3 distinct Subdomains (Order Management,
  Specimen Management, Test Processing & Result Verification), each with a
  different Core/Supporting classification, which would be lost if treated
  as one category.
- "Insurance Modules" (a separate `module-catalog.md` category) was folded
  into "Billing and Claims" in this pass — flagged as a divergence needing
  re-examination once `open-questions.md` #17 is answered, not asserted as
  final.

## Decisions

None (Playbook 04 proposes, does not decide — Constitution Section 39
ADR-before-Accepted applies).

## Open Questions

`open-questions.md` #14 updated with a Proposed (not Accepted) answer.
No new numbered item added this phase — the Core Domain question already
existed; this phase narrowed it with evidence.

## Risks

2 new entries (`RISK-REGISTER.md` #5–6): weak-evidence Subdomains, and an
unresolved competing Core Domain hypothesis.

## Assumptions

3 new entries (`ASSUMPTION-REGISTER.md` #10–12).

## Missing Information

- Real evidence for Inventory, QC/Accreditation, and Staff/Operations
  Subdomains (Phase 02/03 traced no Value Stream touching them).
- Real business-strategy input to resolve the Core Domain competing
  hypothesis (clinical-accuracy-led vs. convenience/access-led
  differentiation).

## Recommendations

- Before Phase 06 finalizes Bounded Context boundaries, prioritize closing
  the Core Domain question with real user input if at all possible — it
  materially affects where deep modeling investment is directed.
- Treat Subdomains #9–11 as placeholders in Phase 05/06, not as settled
  boundaries — revisit if any later phase surfaces real evidence for them.

## DDD Consistency Review (Quick Diagnostic, partial — expected at this
phase)

| Diagnostic Row | Result | Note |
|---|---|---|
| Can a domain expert read the names and understand them? | PASS | All 11 Subdomain names are business-language. |
| Are Bounded Context boundaries explicitly defined? | N/A — not yet | Phase 06's job; premature to score here. |
| Are Aggregates small? | N/A — not yet | Phase 05's job. |
| Do domain objects contain behavior? | N/A — not yet | Phase 05's job. |
| Are Domain Events used for cross-aggregate communication? | Partial | Events identified (Phase 03) but not yet wired to Aggregates. |
| Is there an ACL at every external integration? | Pending | Flagged for Device (#7) and future AI (Phase 10); not designed yet. |
| Has the Core Subdomain been identified? | PASS (Proposed) | See Core Domain proposal above. |

Full diagnostic re-score happens in Phase 06 (once Bounded Contexts exist)
and again in Phase 11 (cross-phase).

## Review Checklist (per Playbook 04)

- [x] Every Subdomain traces to specific events/capabilities — none
      invented without an evidentiary trail (weak-evidence ones explicitly
      labeled as such, not hidden).
- [x] Every Core classification has a written Domain Vision Statement.
- [x] Divergence from `module-catalog.md`'s 16 categories explicitly noted.
- [x] No classification asserts/implies a microservice-extraction decision.

## Quality Gates

- **DDD Consistency Review:** PASS (partial, as expected at this phase —
  see table above).
- **Evidence Gate:** PASS — the one Core classification has a full Domain
  Vision Statement citing specific evidence; no Core classification was
  made without one.

## Exit Criteria Confirmation

- [x] Every Subdomain from Phase 02/03 evidence is classified (weak-
      evidence ones explicitly marked, not silently dropped).
- [x] A Proposed answer to Open Question #14 exists with evidentiary basis.

## Files Updated

- `.claude/context/open-questions.md` (item 14 annotated with Proposed
  answer)
- `.claude/context/glossary.md` (Discovery Phase 04 section, 5 new Draft
  terms)
- `docs/discovery/artifacts/ASSUMPTION-REGISTER.md`, `RISK-REGISTER.md`
  (updated)

## ADR Impact

Potentially significant (per Playbook 04's own note): if the Core Domain
proposal survives Phase 11 Validation unchanged, Phase 12 authors an ADR
formalizing it. Not authored here.
