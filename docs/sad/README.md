# Software Architecture Document (SAD) — Index

**Document Status:** Review (this README) — see Section 12 of Wave 1 for
the full governance rule this status follows.

## What this is

This is the Software Architecture Document for the digital healthcare
platform (`darhous/test-m3ml`), authorized to begin authoring on
2026-07-18 (`docs/certification/26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md`,
verdict: **CLEAN SEMANTIC BASELINE — READY FOR SOFTWARE ARCHITECTURE
DOCUMENT**).

Per `docs/constitution/PROJECT-CONSTITUTION.md` §1: the SAD is **not**
the Constitution and does not restate or reinterpret its governing
rules. The SAD describes *how* the platform is built to satisfy those
rules — it is authored strictly downstream of the Constitution, the 14
Accepted ADRs (`docs/adr/`), the frozen Technology Baseline
(`docs/architecture-review/02-TECHNOLOGY-BASELINE.md`), the Unified
Decision Register (`docs/certification/10-DECISION-REGISTER.md`), the
Unified Risk Register (`docs/certification/11-RISK-REGISTER.md`), and
the API Platform Strategy (`docs/api-platform/`).

## Approved Wave Structure

Adopted 2026-07-20, superseding the 11-wave scaffold originally proposed
during the pre-SAD workstation audit. This structure is now the official
plan for authoring the SAD and is not to be renegotiated unless a real
architectural conflict is discovered during execution.

| Wave | Title | Status |
|---|---|---|
| 1 | Introduction, Goals, Constraints & Stakeholders | **Accepted** — drafted 2026-07-20; Corrective Review verdict PASS (§17.2 of the Wave 1 document); formally **Accepted by the Project Owner on 2026-07-20** following Independent Architecture Review, satisfying gate condition 3 below |
| 2 | Context & Scope | **Accepted** — drafted 2026-07-20; Corrective Review self-verdict PASS (`02-context-and-scope.md` §19, commit `db2ee66`); formally **Accepted by the Project Owner on 2026-07-20** following Independent Architecture Review, satisfying gate condition 3 below (see `02-context-and-scope.md` §20 Acceptance Record) |
| 3 | Solution Strategy | **Accepted** — drafted 2026-07-20; self-review verdict PASS (`03-solution-strategy.md` §25, commit `1f8482f`); Independent Architecture Review found one narrow semantic erratum, corrected and re-verified (`03-solution-strategy.md` §26, commit `b4c341e`); formally **Accepted by the Project Owner on 2026-07-20** following that erratum's closure, satisfying gate condition 3 below (see `03-solution-strategy.md` §27 Acceptance Record) |
| 4 | Building Block View | **Accepted** — drafted 2026-07-20; self-review verdict PASS (`04-building-block-view.md` §26, commit `7377d9e`); Independent Architecture Review found 10 narrow semantic issues, corrected and re-verified (`04-building-block-view.md` §26 Erratum Note, commit `9cf0729`); formally **Accepted by the Project Owner on 2026-07-20** following that erratum's closure, satisfying gate condition 3 below (see `04-building-block-view.md` §27 Acceptance Record) |
| 5 | Runtime View | **Accepted** — drafted 2026-07-20; self-review verdict PASS (`05-runtime-view.md` §18, commit `17e1f80`); Independent Architecture Review found 10 narrow semantic issues, corrected and re-verified (`05-runtime-view.md` §19, commit `38e1558`); formally **Accepted by the Project Owner on 2026-07-20** following that erratum's closure, satisfying gate condition 3 below (see `05-runtime-view.md` §20 Acceptance Record) |
| 6 | Deployment View | **Accepted** — drafted 2026-07-20; self-review verdict PASS (`06-deployment-view.md` §41, 3-pass Reader Testing, 28 Gates A–AB); Independent Architecture Review found 7 narrow semantic issues, corrected and re-verified (`06-deployment-view.md` §42, commit `8db7341`); formally **Accepted by the Project Owner on 2026-07-21** following that erratum's closure, satisfying gate condition 3 below (see `06-deployment-view.md` §43 Acceptance Record) |
| 7 | Security, Privacy & Trust Boundaries | Not started |
| 8 | Multi-Tenancy, Identity & Access Governance | Not started |
| 9 | AI Governance, Device Integration & Other Cross-Cutting Concerns | Not started |
| 10 | Architecture Decisions & Traceability | Not started |
| 11 | Quality Requirements & Quality Scenarios | Not started |
| 12 | Risks, Technical Debt & Evolution | Not started |
| 13 | Glossary, Consistency Review & Final Close-out | Not started |

