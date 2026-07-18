# Project Memory

Permanent record of this project's complete history, for any future
session (human or AI) to orient quickly without re-deriving context
from scratch. This complements, and does not replace, `.claude/context/`
(the living Context Store).

**Current phase: Pre-SAD Baseline Correction & Clean Closure (complete,
2026-07-18).**
**Next phase: Software Architecture Document (SAD) — authorized to
begin, not yet started.** See `20-OPEN-QUESTIONS-RESOLUTION.md` for the
Open Questions resolution log and `25-PRE-SAD-CLEAN-CLOSURE.md` for
this phase's correction log.

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
| 6 | Global Build-vs-Buy & Reuse Intelligence Program | `docs/reuse/` (1,396 files, 28 Modules, 106 Features) | 105/106 Features with a Final Decision, 1 (`home-collection-logistics`) architecturally unblocked 2026-07-18 with classification pending an implementation-level micro-assessment (0 architectural blockers); 9 duplicate Features resolved |
| 7 | Enterprise Adoption Review Board (EARB) | `docs/architecture-review/` (14 files) | Technology Baseline FROZEN: 21 Engines, 4 Libraries, 5 Reference Standards; 0 SDKs, 0 Forks ratified; AGPL checklist established |
| 8 | API Platform Strategy — Part 1 | `docs/api-platform/00-15` (16 files) | API-First architecture, domain inventory, governance, standards, auth, security foundation |
| 9 | API Platform Strategy — Part 2 | `docs/api-platform/16-33` (18 files) | Contract-First tooling, webhooks, SDK strategy, Developer Portal, Marketplace, commercial loop; 3/7 tooling categories recommended, 4 left open |
| 10 | Enterprise Architecture Certification Audit + Closure | `docs/certification/` (20 files) | Full repository audit, 3 documentation defects found and fixed, 0 architectural contradictions, PASS WITH CONDITIONS; closure pass corrected register arithmetic and clarified Conditions vs. Dependencies |
| 11 | Open Questions Resolution | `docs/certification/20-OPEN-QUESTIONS-RESOLUTION.md`, ADR-0011/0012 promotion | All 31 Open Questions resolved (18 Accepted Decisions/Configurations, 13 tracked Dependencies), Core Domain and Bounded Context Map confirmed Accepted, Gateway/Vault products selected, FHIR version pinned |
| 12 | Architecture Readiness Review (ARR) | `docs/certification/21-25` (5 files, ARR series) | Zero architectural inconsistency found; Architecture Baseline Freeze v1; 25-section SAD Readiness Matrix (19 Ready, 5 Partially Ready, 1 Missing Inputs — Disaster Recovery); verdict READY FOR SAD |
| 13 | **Pre-SAD Baseline Correction & Clean Closure (this phase)** | `docs/certification/25-PRE-SAD-CLEAN-CLOSURE.md`, ADR-0013/0014, Baseline Freeze v2 | Feature-decision count corrected (0 architectural blockers); Kong/OpenBao governance clarified (one canonical statement); PostgreSQL formally adopted (ADR-0013); Disaster Recovery baseline governed (ADR-0014, no fabricated numbers); SAD Readiness Matrix now 21 Ready / 4 Partially Ready / 0 Missing Inputs |

**Next authorized phase**: Software Architecture Document (SAD) —
**authorized to begin, not yet started.**

## Major Decisions (Accepted)

**14 ADRs (0001-0014), all Accepted, 0 Proposed.** ADRs 0001-0010:
Modular Monolith First, Domain-Driven Design, Schema per Module,
Event-Driven Integration, Hybrid Tenant Isolation, Independent Device
Gateway, Governed AI Gateway, Unified Login and Policy-Based Access,
SaaS First/On-Premise/Hybrid Ready, Arabic/English and Localization
First. ADR-0011 (Core Domain: Patient-to-Result Orchestration) and
ADR-0012 (Bounded Context Map, 28 contexts) — promoted Proposed →
Accepted 2026-07-18 in the Open Questions Resolution phase (see
"Historical Note" below). ADR-0013 (PostgreSQL as the Primary
Relational Database) and ADR-0014 (Disaster Recovery and Business
Continuity Baseline) — Accepted 2026-07-18 in the Pre-SAD Baseline
Correction phase. Full detail: `10-DECISION-REGISTER.md`.

### Historical Note — ADR-0011/0012's Former Proposed Status

