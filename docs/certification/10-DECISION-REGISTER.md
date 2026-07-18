# Unified Decision Register

Every architecturally significant decision made across this
repository's history, consolidated into one register. Feature-level
Build-vs-Buy decisions (106 rows) are not individually reproduced here
— they remain authoritative in `docs/reuse/MASTER_DECISION_REGISTER.md`
— this register summarizes them by category and lists every decision
at the ADR/Constitution/Technology-Baseline/API-Platform granularity in
full.

## Governing Decisions (ADR-backed, Accepted)

| ID | Decision | Source | Status | Dependencies | Affected Documents |
|---|---|---|---|---|---|
| D-01 | Modular Monolith First | ADR-0001 | Accepted | — | All architecture documents |
| D-02 | Domain-Driven Design | ADR-0002 | Accepted | D-01 | All domain-modeling documents |
| D-03 | Schema per Module | ADR-0003 | Accepted | D-01, D-02 | `docs/api-platform/02, 16, 17` |
| D-04 | Event-Driven Integration (RabbitMQ) | ADR-0004 | Accepted | D-02 | `docs/api-platform/18` |
| D-05 | Hybrid Tenant Isolation | ADR-0005 | Accepted | — | `docs/api-platform/14`, Open Question #15 |
| D-06 | Independent Device Gateway | ADR-0006 | Accepted | D-02 | `docs/api-platform/02, 08` |
| D-07 | Governed AI Gateway, Human-in-the-Loop | ADR-0007 | Accepted | — | `docs/api-platform/03, 11` |
| D-08 | Unified Login and Policy-Based Access (Keycloak + OPA) | ADR-0008 | Accepted | — | `docs/api-platform/08, 09` |
| D-09 | SaaS First, On-Premise Ready, Hybrid Ready | ADR-0009 | Accepted | — | `docs/architecture-review/07`, licensing decisions |
| D-10 | Arabic/English and Localization First | ADR-0010 | Accepted | — | `docs/api-platform/05` |
| D-11 | Core Domain: Patient-to-Result Orchestration | ADR-0011 | **Accepted (superseded 2026-07-18 — see D-40)** | — | `docs/architecture-review/10`, `docs/api-platform/15`, `20-OPEN-QUESTIONS-RESOLUTION.md` |
| D-12 | Bounded Context Map (28 contexts, Hybrid Modeled/Recognized) | ADR-0012 | **Accepted (superseded 2026-07-18 — see D-41)** | D-11 | `docs/reuse/` Module structure, `20-OPEN-QUESTIONS-RESOLUTION.md` |

## Technology Baseline Decisions (Frozen, EARB phase)

| ID | Decision | Status | Count |
|---|---|---|---|
| D-13 | 21 Engines ratified (19 fully, 2 conditionally: Eramba, Mirth Connect) | Frozen | 21 |
| D-14 | 4 Libraries ratified | Frozen | 4 |
| D-15 | 5 Reference Standards adopted | Frozen | 5 |
| D-16 | 0 third-party SDKs ratified (confirmed absence) | Frozen | 0 |
| D-17 | 0 Controlled Forks ratified (confirmed absence) | Frozen | 0 |
| D-18 | Amendment process: new ADR, EARB review cycle, or legal counsel finding only | Frozen | — |

## API Platform Decisions (Parts 1-2)

| ID | Decision | Status | Source |
|---|---|---|---|
| D-19 | REST as default API paradigm | Recommendation | `docs/api-platform/01, 05` |
| D-20 | URL-path major versioning | Recommendation | `docs/api-platform/07` |
| D-21 | OpenAPI 3.1.x / AsyncAPI 3.x as mandatory contract notations | Recommendation | `docs/api-platform/17, 18` |
| D-22 | Consumer-Driven Contracts for Internal traffic | Recommendation | `docs/api-platform/16` |
| D-23 | Webhooks: at-least-once delivery, signed, SSRF-protected | Recommendation | `docs/api-platform/19` |
| D-24 | SDKs generated (never hand-written), from OpenAPI source | Recommendation | `docs/api-platform/20` |
| D-25 | Monetization/Billing reuse Kill Bill + OPA (no new commercial engine) | Recommendation, evidence-grounded | `docs/api-platform/25, 26` |
| D-26 | No numeric SLA/rate-limit/deprecation-window value asserted pending real data | Explicit non-decision | `docs/api-platform/07, 13, 28` |
| D-27 | Pact recommended for Contract Testing | Recommendation | `docs/api-platform/31` |
| D-28 | OpenAPI Generator recommended for SDK Generation | Recommendation | `docs/api-platform/31` |
| D-29 | Redoc recommended conditionally for API Documentation (RTL unverified) | Conditional Recommendation | `docs/api-platform/31` |
| D-30 | API Gateway product selection | **Resolved 2026-07-18 — see D-44 (Kong Gateway)** | `docs/api-platform/10, 31`, Open Question #28 |
| D-31 | Secrets/Vault Engine selection | **Resolved 2026-07-18 — see D-45 (OpenBao)** | `docs/api-platform/12, 31`, Open Question #29 |
| D-32 | Developer Portal product selection | **Resolved 2026-07-18 — see D-46** | `docs/api-platform/22, 31`, Open Question #30 |
| D-33 | API Analytics tooling need | **Resolved 2026-07-18 — see D-47 (Superset, no new tool)** | `docs/api-platform/27, 31`, Open Question #31 |

