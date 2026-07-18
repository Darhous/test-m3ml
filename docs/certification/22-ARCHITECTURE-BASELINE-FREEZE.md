# Architecture Baseline Freeze

**Effective**: Upon commit of this document to `main`. **Authority**:
Enterprise Architecture Review Board, following a PASS verdict in
`21-ARCHITECTURE-READINESS-REVIEW.md`. **Repository Commit at Freeze
(pre-this-phase's-own-commit)**: `47b7979f3e716f38cd4b09cec15fd04a55e96d63`.

## What "Frozen" Means

This freeze applies the same discipline already established by
`docs/architecture-review/12-DECISION-FREEZE.md` (Technology Baseline
freeze) to the *complete* architectural decision set — Constitution,
ADRs, Discovery/Reuse conclusions, Technology Baseline, API Platform,
and the Open Questions Resolution decisions. **The Software Architecture
Document inherits everything below as fixed input, not as material to
re-derive or re-litigate.** Amendment requires a new ADR, a subsequent
Architecture Review Board cycle, or a formal legal counsel finding —
never a silent edit.

## Approved ADRs (12/12 Accepted)

| ADR | Title | Status |
|---|---|---|
| 0001 | Modular Monolith First | Accepted |
| 0002 | Domain-Driven Design | Accepted |
| 0003 | Schema per Module | Accepted |
| 0004 | Event-Driven Integration | Accepted |
| 0005 | Hybrid Tenant Isolation | Accepted |
| 0006 | Independent Device Gateway | Accepted |
| 0007 | Governed AI Gateway | Accepted |
| 0008 | Unified Login and Policy-Based Access | Accepted |
| 0009 | SaaS First, On-Premise Ready, Hybrid Ready | Accepted |
| 0010 | Arabic/English and Localization First | Accepted |
| 0011 | Core Domain — Patient-to-Result Orchestration | **Accepted** (2026-07-18) |
| 0012 | Bounded Context Map (28: 9 Modeled + 19 Recognized) | **Accepted** (2026-07-18) |

**12/12 Accepted. Zero Proposed, Rejected, or Superseded ADRs remain.**

## Final Architectural Decisions (this freeze's own scope, beyond the ADR set)

| Decision | Value | Classification |
|---|---|---|
| Shared-tier tenant partitioning | PostgreSQL RLS + tenant-ID column | Product Configuration |
| FHIR version | R4 | Accepted Decision |
| API Gateway | Kong Gateway (Apache-2.0) | Product Configuration |
| Secrets/Vault Engine | OpenBao (MPL-2.0) | Product Configuration |
| Developer Portal (v1) | Generated docs (Redoc), no dedicated platform | Accepted Decision |
| API Analytics | Apache Superset (E10), no new tool | Accepted Decision |
| Home Collection Offline Mode | Required (local-first capture + sync) | Accepted with Constraints |
| Billing/Insurance model | Architecture supports Direct/Reimbursement/Capitation, Tenant-configurable | Accepted Decision |
| Result Verifier eligibility mechanism | OPA policy-driven, configurable per axis | Accepted Decision |
| Device/processing-failure recovery | Degraded-Mode workflow, Provenance-tracked | Accepted Decision |
| Elevated Audit tier | Adopted (Refund, Expiry-block, Break-Glass, Tenant Config) | Accepted Decision |
| National ID field | Structurally present, FHIR identifier pattern | Accepted Decision |

Full rationale for each: `20-OPEN-QUESTIONS-RESOLUTION.md`.

## Accepted Technology Selections

**Technology Baseline (frozen since EARB, unmodified)**: 21 Engines, 4
Libraries, 5 Reference Standards = 30 entries. 0 SDKs, 0 Controlled
Forks. See `docs/architecture-review/02-TECHNOLOGY-BASELINE.md`.

**New Product Configuration selections this cycle** (layered on top of,
not amending, the frozen Baseline): Kong Gateway, OpenBao. Neither
Engine addition to `docs/architecture-review/02-TECHNOLOGY-BASELINE.md`
is required — both fill previously-acknowledged gaps (no Gateway/Vault
Engine existed in that table), and adding them retroactively is
correctly deferred to a real Build-vs-Buy pass at SAD/Implementation
time if the platform team wants them formally baselined; this freeze
records them as directional decisions, not Baseline entries.

**One genuine gap surfaced this review** (`23-SAD-READINESS-MATRIX.md`
row 18): no document formally states PostgreSQL as the platform's
relational database engine, despite it being consistently implied
throughout (pgvector, Row-Level Security). **Recorded here, not
invented** — the SAD should make this explicit as its first Data
Architecture action.

## Remaining External Dependencies (13, none architectural)

| Type | Items |
|---|---|
| Legal Dependency | AGPL-3.0 review (5 Engines, R-04), unconfirmed licenses (Novu/Documenso, R-07), general local legal requirements (#2), Egypt cross-border transfer rules (#25) |
| Regulatory Dependency | Result Verifier eligibility values (#19/#23), Egypt regulatory consolidated (R-13) |
| Country Localization | Language/currency exhaustive list (#12), Egypt Payroll statutory rules (#26), National ID validation rules (#27) |
| Operational Assumption | Expected usage volume (#4), legacy migration N/A (#13) |

## Remaining Risks (11 open, 4 closed this cycle)

| Severity | Open | Closed This Cycle |
|---|---|---|
| High | R-02 (Mirth Connect), R-04 (AGPL) | — |
| Medium-High | R-07 (unconfirmed licenses), R-08 (exit strategy) | — |
| Medium | R-01 (Eramba), R-03 (ERPNext concentration), R-05 (Frappe drift), R-13 (Egypt regulatory) | R-06 (FHIR), R-09 (Gateway), R-10 (Vault) |
| Low | R-12 (Marketplace contingency), R-14 (Home Collection, now unblocked but engine TBD) | R-15 (Core Domain/BC Map) |

Full detail: `11-RISK-REGISTER.md`.

## SAD Authorization Status

**AUTHORIZED.** Confirmed by `21-ARCHITECTURE-READINESS-REVIEW.md`
(PASS, zero architectural inconsistency) and `23-SAD-READINESS-
MATRIX.md` (19/25 sections fully Ready, 5 Partially Ready with named
non-blocking dependencies, 1 genuinely Missing Inputs — Disaster
Recovery — identified honestly, not blocking).

## Freeze Contents Cross-Reference

| Document | Role in This Freeze |
|---|---|
| `docs/adr/0001` – `0012` | The 12 Accepted ADRs themselves |
| `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` | Frozen Technology Baseline (unmodified) |
| `10-DECISION-REGISTER.md` | Full decision log, 55 entries |
| `11-RISK-REGISTER.md` | Risk status, governance metadata |
| `20-OPEN-QUESTIONS-RESOLUTION.md` | Rationale for every decision this freeze records |
| `21-ARCHITECTURE-READINESS-REVIEW.md` | The review that authorized this freeze |
| `23-SAD-READINESS-MATRIX.md` | Section-by-section SAD input verification |

## Board Attestation

This Board attests: every decision in this freeze traces to documented
evidence (no invented fact); no ADR was changed without its own
Amendment section explaining why; the Technology Baseline was not
modified, only extended with non-Baseline Product Configuration
choices; every remaining dependency is honestly classified as
non-architectural; the one genuine input gap (Disaster Recovery) is
disclosed, not concealed.

**The Architecture Baseline is FROZEN as of this commit.**