Until 2026-07-18, ADR-0011 and ADR-0012 were deliberately withheld from
Accepted status pending genuine business-strategy resolution (the
competing Specimen Management alternative), re-verified as correctly
still-Proposed by three independent reviews (Discovery, EARB, API
Platform Part 2) plus the Certification Audit's own ADR Certification
(`04-ADR-CERTIFICATION.md`). This finding was accurate at the time each
of those reviews was issued and is preserved here as history, not
rewritten. The Open Questions Resolution phase then reviewed and
promoted both ADRs to Accepted, per each ADR's own stated promotion
condition — see `20-OPEN-QUESTIONS-RESOLUTION.md` and each ADR's
"Amendment — Open Questions Resolution Phase" section for the disclosed
evidentiary gap that remains (the Specimen Management alternative was
never head-to-head scored).

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

Technology Baseline (24 Engines, 4 Libraries, 5 Reference Standards =
33 entries). 21 Engines ratified at the original EARB freeze
(2026-07-17, unmodified): Keycloak, OPA, Unleash, immudb, Eramba, Mirth
Connect, RabbitMQ, Novu, Portkey Gateway, Apache Superset, Alfresco,
Documenso, Cal.com, Atlas CMMS, OpenBoxes, ERPNext, openIMIS, Frappe HR,
Frappe Helpdesk, Frappe CRM, Kill Bill. **3 Engines added 2026-07-18**
(Pre-SAD Baseline Correction, under the Baseline's own Amendment
Process): Kong Gateway (API Gateway, D-44), OpenBao (Secrets/Vault,
D-45), PostgreSQL (primary relational database, ADR-0013). 4 Libraries
(pgvector, Prophet, FullCalendar, ZXing), 5 Reference Standards (HL7
FHIR family, LOINC, Westgard Rules, PostgreSQL RLS, Omnipay pattern).
Kong Gateway and OpenBao's governance status (approved Version 1
product selections, not subject to architectural re-evaluation, subject
only to implementation due diligence) is authoritatively stated once in
`22-ARCHITECTURE-BASELINE-FREEZE.md`. Full detail:
`docs/architecture-review/02-TECHNOLOGY-BASELINE.md`.

## Governance

Constitution §44-45 (Exception/Amendment), §57 (Architecture Review
Board), §58 (Risk Governance), §59-61 (Documentation/Glossary/ADR
Governance) form the complete governance apparatus. Amendment of any
Accepted decision requires a new ADR, never a silent edit. Technology
Baseline amendment requires a new ADR, an EARB review cycle, or formal
legal counsel findings (`docs/architecture-review/
12-DECISION-FREEZE.md`).

## Current Repository State (updated 2026-07-18, Pre-SAD Baseline Correction)

- **1,607+ markdown files** across `docs/` and `.claude/context/` (count
  as of the Certification Audit; grows with each subsequent phase's new
  documents).
- **14 ADRs** (14 Accepted, 0 Proposed).
- **28 Modules, 106 Features** (106 architecturally resolved, 0
  architectural blockers — 105 with a Final Decision, 1,
  `home-collection-logistics`, unblocked 2026-07-18 with its
  Build-vs-Buy classification pending a scoped implementation-level
  micro-assessment).
- **33 Technology Baseline entries** (24 Engines, 4 Libraries, 5
  Reference Standards — frozen at EARB, extended 2026-07-18 under the
  Baseline's own Amendment Process).
- **52 API Platform documents** (34 Parts 1-2 + the Certification
  Audit's own review of them).
- **31 Open Questions**, all resolved (`20-OPEN-QUESTIONS-RESOLUTION.md`);
  0 remain as architectural open questions. Two SAD-input gaps
  discovered afterward at the Architecture Readiness Review (PostgreSQL,
  Disaster Recovery) are also now closed (ADR-0013, ADR-0014).
- **15 enterprise risks** tracked; 0 newly discovered beyond
  documentation-currency issues found by the Certification Audit (3, all
  fixed).
- **Latest commit prior to the Certification Audit**: `baf1776`. Latest
  commit prior to this phase (Pre-SAD Baseline Correction): `d152320`.

## Important Assumptions Carried Forward

- Discovery's Assumption-Driven findings remain explicitly labeled
  Inferred/Industry-Reference, never silently promoted to Confirmed.
- FHIR R4 was the evidence-weighted *default* pending version pinning;
  **resolved 2026-07-18** — FHIR R4 is now pinned as an Accepted
  Decision (D-43), closing R-06.
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
