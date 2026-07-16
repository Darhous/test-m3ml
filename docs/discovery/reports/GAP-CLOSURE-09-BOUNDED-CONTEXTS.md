# Gap Closure Wave 9 — Bounded Context Remapping

**Skills used:** `domain-driven-design` (full Context Mapping pattern
suite applied — Customer/Supplier, Partnership, ACL, Open Host Service —
including one new pattern, Partnership, not used in the Baseline),
`c4-architecture`/`mermaid-diagrams` (tiered Context Map diagram).

## Executive Summary

Remapped from the Baseline's 8 Bounded Contexts to 28, each individually
justified (business language/ownership/lifecycle/evidence). Rejected a
29th candidate ("Integration Hub") on evidence grounds rather than
including it by default. Built a 3-option Decision Matrix for ADR 0012
(Retain 8 / Expand to 28 / Hybrid-tiered) and recommends the Hybrid option
as most honest given the evidence-distribution reality Wave 3 already
established.

## Findings

- The Modeled/Recognized tiering directly operationalizes Wave 3's
  evidence-distribution finding at the architecture-boundary level, not
  just the capability level — the same 9 contexts that trace to real
  events/aggregates are exactly the ones marked "Modeled."
- "Integration Hub" being rejected (not merely unaddressed) is itself a
  finding worth surfacing — distributed integration ownership per
  consuming context, already established in the Baseline, holds up under
  enterprise-scale scrutiny rather than needing a centralizing context.
- The acyclic graph property survives the expansion from 8 to 28 contexts
  without modification to the Core Platform rule — a positive
  architectural-stability signal.

## Decisions

None Accepted — Recommended disposition for ADR 0012 stated, formally
decided at Wave 14.

## Open Questions

None new — this Wave organizes existing evidence into contexts; it
doesn't surface new unknowns beyond what Waves 3–7 already logged.

## Risks

The 19 "Recognized" contexts being treated as equally solid as the 9
"Modeled" ones by a future reader is the primary risk this Wave's tiering
exists to prevent — carried to Wave 12/13 as a documentation-discipline
item, not a security risk per se.

## Assumptions

All 19 "Recognized" context justifications are `Inferred`; the 9
"Modeled" ones inherit their existing Evidenced status from the Baseline/
Wave 5 — no new assumption category needed.

## Files Updated

- `docs/discovery/artifacts/W9-bounded-context-remapping.md` (created)
- `docs/discovery/diagrams/W9-context-map-enterprise.md` (created)
- `.claude/context/module-catalog.md` (Wave 9 pointer appended, existing
  content preserved)

## Review Checklist

- [x] Every one of the 28 candidate contexts justified individually — none
      accepted by default.
- [x] 1 candidate (Integration Hub) explicitly evaluated and rejected,
      not silently dropped.
- [x] Every relationship in the Context Mapping table has a named DDD
      pattern.
- [x] Acyclic graph property re-verified at the larger scale.
- [x] No Shared Kernel adopted without justification (none needed, same
      as Baseline).
