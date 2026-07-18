# Project Memory

Permanent record of this project's complete history, for any future
session (human or AI) to orient quickly without re-deriving context
from scratch. This complements, and does not replace, `.claude/context/`
(the living Context Store) — this document is a point-in-time narrative
snapshot as of the Enterprise Architecture Certification Audit; the
Context Store remains the file to actually update going forward.

## What This Project Is

A **Digital Healthcare Platform**, starting point Laboratory Management,
long-term goal a broad, extensible **Healthcare Operations Platform**:
SaaS Multi-Tenant, first market Egypt, serving independent labs, lab
chains, hospitals, clinics, medical groups, corporate healthcare
providers, and external API/Partner clients — via a central backend,
unified login, and role/permission/data-scope/organization/branch-based
routing to the correct Portal/Dashboard. Explicitly **not** a plain CRUD
system.

## Complete Phase History

| # | Phase | Output | Key Outcome |
|---|---|---|---|
| 1 | Skills & Environment Setup | `.claude/skills/` (9 skills), `.claude/context/` (9 files), `CLAUDE.md` | Working-agreement + tooling foundation established |
| 2 | Project Constitution v1 | `docs/constitution/PROJECT-CONSTITUTION.md` (47 sections), 10 ADRs | Modular Monolith, DDD, Event-Driven, Tenancy, Security, Device/AI Gateway, SaaS-first, Localization all Accepted |
| 3 | Constitution v2 | +15 sections (48-62) | Engineering principles, fitness functions, governance apparatus — no new ADRs, strict superset of v1 |
| 4 | Enterprise Discovery (12 baseline phases) | `docs/discovery/` baseline | Assumption-Driven Autonomous Run (explicitly labeled Inferred, not real stakeholder input); 8 candidate Bounded Contexts, Core Domain candidate proposed |
| 5 | Discovery Gap Closure (15 waves) | `docs/discovery/reports/GAP-CLOSURE-*.md` | Expanded from 4/32 to full business-domain coverage; 28-context remap (Wave 9); ADR-0011/0012 created as Proposed |
| 6 | Global Build-vs-Buy & Reuse Intelligence Program | `docs/reuse/` (1,396 files, 28 Modules, 106 Features) | 105/106 Features decided, 1 blocked; 9 duplicate Features resolved |
| 7 | Enterprise Adoption Review Board (EARB) | `docs/architecture-review/` (14 files) | Technology Baseline FROZEN: 21 Engines, 4 Libraries, 5 Reference Standards; 0 SDKs, 0 Forks ratified; AGPL checklist established |
| 8 | API Platform Strategy — Part 1 | `docs/api-platform/00-15` (16 files) | API-First architecture, domain inventory, governance, standards, auth, security foundation |
| 9 | API Platform Strategy — Part 2 | `docs/api-platform/16-33` (18 files) | Contract-First tooling, webhooks, SDK strategy, Developer Portal, Marketplace, commercial loop; 3/7 tooling categories recommended, 4 left open |
| 10 | **Enterprise Architecture Certification Audit + Closure (this phase)** | `docs/certification/` (20 files) | Full repository audit, 3 documentation defects found and fixed, 0 architectural contradictions, PASS WITH CONDITIONS; closure pass corrected register arithmetic and clarified Conditions vs. Dependencies |

**Next authorized phase**: Software Architecture Document (SAD) —
**not started**, requires explicit separate authorization per this
phase's own Stop Condition.

## Major Decisions (Accepted)

10 ADRs (0001-0010): Modular Monolith First, Domain-Driven Design,
Schema per Module, Event-Driven Integration, Hybrid Tenant Isolation,
Independent Device Gateway, Governed AI Gateway, Unified Login and
Policy-Based Access, SaaS First/On-Premise/Hybrid Ready, Arabic/English
and Localization First. Full detail: `10-DECISION-REGISTER.md`.

## Major Decisions (Proposed, Not Accepted — By Design)

ADR-0011 (Core Domain: Patient-to-Result Orchestration candidate) and
ADR-0012 (Bounded Context Map, 28 contexts) — both deliberately
withheld from Accepted status pending genuine business-strategy
resolution (the competing Specimen Management alternative), re-verified
as correctly still-Proposed by three independent reviews (Discovery,
EARB, API Platform Part 2) plus this audit's own ADR Certification
(`04-ADR-CERTIFICATION.md`).

## Rejected/Deferred Decisions

- Microservices as a default architecture — explicitly rejected as a
  starting assumption (ADR-0001); `microservices-patterns` Skill
  deliberately not installed to avoid biasing early design.