## Inter-Wave Gate (Required, not optional)

A Wave may begin **only after every one of the following is true for
the immediately preceding Wave**:

1. **Completed** — its full required content, per this table, has been
   authored.
2. **Reviewed** — a consistency/terminology/full-source review has been
   performed on it (see that Wave's own Review Report section) and
   produced a verdict of `PASS` or `PASS WITH CONDITIONS` with the
   conditions explicitly tracked, not silently dropped.
3. **Explicitly Accepted by the project owner** (today's sole
   Architecture Review Board authority, Constitution §57) — a review
   verdict of `PASS` from the author/reviewer is **not** the same thing
   as project-owner Accepted approval, and does not by itself authorize
   starting the next Wave. The project owner must say so explicitly.
4. **Committed** to the local `main` branch.
5. **Pushed** to `origin/main`.

**A commit by itself — even a pushed one — does not satisfy this gate.**
All five conditions must hold; the first Wave found not satisfying all
five blocks every subsequent Wave from starting, regardless of how much
work exists in the pipeline behind it.

This gate was corrected 2026-07-20 (Wave 1 Corrective Review) — the
original wording only required a commit, which is insufficient and was
itself the reason Wave 1's initial `PASS` self-review was not accepted
as authorization to proceed.

## Files

| File | Wave | Content |
|---|---|---|
| `01-introduction-goals-constraints-stakeholders.md` | 1 | Purpose, objectives, audience, goals, stakeholders, constraints, assumptions, out-of-scope, governance |
| `02-context-and-scope.md` | 2 | System of Interest, business context, system boundary, actors, external systems, bounded-context landscape at scope level, functional/current/target/future scope, integration context, data responsibility boundaries, out-of-scope, context diagram specification, scope decision rules |
| `03-solution-strategy.md` | 3 | Executive Solution Strategy, Domain Vision Statement, Architectural Drivers, Strategy Pillars (architecture style, DDD, Clean/Hexagonal, communication, API, data, multi-tenancy/IAM, reuse, device, AI, deployment, auditability, evolution), trade-offs, rejected alternatives, explicit non-decisions, open dependencies, traceability matrix, wave boundary map |
| `04-building-block-view.md` | 4 | Level-0/1/2 building blocks, BC-to-Module Mapping Matrix (28 contexts), Independent-Capable Components Catalog, Core Platform white box, Engine Adoption-Point Mapping, dependency model, diagrams |
| `05-runtime-view.md` | 5 | Universal Runtime Invariants, 12 runtime scenarios (order-to-release, device ingestion/failure, notification, billing/insurance, AI assistance, FHIR/partner, background work), interaction catalog, transaction/consistency boundaries, idempotency, error/failure matrix, audit/provenance, state-transition coverage, sequence diagrams |
| `06-deployment-view.md` | 6 | Deployment Unit Classification Matrix, Baseline/SaaS/Dedicated-DB/Dedicated-Deployment/On-Prem/Hybrid archetypes, Independent Components and Engine placement, data/backup/DR topology (ADR-0014), failure domains, deployment diagrams (C4Deployment), open deployment decisions |

## Traceability

- Validated inputs this document set inherits as fixed:
  `docs/certification/15-SAD-INPUT-PACKAGE.md`
- Section-by-section input readiness: `docs/certification/23-SAD-READINESS-MATRIX.md`
- Full decision history: `docs/certification/10-DECISION-REGISTER.md`
- Full risk history: `docs/certification/11-RISK-REGISTER.md`
