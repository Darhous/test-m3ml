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
| 106-Feature Build-vs-Buy decisions — 106 architecturally resolved, 0 architectural blockers (105 with a Final Decision, 1 — `home-collection-logistics` — unblocked 2026-07-18, classification pending an implementation-level micro-assessment, not an architectural gap) | `docs/reuse/MASTER_DECISION_REGISTER.md`, `MASTER_BUILD_VS_BUY_MATRIX.md` | `01-FULL-ENTERPRISE-AUDIT.md` §8 — Sound |
| Technology Baseline (33 entries — 21 Engines frozen at EARB + 3 added 2026-07-18: Kong Gateway, OpenBao, PostgreSQL) | `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` | `08-LICENSING-CERTIFICATION.md` — PASS |
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
6. ✅ **Eramba Community governance status** (R-01) — **Resolved**:
   conditionally approved Version 1 selection, **not** SAD-authoring
   work. **Corrected 2026-07-18 (Final Pre-SAD Semantic
   Consistency Correction):** Eramba is the conditionally approved
   Version 1 GRC/Compliance selection; the SAD documents that selection,
   its constraints, and its due-diligence gate, but does not compare or
   select a replacement product. The genuine remaining Dependency is
   narrower than originally framed: implementation-time due diligence
   (license verification, security/maintenance assessment, deployment
   fit, operational ownership, exit-strategy validation) before
   production adoption — see `docs/architecture-review/
   02-TECHNOLOGY-BASELINE.md` E5 and `26-FINAL-SEMANTIC-CONSISTENCY-
   CLOSURE.md`.
7. **Infrastructure product selections** — all resolved:
   - ✅ **API Gateway**: Kong Gateway (Apache-2.0), D-44. **Approved
     Version 1 selection, not subject to architectural re-evaluation
     during SAD authoring — see `22-ARCHITECTURE-BASELINE-FREEZE.md`'s
     Governance Statement.** Subject only to implementation due
     diligence.
   - ✅ **Secrets/Vault**: OpenBao (MPL-2.0), D-45. Same governance
     status as Kong Gateway above.
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
11. ✅ **PostgreSQL as primary relational database** — **Resolved
    2026-07-18** (Pre-SAD Baseline Correction): ADR-0013 Accepted.
    Closes the Data Architecture gap `23-SAD-READINESS-MATRIX.md`
    identified at the Architecture Readiness Review. *(New item, not in
    the original 10 — added because the ARR discovered this gap after
    the original list was written.)*
12. ✅ **Disaster Recovery baseline** — **Resolved 2026-07-18**
    (Pre-SAD Baseline Correction): ADR-0014 Accepted — 4-tier
    criticality classification, backup/recovery/governance principles;
    numeric RPO/RTO honestly labeled Pending, not fabricated. Closes
    the sole Missing-Inputs finding `23-SAD-READINESS-MATRIX.md`
    identified. *(New item, same reason as #11.)*

**8 of 12 items resolved** (updated 2026-07-18, Final Pre-SAD Semantic
Consistency Correction — item 6/Eramba governance status added to the
resolved set). **All 6 formal Certification Conditions satisfied**
(items 1, 2, 4-partially via explicit non-closure, 7×2, 9 — item 4/AGPL
remains the one formal Condition still open, a genuine Legal Dependency
this Board cannot close). **Both gaps discovered at the Architecture
Readiness Review (items 11-12) are also now closed.**

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
carrying forward the AGPL Legal Dependency. Kong Gateway and OpenBao
(item 7) are approved product selections the SAD must treat as fixed
input, not re-evaluate.
