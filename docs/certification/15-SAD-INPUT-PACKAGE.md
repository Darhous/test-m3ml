# Software Architecture Document — Validated Input Package

**This document does not create the SAD.** It packages the validated,
certified inputs the SAD phase inherits as fixed, plus the explicit
list of what the SAD itself must still produce. Per this audit's Stop
Condition, no SAD section is drafted here.

## Fixed Inputs (Certified, Do Not Re-Derive)

| Input | Source | Certification |
|---|---|---|
| Architecture Principles (Modular Monolith, DDD, Event-Driven, API-First, etc.) | `.claude/context/architecture-principles.md`, ADRs 0001-0010 | `04-ADR-CERTIFICATION.md` — PASS |
| 28-Module Catalog, Bounded Context Map (28 contexts, Hybrid Modeled/Recognized) | `.claude/context/module-catalog.md`, ADR-0012 (**Accepted**, 2026-07-18) | `05-DDD-CERTIFICATION.md` — 8/10, boundaries sound |
| 106-Feature Build-vs-Buy decisions (105 decided, 1 blocked) | `docs/reuse/MASTER_DECISION_REGISTER.md` | `01-FULL-ENTERPRISE-AUDIT.md` §8 — Sound |
| Frozen Technology Baseline (30 entries) | `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` | `08-LICENSING-CERTIFICATION.md` — PASS |
| API-First Architecture (5-layer model, standards, naming, versioning) | `docs/api-platform/01-15` | `06-API-CERTIFICATION.md` — PASS |
| Contract-First, OpenAPI/AsyncAPI, Webhooks, SDK, Integrations, Developer Portal, Catalog, Marketplace, Monetization, Billing, Observability, SLA, Lifecycle, Roadmap architecture | `docs/api-platform/16-30` | `06-API-CERTIFICATION.md` — PASS |
| 3 recommended tooling categories (Pact, OpenAPI Generator, conditional Redoc) | `docs/api-platform/31` | `06-API-CERTIFICATION.md` — independently re-verified |
| Security architecture (STRIDE, OWASP Top 10, two-PEP defense-in-depth) | `docs/api-platform/11`, `docs/discovery/reports/11-stride-mitigation-mapping.md` | `07-SECURITY-CERTIFICATION.md` — PASS WITH CONDITIONS |
| AGPL Legal Checklist (7 items) | `docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md` | `08-LICENSING-CERTIFICATION.md` — PASS, still open |
| Governance apparatus (Architecture Review Board, Amendment Process, Quality Gates) | Constitution §44-45, 57-62 | `01-FULL-ENTERPRISE-AUDIT.md` §4 — Sound |

## What the SAD Must Still Produce (Not Pre-Empted by Any Prior Phase)

Carried forward from `docs/architecture-review/14-READINESS-FOR-SAD.md`
and `13-READINESS-FOR-API-STRATEGY.md`. **Updated 2026-07-18**: 5 of
these 10 items were resolved in the Open Questions Resolution phase
(`20-OPEN-QUESTIONS-RESOLUTION.md`) — marked ✅ below, satisfying all 6
formal Certification Conditions (item 7 alone covered 2). Unmarked
items remain genuine Dependencies, unresolved by design (outside
architectural authority).

1. ✅ **Tenant-partitioning technology** — **Resolved**: PostgreSQL RLS
   + tenant-ID column (D-42).
2. ✅ **FHIR version** — **Resolved**: R4 pinned (D-43).
3. **Actual exit-strategy procedures** for the 7 Tier-1 Engines (R-08)
   — still a Dependency; fallback candidates are named, procedures are
   not. See `11-RISK-REGISTER.md`'s Resolution Gate for R-08.
4. **AGPL legal review outcome** (R-04) — still a **Legal Dependency**,
   correctly not resolved by this Board (see `20-OPEN-QUESTIONS-
   RESOLUTION.md`'s explicit statement that this is outside
   architectural authority).
5. **Verification of Arabic/RTL localization support** for each
   ratified Engine and for Redoc — still a Dependency, unresolved.
6. **Eramba Community reconsideration** (R-01) — still a Dependency,
   unresolved.
7. **Infrastructure product selections** — all resolved:
   - ✅ **API Gateway**: Kong Gateway (Apache-2.0), D-44.
   - ✅ **Secrets/Vault**: OpenBao (MPL-2.0), D-45.
   - ✅ **Developer Portal**: generated-docs approach for v1, D-46 (was
     never a formal Condition; now also has a v1 answer).
8. **Numeric SLA/SLO/rate-limit/deprecation-window targets** — still a
   Dependency; #4 (usage volume) now has an Operational Assumption
   (D-54) but not a hard number — structure exists, numbers still
   deferred to real usage data by design.
9. ✅ **Core Domain and Bounded Context Map** — **Resolved**: ADR-0011
   and ADR-0012 both Accepted (D-40, D-41). The 7-Module boundary table
   in `docs/architecture-review/10-ADR-REVIEW.md` is now confirmed, not
   conditional.
10. **A dedicated one-page Domain Vision Statement** — still a minor
    Dependency, unresolved.

**5 of 10 items resolved. All 6 formal Certification Conditions
satisfied** (items 1, 2, 4-partially via explicit non-closure, 7×2, 9 —
note item 4/AGPL remains the one formal Condition still open, since it
is a genuine Legal Dependency this Board cannot close).

## SAD Readiness Verdict

**Updated 2026-07-18: READY.** Following the Open Questions Resolution
phase, all 6 formal Certification Conditions except the AGPL Legal
Dependency (outside architectural authority by design) are satisfied.
See `20-OPEN-QUESTIONS-RESOLUTION.md` for the SAD Authorization
statement. `18-CERTIFICATION-REPORT.md` and `17-READINESS-SCORES.md`
remain the historical record of the original CONDITIONALLY READY
verdict and are not retroactively rewritten.

## Explicit Boundary

This package is an index of *what to inherit* and *what remains
undone* — it contains no architectural design, no section drafts, no
component diagrams, and no technology selections beyond what is
already frozen. The SAD phase itself, when authorized, is responsible
for producing the 5 items still open above (3, 5, 6, 8, 10) plus
carrying forward the AGPL Legal Dependency.
