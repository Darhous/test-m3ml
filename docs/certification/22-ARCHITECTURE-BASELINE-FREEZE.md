# Architecture Baseline Freeze

**Effective**: Upon commit of this document to `main`. **Authority**:
Enterprise Architecture Review Board, following a PASS verdict in
`21-ARCHITECTURE-READINESS-REVIEW.md`. **Original Freeze Commit**:
`47b7979f3e716f38cd4b09cec15fd04a55e96d63` (Architecture Readiness
Review). **Updated 2026-07-18 (Pre-SAD Baseline Correction, starting
baseline commit `d152320533247ddf13c518a422411f07e5ddfd57`)**: this is
now Freeze v2 — corrects the Feature-decision count, clarifies Kong/
OpenBao governance, and adds ADR-0013 (PostgreSQL) and ADR-0014
(Disaster Recovery). Nothing in v1 was reversed; this is an extension,
not a revision of substance.

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

## Approved ADRs (14/14 Accepted)

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
| 0011 | Core Domain — Patient-to-Result Orchestration | Accepted (2026-07-18) |
| 0012 | Bounded Context Map (28: 9 Modeled + 19 Recognized) | Accepted (2026-07-18) |
| 0013 | PostgreSQL as the Primary Relational Database | **Accepted** (2026-07-18, this cycle) |
| 0014 | Disaster Recovery and Business Continuity Baseline | **Accepted** (2026-07-18, this cycle) |

**14/14 Accepted. Zero Proposed, Rejected, or Superseded ADRs remain.**

## Final Architectural Decisions (this freeze's own scope, beyond the ADR set)

| Decision | Value | Classification |
|---|---|---|
| Shared-tier tenant partitioning | PostgreSQL RLS + tenant-ID column | Product Configuration |
| FHIR version | R4 | Accepted Decision |
| API Gateway | Kong Gateway (Apache-2.0) | Product Configuration |
| Secrets/Vault Engine | OpenBao (MPL-2.0) | Product Configuration |
| Developer Portal (v1) | Generated docs (Redoc), no dedicated platform | Accepted Decision |
| API Analytics | Apache Superset (E10), no new tool | Accepted Decision |
| Home Collection Offline Mode | Required (local-first capture + sync); 106/106 Features have 0 architectural blockers | Accepted with Constraints |
| Primary relational database | PostgreSQL (ADR-0013) | Accepted Decision |
| Disaster Recovery baseline | 4-tier criticality classification + backup/recovery/governance principles (ADR-0014); numeric RPO/RTO explicitly not yet approved | Accepted Decision (framework) |
| Billing/Insurance model | Architecture supports Direct/Reimbursement/Capitation, Tenant-configurable | Accepted Decision |
| Result Verifier eligibility mechanism | OPA policy-driven, configurable per axis | Accepted Decision |
| Device/processing-failure recovery | Degraded-Mode workflow, Provenance-tracked | Accepted Decision |
| Elevated Audit tier | Adopted (Refund, Expiry-block, Break-Glass, Tenant Config) | Accepted Decision |
| National ID field | Structurally present, FHIR identifier pattern | Accepted Decision |

Full rationale for each: `20-OPEN-QUESTIONS-RESOLUTION.md`.

## Accepted Technology Selections

**Technology Baseline: 24 Engines, 4 Libraries, 5 Reference Standards =
33 entries.** 21 Engines ratified at the original EARB freeze
(2026-07-17), unmodified. **3 Engines added 2026-07-18** (this cycle):
Kong Gateway (E22), OpenBao (E23), PostgreSQL (E24) — added directly to
`docs/architecture-review/02-TECHNOLOGY-BASELINE.md` under that
document's own Amendment Process (a subsequent EARB-equivalent review
cycle, which this Board's explicit mandate this cycle constitutes), not
a silent edit. 0 SDKs, 0 Controlled Forks.

### Governance Statement — Kong Gateway and OpenBao (authoritative, single source of truth)

This is the one canonical statement of Kong/OpenBao's governance
status; every other document in this repository that references them
must be read consistently with this statement, not as an independent
or conflicting authority:

