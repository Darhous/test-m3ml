# Software Architecture Document — Validated Input Package

**This document does not create the SAD.** It packages the validated,
certified inputs the SAD phase inherits as fixed, plus the explicit
list of what the SAD itself must still produce. Per this audit's Stop
Condition, no SAD section is drafted here.

## Fixed Inputs (Certified, Do Not Re-Derive)

| Input | Source | Certification |
|---|---|---|
| Architecture Principles (Modular Monolith, DDD, Event-Driven, API-First, etc.) | `.claude/context/architecture-principles.md`, ADRs 0001-0010 | `04-ADR-CERTIFICATION.md` — PASS |
| 28-Module Catalog, Bounded Context Map (28 contexts, Hybrid Modeled/Recognized) | `.claude/context/module-catalog.md`, ADR-0012 (Proposed) | `05-DDD-CERTIFICATION.md` — 8/10, boundaries sound |
| 106-Feature Build-vs-Buy decisions (105 decided, 1 blocked) | `docs/reuse/MASTER_DECISION_REGISTER.md` | `01-FULL-ENTERPRISE-AUDIT.md` §8 — Sound |
| Frozen Technology Baseline (30 entries) | `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` | `08-LICENSING-CERTIFICATION.md` — PASS |
| API-First Architecture (5-layer model, standards, naming, versioning) | `docs/api-platform/01-15` | `06-API-CERTIFICATION.md` — PASS |
| Contract-First, OpenAPI/AsyncAPI, Webhooks, SDK, Integrations, Developer Portal, Catalog, Marketplace, Monetization, Billing, Observability, SLA, Lifecycle, Roadmap architecture | `docs/api-platform/16-30` | `06-API-CERTIFICATION.md` — PASS |
| 3 recommended tooling categories (Pact, OpenAPI Generator, conditional Redoc) | `docs/api-platform/31` | `06-API-CERTIFICATION.md` — independently re-verified |
| Security architecture (STRIDE, OWASP Top 10, two-PEP defense-in-depth) | `docs/api-platform/11`, `docs/discovery/reports/11-stride-mitigation-mapping.md` | `07-SECURITY-CERTIFICATION.md` — PASS WITH CONDITIONS |
| AGPL Legal Checklist (7 items) | `docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md` | `08-LICENSING-CERTIFICATION.md` — PASS, still open |
| Governance apparatus (Architecture Review Board, Amendment Process, Quality Gates) | Constitution §44-45, 57-62 | `01-FULL-ENTERPRISE-AUDIT.md` §4 — Sound |

## What the SAD Must Still Produce (Not Pre-Empted by Any Prior Phase)

Carried forward and consolidated from `docs/architecture-review/
14-READINESS-FOR-SAD.md` and `13-READINESS-FOR-API-STRATEGY.md`, now
cross-checked against this audit's own Open Questions Register
(`12-OPEN-QUESTIONS-REGISTER.md`) for completeness.

**Marker key** (added this closure pass): ⚑ = also one of the 6 formal
Certification Conditions in `18-CERTIFICATION-REPORT.md`. Unmarked
items are tracked SAD-input Dependencies the SAD must still produce,
but are **not** formal conditions of this certification's PASS WITH
CONDITIONS verdict.

1. ⚑ **The tenant-partitioning technical decision** (Open Question
   #15) — Technology Baseline provides evidence (R4, PostgreSQL RLS),
   not the decision.
2. ⚑ **A pinned FHIR version** (R-06) — R4 is the evidence-weighted
   default, not an asserted Decision.
3. **Actual exit-strategy procedures** for the 7 Tier-1 Engines (R-08)
   — fallback candidates are named, procedures are not. (Dependency,
   not a formal Condition — see `11-RISK-REGISTER.md`'s Resolution
   Gate for R-08.)
4. ⚑ **Resolution or explicit carry-forward of the AGPL legal review
   outcome** (R-04) into the SAD's own dependency documentation.
5. **Verification of Arabic/RTL localization support** for each
   ratified Engine (ADR-0010 gap) and specifically for Redoc
   (`docs/api-platform/31`'s conditional recommendation). (Dependency,
   not a formal Condition.)
6. **A decision on the Eramba Community reconsideration** (R-01) — the
   SAD is the appropriate venue for the focused re-scan every prior
   phase has declined to perform. (Dependency, not a formal Condition.)
7. **Infrastructure product selections**, two of which are formal
   Conditions and one of which is not:
   - ⚑ **API Gateway** (Open Question #28) and ⚑ **Secrets/Vault**
     (Open Question #29) — each via a scoped Build-vs-Buy micro-
     assessment, not a full program re-run.
   - **Developer Portal** (Open Question #30) — **not a formal
     Certification Condition.** Medium priority, entangled with and
     lower-urgency than #28; recommended on the same evaluation
     timeline for efficiency, but its resolution does not gate this
     certification's verdict. See `18-CERTIFICATION-REPORT.md`'s
     "Formal Certification Conditions vs. Additional SAD Section
     Finalization Dependencies" section for the full reasoning.
8. **Numeric SLA/SLO/rate-limit/deprecation-window targets** (Open
   Question #4-dependent) — structure exists (`docs/api-platform/
   07, 13, 28`), numbers do not. (Dependency, not a formal Condition —
   #4 is Critical-priority but is not itself one of the 6 formal
   Conditions, since no SAD section can be finalized against it until
   real usage data exists regardless of any certification verdict.)
9. ⚑ **Core Domain and Bounded Context Map final resolution** (Open
   Question #14, ADR-0011/0012) — **the single highest-impact open
   item**; if the SAD proceeds without this resolved, it must explicitly
   document which Module boundaries are contingent on the eventual
   answer (the 7-Module table in `docs/architecture-review/
   10-ADR-REVIEW.md` names them precisely).
10. **A dedicated one-page Domain Vision Statement** for the Core
    Domain candidate — currently folded into `.claude/context/
    vision.md` rather than existing as its own artifact (minor,
    `05-DDD-CERTIFICATION.md` finding). (Dependency, not a formal
    Condition.)

## SAD Readiness Verdict

**CONDITIONALLY READY**, consistent with and formally re-confirming
every prior readiness assessment in this repository. See
`18-CERTIFICATION-REPORT.md` for the full certification decision and
`17-READINESS-SCORES.md` for quantified scores.

## Explicit Boundary

This package is an index of *what to inherit* and *what remains
undone* — it contains no architectural design, no section drafts, no
component diagrams, and no technology selections beyond what is
already frozen. The SAD phase itself, when authorized, is responsible
for producing all 10 items above.