## Reuse Intelligence Decisions (Summarized — 106 individual rows in `MASTER_DECISION_REGISTER.md`)

| ID | Decision Category | Count | Status |
|---|---|---|---|
| D-34 | Features decided (Build/Reuse-Engine/Reuse-Library/Reference) | 105/106 | Ratified via EARB freeze (D-13 through D-15) |
| D-35 | Features blocked (home-collection-logistics) | 1/106 → 0/106 | **Unblocked 2026-07-18 — Open Question #6 resolved (D-48, Offline Mode Required)** |
| D-36 | Duplicate Features detected and resolved | 9/9 | Resolved (2 reactive, 7 proactive) |

## This Certification Audit's Own Decisions

| ID | Decision | Status |
|---|---|---|
| D-37 | 3 documentation-currency defects corrected (safe fixes) | Applied — see `09-SAFE-FIXES-APPLIED.md` |
| D-38 | No architectural, ADR, or Technology Baseline change made | Confirmed — this audit is certification, not redesign |
| D-39 | Certification verdict: PASS WITH CONDITIONS | See `18-CERTIFICATION-REPORT.md` |

## Open Questions Resolution Phase Decisions (2026-07-18)

Full rationale/evidence for each: `20-OPEN-QUESTIONS-RESOLUTION.md`.
Supersedes/updates: D-11 (Core Domain, now Accepted), D-12 (Bounded
Context Map, now Accepted), D-30/D-31/D-32/D-33 (product selections
now made), D-35 (home-collection-logistics now unblocked).

| ID | Decision | Classification | Status |
|---|---|---|---|
| D-40 | Core Domain = Patient-to-Result Orchestration | Accepted Decision | ADR-0011 Accepted |
| D-41 | Bounded Context Map = 28 (9 Modeled + 19 Recognized) | Accepted Decision | ADR-0012 Accepted |
| D-42 | Shared-tier partitioning = PostgreSQL RLS + tenant-ID column | Product Configuration | Accepted |
| D-43 | FHIR version pinned = R4 | Accepted Decision | Accepted |
| D-44 | API Gateway = Kong Gateway (OSS, Apache-2.0) | Product Configuration | Accepted |
| D-45 | Secrets/Vault = OpenBao (MPL-2.0) | Product Configuration | Accepted |
| D-46 | Developer Portal v1 = generated docs (Redoc), no dedicated platform | Accepted Decision | Accepted |
| D-47 | API Analytics = Superset (E10), no new tool | Accepted Decision | Accepted |
| D-48 | Home Collection Offline Mode = Required (local-first capture + sync) | Accepted with Constraints | Accepted, scoped to Home Collection |
| D-49 | Billing/Insurance model = architecture supports all 3 (Direct/Reimbursement/Capitation), Tenant-configurable | Accepted Decision | Accepted |
| D-50 | Result Verifier eligibility = OPA policy-driven mechanism; values are Regulatory Dependency | Accepted Decision (mechanism) | Accepted |
| D-51 | Device/processing-failure recovery = Degraded-Mode workflow (Provenance-tracked queue/retry) | Accepted Decision | Accepted |
| D-52 | Elevated Audit tier adopted (Refund, Expiry-block, Break-Glass, Tenant Config) | Accepted Decision | Accepted |
| D-53 | National ID = structurally-present optional Patient identifier (FHIR pattern); validation rules are Country Localization | Accepted Decision | Accepted |
| D-54 | Expected usage volume = launch-scale Operational Assumption, no fixed number | Operational Assumption | Recorded |
| D-55 | AGPL legal review outcome = remains Legal Dependency, not resolved by this Board | Legal Dependency | Unchanged, tracked |

## Decision Quality Summary

- **Total decisions tracked in this register: 39** (12 governing +
  6 Baseline + 15 API Platform + 3 Reuse-summary + 3 this-audit).
- **Every decision cites a traceable source document** — verified,
  zero orphan decisions (a decision with no cited evidence) found.
- **Every non-decision (D-26, D-30, D-31, D-32, D-33) is explicit**,
  not a silent gap — each has a named Open Question ID.