- Full financial ERP build in v1 — explicitly not assumed; boundary
  between Native/Integration/Deferred financial scope left to Gap
  Closure Wave 3/10, not assumed.
- Several Skill candidates rejected at installation (heavy multi-skill
  DDD pipelines, PyPI-distributed skills, event-sourcing-biased
  bundles) — see `.claude/SKILLS-VALIDATION-REPORT.md` Section 5.
- Eramba Community's low-confidence GRC selection was *not* reversed
  despite low confidence — no stronger alternative was found across the
  full 28-Module program; carried forward as R-01, not silently
  resolved either direction.

## Technology Decisions

Frozen Technology Baseline: 21 Engines (Keycloak, OPA, Unleash, immudb,
Eramba, Mirth Connect, RabbitMQ, Novu, Portkey Gateway, Apache Superset,
Alfresco, Documenso, Cal.com, Atlas CMMS, OpenBoxes, ERPNext, openIMIS,
Frappe HR, Frappe Helpdesk, Frappe CRM, Kill Bill), 4 Libraries
(pgvector, Prophet, FullCalendar, ZXing), 5 Reference Standards (HL7
FHIR family, LOINC, Westgard Rules, PostgreSQL RLS, Omnipay pattern).
Full detail: `docs/architecture-review/02-TECHNOLOGY-BASELINE.md`.

## Governance

Constitution §44-45 (Exception/Amendment), §57 (Architecture Review
Board), §58 (Risk Governance), §59-61 (Documentation/Glossary/ADR
Governance) form the complete governance apparatus. Amendment of any
Accepted decision requires a new ADR, never a silent edit. Technology
Baseline amendment requires a new ADR, an EARB review cycle, or formal
legal counsel findings (`docs/architecture-review/
12-DECISION-FREEZE.md`).

## Current Repository State (as of this audit)

- **1,607 markdown files** across `docs/` and `.claude/context/`.
- **12 ADRs** (10 Accepted, 2 Proposed).
- **28 Modules, 106 Features** (105 decided, 1 blocked).
- **30 Technology Baseline entries** (frozen).
- **52 API Platform documents** (34 Parts 1-2 + this audit's own review
  of them).
- **31 Open Questions** tracked, 0 silently closed.
- **15 enterprise risks** tracked, 0 newly discovered by this audit
  beyond documentation-currency issues (3, all fixed).
- **Latest commit prior to this audit**: `baf1776`.

## Important Assumptions Carried Forward

- Discovery's Assumption-Driven findings remain explicitly labeled
  Inferred/Industry-Reference, never silently promoted to Confirmed.
- FHIR R4 is the evidence-weighted *default* for eventual version
  pinning, not an asserted Decision (R-06 remains open).
- REST (not GraphQL) is the API Platform's Recommendation, not an ADR-
  backed Decision.

## Important Constraints Carried Forward

14 Confirmed constraints in `.claude/context/constraints.md` — 7
original (scalability, independent-team support, no direct Module
coupling, backend-enforced authorization, medical data sensitivity, no
unreviewed AI medical decisions, no default microservices) + 7 added
post-Constitution-v1 (schema isolation, testable tenant isolation,
device-adapter provenance, AI data-sharing policy gate, no UI-hiding-
as-authorization, replaceable cloud provider, no hardcoded locale/
currency/timezone).

## Known Risks

15 tracked, full detail in `11-RISK-REGISTER.md`. Highest severity: R-02
(Mirth Connect frozen-release) and R-04 (AGPL-3.0 legal exposure, 5
Engines).

## Knowledge Preservation Notes

- This project's single most consistently-applied discipline across
  every phase is the **No-Guessing Rule** (CLAUDE.md §3): no number,
  requirement, or decision is invented without a traceable source —
  verified by this audit to hold with zero exceptions found across
  1,607 files.
- The second most consistent discipline is **honest scope disclosure**:
  every phase that could not achieve full depth explicitly said so
  (reuse program's per-Module scoring depth disclosure, Discovery's
  Assumption-Driven labeling, this audit's own Method Note on how
  1,396+99 files were actually covered) rather than implying uniform
  rigor it did not perform.
- A new session picking this project up should read, in order:
  `CLAUDE.md` → `.claude/context/README.md` and its 8 files →
  `docs/constitution/README.md` → `docs/architecture-review/
  12-DECISION-FREEZE.md` → `docs/api-platform/33-PART2-EXECUTIVE-
  SUMMARY.md` → this document → `18-CERTIFICATION-REPORT.md`.