1. **The architectural need for an API Gateway and centralized Secrets
   Management is architecturally frozen** — both are required
   capabilities of the platform, established in `docs/api-platform/10`
   and `12` and unchanged by this statement.
2. **Kong Gateway is the approved Version 1 API Gateway product
   selection.**
3. **OpenBao is the approved Version 1 Secrets Management product
   selection.**
4. **Neither product may be architecturally re-evaluated during SAD
   authoring.** The SAD treats both as fixed input, exactly like any
   other Technology Baseline Engine.
5. **Both remain subject only to implementation due diligence**:
   deployment fit, security hardening, operational compatibility,
   licensing re-verification at implementation time (per this Baseline's
   own standard practice for every Engine), and exit-strategy
   validation (folding into R-08's existing Tier-1 exit-strategy
   scope).
6. **A failed implementation due-diligence gate triggers formal
   governance** — an ADR amendment or replacement decision through
   Constitution Section 45 — **it must never silently change the
   product.** A due-diligence failure is not authorization for an
   individual Module team or implementer to unilaterally substitute a
   different Gateway or Secrets Engine.

This freeze records Kong Gateway, OpenBao, and PostgreSQL as full
Technology Baseline Engine entries (E22-E24), not merely directional
recommendations — see the Governance Statement above for exactly what
"approved" means for each.

**The gap `23-SAD-READINESS-MATRIX.md` row 18 surfaced at the
Architecture Readiness Review — no document formally stated PostgreSQL
as the platform's relational database engine, despite it being
consistently implied throughout (pgvector, Row-Level Security) — is now
closed by ADR-0013.** The SAD's Data Architecture section cites
ADR-0013 directly; no further action is required to close this gap.

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
| Low | R-12 (Marketplace contingency), R-14 (Home Collection — 0 architectural blockers; Build-vs-Buy classification pending a scoped implementation-level micro-assessment, not an architectural gap) | R-15 (Core Domain/BC Map) |

Full detail: `11-RISK-REGISTER.md`.

## SAD Authorization Status

**AUTHORIZED.** Originally confirmed by `21-ARCHITECTURE-READINESS-
REVIEW.md` (PASS, zero architectural inconsistency). **Updated
2026-07-18**: `23-SAD-READINESS-MATRIX.md`'s one Missing-Inputs finding
(Disaster Recovery) is now closed by ADR-0014, and the Data Architecture
Partially-Ready finding is closed by ADR-0013 — see
`25-PRE-SAD-CLEAN-CLOSURE.md` for the updated matrix status.

## Freeze Contents Cross-Reference

| Document | Role in This Freeze |
|---|---|
| `docs/adr/0001` – `0014` | The 14 Accepted ADRs themselves |
| `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` | Technology Baseline — 21 Engines frozen at EARB, 3 added 2026-07-18 (E22-E24) |
| `10-DECISION-REGISTER.md` | Full decision log, 43 entries |
| `11-RISK-REGISTER.md` | Risk status, governance metadata |
| `20-OPEN-QUESTIONS-RESOLUTION.md` | Rationale for every decision this freeze records |
| `21-ARCHITECTURE-READINESS-REVIEW.md` | The review that authorized the original freeze |
| `23-SAD-READINESS-MATRIX.md` | Section-by-section SAD input verification (updated 2026-07-18) |
| `25-PRE-SAD-CLEAN-CLOSURE.md` | This cycle's correction log |

## Board Attestation

This Board attests: every decision in this freeze traces to documented
evidence (no invented fact); no ADR was changed without its own
Amendment section explaining why; the Technology Baseline was extended
(not silently modified) under its own documented Amendment Process,
with the addition itself recorded as a decision (D-58), not a silent
edit; every remaining dependency is honestly classified as
non-architectural; the Disaster Recovery gap is now closed by a
governed framework (ADR-0014) that does not fabricate final numeric
targets — every RPO/RTO cell remains honestly labeled Pending rather
than asserted.

**The Architecture Baseline is FROZEN as of this commit.**
