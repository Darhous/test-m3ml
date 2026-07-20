# SAD Wave 1 — Introduction, Goals, Constraints & Stakeholders

**Document Status:** Review (per `docs/constitution/PROJECT-CONSTITUTION.md`
§59 Document Status Vocabulary — circulated, not yet Accepted). Becomes
Accepted upon review by the Architecture Review Board, which today is
fulfilled entirely by the project owner (Constitution §57).

**Wave:** 1 of 13 (see `docs/sad/README.md` for the full wave plan).

**Scope of this Wave:** this document covers only Introduction, Goals,
Constraints, and Stakeholders, at the depth listed in the Table of
Contents below. It intentionally does not draw diagrams, define Bounded
Contexts in detail, or specify runtime/deployment/API design — those are
later Waves.

---

## Table of Contents

1. Purpose of the SAD
2. Document Objectives
3. Intended Audience
4. Business and Architectural Goals
5. Primary Stakeholders
6. Stakeholder Concerns
7. Known Constraints
8. Regulatory and Healthcare-Domain Constraints
9. Technical and Operational Constraints
10. Assumptions
11. Out-of-Scope Items (this Document)
12. Document Governance and Ownership
13. Relationship to the Constitution, ADRs, Baselines, Registers, and Prior Artifacts
14. Wave 1 Traceability References

---

## 1. Purpose of the SAD

The Software Architecture Document (SAD) exists to describe **how** the
digital healthcare platform is built to satisfy the governing rules
already established in `docs/constitution/PROJECT-CONSTITUTION.md`
(v2.1, Accepted), the 14 Accepted Architecture Decision Records
(`docs/adr/0001`–`0014`), the frozen Technology Baseline (33 entries,
`docs/architecture-review/02-TECHNOLOGY-BASELINE.md`), the API Platform
Strategy (`docs/api-platform/`), and the Unified Decision and Risk
Registers (`docs/certification/10-DECISION-REGISTER.md`,
`11-RISK-REGISTER.md`).

Per Constitution §1 ("Non-authority"), the Constitution explicitly does
**not** select a programming language, framework, cloud provider,
message broker, database product, AI provider, or frontend framework,
and explicitly defers those concrete designs to the SAD. The SAD is
therefore the first document in this repository whose job is to turn
Accepted rules and a frozen Technology Baseline into an actual system
design — not to re-decide anything already Accepted.

The SAD was authorized to begin on 2026-07-18, when
`docs/certification/26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md` recorded
the verdict **"CLEAN SEMANTIC BASELINE — READY FOR SOFTWARE ARCHITECTURE
DOCUMENT."** `docs/certification/15-SAD-INPUT-PACKAGE.md` independently
confirms a **READY** verdict for SAD authoring, noting that all 6 formal
Certification Conditions are satisfied except the AGPL-3.0 legal review
(R-04), which is an explicit Legal Dependency outside architectural
authority and is carried forward, not treated as a blocker (see §9 and
§13 below).

## 2. Document Objectives

1. Translate the 25 SAD-relevant areas identified in
   `docs/certification/23-SAD-READINESS-MATRIX.md` (21 rated Ready, 4
   rated Partially Ready, 0 with Missing Inputs) into an authored
   architecture description, Wave by Wave, per `docs/sad/README.md`.
2. Preserve full traceability: every substantive statement in the SAD
   must trace back to a governing ADR, Constitution section, Decision
   Register ID (`D-nn`), or Risk Register ID (`R-nn`) — the SAD does not
   introduce new architectural decisions silently.
3. Explicitly carry forward, without resolving them here, the items
   `docs/certification/15-SAD-INPUT-PACKAGE.md` names as still owed by
   the SAD itself: exit-strategy procedures for the 7 Tier-1 Engines
   (R-08), the AGPL-3.0 legal review outcome (R-04), Arabic/RTL
   verification per ratified Engine, numeric SLA/SLO/rate-limit/
   deprecation-window targets, and a one-page Domain Vision Statement.
   None of these are resolved in Wave 1.
4. Provide a single, versioned reference intended to guide module
   implementation once it begins — not a one-time report.
5. Respect the No-Guessing Rule (`CLAUDE.md` §3): where a fact,
   constraint, or number is not already Accepted or explicitly stated by
   the user, this document records it as unresolved rather than
   inventing an answer.

## 3. Intended Audience

Drawn from `.claude/context/stakeholders.md` and the 39-Persona
expansion (`docs/discovery/artifacts/W2-persona-catalog.md`), scoped to
the roles that actually consume an architecture document (as opposed to
a product/UX document):

- **Development Teams** — the primary audience once module
  implementation starts; not yet an active roster (Constitution §57
  notes this explicitly — see §12 below).
- **The Architecture Review Board** — today fulfilled entirely by the
  project owner (Constitution §57).
- **Platform Administrators** and **Organization Administrators** — for
  capability and boundary decisions that affect how they operate the
  platform.
- **Security and Compliance Teams** — for the security, privacy, and
  audit architecture defined in later Waves.
- **Device Integration Teams** — for the Device Integration Gateway
  architecture (Wave 9).
- **External API Partners** — for the parts of the API Architecture that
  become public-facing (Wave 4 onward, `docs/api-platform/`).

**Not the intended audience of the SAD:** Patients, Doctors, and
Laboratory Staff (end users) — their needs inform product/UX
documentation and the Discovery artifacts already produced
(`docs/discovery/`), not this document.

## 4. Business and Architectural Goals

### 4.1 Business Goals (from `.claude/context/vision.md`)

Status preserved exactly as the source file states it. `vision.md` as a
whole is still file-level `Draft`, but its content is internally labeled
`Confirmed` where the user gave it directly — this Wave keeps that same
distinction rather than flattening it into a single status:

- A **Digital Healthcare Platform**, starting point **Laboratory
  Management**, long-term goal a broad healthcare platform — not a plain
  CRUD system. (From `vision.md`'s "Initial Confirmed Context" — file is
  `Draft` overall, this base framing is internally marked Confirmed.)
- **Confirmed, 2026-07-16** (`docs/discovery/artifacts/W1-vision-scope-operating-model.md`):
  the target product is a **Healthcare Operations Platform** — a
  multi-tenant SaaS platform that runs the operations of healthcare and
  diagnostic organizations — not merely a LIMS, a Patient Results
  Portal, or a Billing System.
- First target market: **Egypt**, with architectural readiness for
  additional markets later (not a commitment to build for them now).
- Target customer types (Confirmed): independent lab, lab chain,
  hospital, medical center, clinic, medical group, corporate healthcare
  provider, multi-branch diagnostic entity, and external Partner/API
  clients.
- Confirmed operational commitments: White Label, Plans and
  Subscriptions, Usage/Entitlement Tracking, SaaS billing readiness —
  verified as not conflicting with any prior Accepted decision.
- Explicitly **not** assumed: a full financial ERP is not required in
  v1 by default (explicit user instruction) — the Native/Integration/
  Deferred boundary for the financial scope is a Gap Closure finding,
  not re-litigated here.

### 4.2 Architectural Goals (Accepted, ADR-backed)

| Goal | ADR |
|---|---|
| Modular Monolith as the v1 architectural style, with Selective Service Extraction only when a measured trigger exists | [0001](../adr/0001-modular-monolith-first.md) |
| Domain-Driven Design as the modeling approach | [0002](../adr/0002-domain-driven-design.md) |
| Schema per Module — no direct cross-module database access | [0003](../adr/0003-schema-per-module.md) |
| Event-Driven Integration between modules | [0004](../adr/0004-event-driven-integration.md) |
| Hybrid Tenant Isolation (shared tier + dedicated tier for large/regulated tenants) | [0005](../adr/0005-hybrid-tenant-isolation.md) |
| Independent Device Integration Gateway with an Anti-Corruption Layer | [0006](../adr/0006-independent-device-gateway.md) |
| Governed AI Gateway with mandatory Human-in-the-Loop | [0007](../adr/0007-governed-ai-gateway.md) |
| Unified Login and Policy-Based Access | [0008](../adr/0008-unified-login-and-policy-based-access.md) |
| SaaS First, On-Premise Ready, Hybrid Ready, replaceable cloud provider | [0009](../adr/0009-saas-first-on-premise-and-hybrid-ready.md) |
| Arabic/English and Localization First | [0010](../adr/0010-arabic-english-and-localization-first.md) |
| Core Domain = Patient-to-Result Orchestration | [0011](../adr/0011-core-domain-test-processing-and-result-verification.md) |
| Bounded Context Map — 28 contexts (9 Modeled + 19 Recognized) | [0012](../adr/0012-candidate-bounded-context-map.md) |
| PostgreSQL as the primary relational database | [0013](../adr/0013-postgresql-as-primary-relational-database.md) |
| Disaster Recovery and Business Continuity baseline (4-tier criticality; numeric RPO/RTO Pending, not fabricated) | [0014](../adr/0014-disaster-recovery-and-business-continuity-baseline.md) |

API-First Design is Accepted as part of the same decision block as
ADR-0001 (`.claude/context/architecture-principles.md`, principle #9),
not a separately numbered ADR.

## 5. Primary Stakeholders

From `.claude/context/stakeholders.md`, Status: **Draft** (initial
categories, not individually detailed) unless noted:

| # | Stakeholder |
|---|---|
| 1 | Patients |
| 2 | Doctors |
| 3 | Laboratory Staff |
| 4 | Laboratory Management |
| 5 | Organization Administrators |
| 6 | Platform Administrators |
| 7 | Finance Teams |
| 8 | Inventory Teams |
| 9 | Insurance Users |
| 10 | Suppliers |
| 11 | Device Integration Teams |
| 12 | Support Teams |
| 13 | Security and Compliance Teams |
| 14 | Development Teams |
| 15 | External API Partners |

This 15-category list was later expanded to **39 Personas** during Gap
Closure Wave 2 (2026-07-16), adding categories the original list did not
cover at all: Financial (Cashier, Accountant, Finance Manager),
Workforce (HR, Payroll), Supply Chain (Procurement, Inventory, Store
Manager), Platform/SaaS (Platform Operator, Tenant/Branch
Administrator, SaaS Commercial Team), and Governance (Auditor,
Compliance Staff, Legal Reviewer, Regulator). The full per-persona
detail (Goals/Pain Points/Data Scope/High-Risk Actions/KPI) lives in
`docs/discovery/artifacts/W2-persona-catalog.md` and is not duplicated
here, to avoid the two documents drifting out of sync.

## 6. Stakeholder Concerns

**Explicit caveat carried forward from the source document:** the needs
below are labeled `Inferred — Industry Reference` in
`.claude/context/stakeholders.md` — general laboratory-industry
knowledge captured during an Assumption-Driven Discovery run, **not**
the result of a real conversation with actual stakeholders. They have
not been reviewed or confirmed by the user and must not be treated as
Accepted requirements.

| Stakeholder | Candidate Concern (Inferred) | Primarily Addressed In |
|---|---|---|
| Patients | Convenient test ordering; trustworthy, timely results; clear billing | Later Waves (Runtime View, API Architecture) |
| Doctors | Fast, reliable result delivery; ordering on a patient's behalf; result history access | Later Waves |
| Laboratory Staff | Clear worklists; accurate specimen tracking; low-friction result entry/verification | Wave 4 (Building Block View) |
| Laboratory Management | Operational visibility; staff workload balancing | Wave 4 |
| Organization Administrators | Branch-level oversight; user/role administration within their Organization | Wave 8 (Multi-Tenancy, Identity & Access Governance) |
| Platform Administrators | Cross-organization oversight; platform health/configuration | Wave 8 |
| Finance Teams | Accurate invoicing; reconciliation with insurance payments | Wave 4 (Billing and Claims context) |
| Inventory Teams | Reagent/supply visibility; low-stock alerts | Wave 4 |
| Insurance Users | Clear eligibility/coverage determination; claim status visibility | Wave 4 |
| Suppliers | Predictable ordering/replenishment signals | Wave 4 |
| Device Integration Teams | Reliable device connectivity; clear failure diagnostics | Wave 9 (AI Governance, Device Integration & Other Cross-Cutting Concerns) |
| Support Teams | Tools to resolve patient/doctor issues | Later Waves |
| Security and Compliance Teams | Full audit trail; enforceable Data Scope; breach-readiness | Wave 7 (Security, Privacy & Trust Boundaries) |
| Development Teams | Clear module boundaries and contracts to build against | Wave 3 (Solution Strategy), Wave 4 |
| External API Partners | Stable, versioned integration contracts | Later Waves (`docs/api-platform/`) |

## 7. Known Constraints

From `.claude/context/constraints.md`, Status: **Confirmed** (distinct
from the Draft/Inferred material in §6 above) unless the row says
otherwise:

| # | Constraint | Type | Source |
|---|---|---|---|
| 1 | The system must be Scalable | Technical | Confirmed |
| 2 | Independent teams must be able to work on separate Modules | Organizational | Confirmed |
| 3 | A Module must not depend on another Module's implementation details (avoid direct coupling) | Technical | Confirmed |
| 4 | Authorization must be enforced in the Backend, not only in the UI | Technical/Security | Confirmed |
| 5 | Medical data is highly sensitive | Regulatory/Ethical | Confirmed |
| 6 | AI must never issue a final, unreviewed medical decision independently | Ethical/Regulatory | Confirmed |
| 7 | Microservices is not the default starting choice (Modular Monolith First) | Technical | Confirmed |
| 8 | No Module may directly access (SQL joins/writes) another Module's owned tables/schema — only via approved API/Events/Read Models | Technical | [ADR-0003](../adr/0003-schema-per-module.md) |
| 9 | Tenant isolation must be automatically testable before a Module handling tenant data is considered "done" | Technical | [ADR-0005](../adr/0005-hybrid-tenant-isolation.md) |
| 10 | Device integration adapters must retain source/provenance for every imported result; a device failure must never corrupt core operational data | Technical/Regulatory | [ADR-0006](../adr/0006-independent-device-gateway.md) |
| 11 | Sensitive data may not be sent to an external AI provider without a pre-approved policy and controls | Ethical/Regulatory | [ADR-0007](../adr/0007-governed-ai-gateway.md) |
| 12 | Hiding a UI element is never itself an Authorization control | Technical/Security | [ADR-0008](../adr/0008-unified-login-and-policy-based-access.md) |
| 13 | The cloud provider must remain replaceable wherever practical; Data Residency must be configurable per market | Technical/Regulatory | [ADR-0009](../adr/0009-saas-first-on-premise-and-hybrid-ready.md) |
| 14 | No data model or contract may hardcode a single language/currency/timezone | Technical | [ADR-0010](../adr/0010-arabic-english-and-localization-first.md) |

## 8. Regulatory and Healthcare-Domain Constraints

Only constraints already Accepted by an ADR or the Constitution are
listed as settled here. Items still genuinely open are listed as
Dependencies, not as constraints — conflating the two would violate the
No-Guessing Rule.

**Accepted:**
- Medical data is highly sensitive (constraint #5 above).
- AI may never issue a final, unreviewed medical decision; mandatory
  Human-in-the-Loop for sensitive AI-assisted actions
  ([ADR-0007](../adr/0007-governed-ai-gateway.md); Constitution §28).
- Authorization is backend-enforced, never UI-only (constraint #4).
- Result Verifier eligibility uses a policy-driven mechanism (OPA),
  Decision D-50 in `docs/certification/10-DECISION-REGISTER.md` — but
  the **actual eligibility values** (e.g., which qualifications a
  Result Verifier must hold per test type) remain an unresolved
  Regulatory Dependency, not yet set. The mechanism is Accepted; the
  values are not.
- National ID is Accepted as a structurally-present, optional Patient
  identifier following the FHIR pattern (D-53) — but the specific
  **validation rules** for it are an unresolved Country Localization
  Dependency.

**Explicitly still open (Dependencies, not constraints the SAD may
assume as settled):**
- General local legal/regulatory requirements
  (`.claude/context/open-questions.md` #2) — still fully Open, part of
  the block of 13 questions the Constitution itself states it did not
  answer.
- Egypt Cross-Border Transfer rules under Law 151/2020 — Requires Legal
  Verification (`R-13`, open-questions.md #25).
- Egypt Labor Law / Social Insurance impact on Payroll — not researched
  at all yet (`R-13`, open-questions.md #26).
- AGPL-3.0 legal exposure across 5 running Engines (`R-04`) — an open,
  High-severity risk; formal legal review is an explicit early-SAD-phase
  workstream, not resolved by this Wave.
- Unconfirmed licenses for 2 Engines, Novu and Documenso (`R-07`).

## 9. Technical and Operational Constraints

- Modular Monolith v1, Selective Service Extraction only on a measured
  trigger ([ADR-0001](../adr/0001-modular-monolith-first.md)).
- Schema per Module; no cross-module database access
  ([ADR-0003](../adr/0003-schema-per-module.md)).
- Tenant isolation must be automatically testable
  ([ADR-0005](../adr/0005-hybrid-tenant-isolation.md)); shared-tier
  partitioning technique is Accepted as PostgreSQL RLS + tenant-ID
  column (D-42).
- Device adapters retain provenance; device failure must not corrupt
  core data ([ADR-0006](../adr/0006-independent-device-gateway.md)).
- No ungoverned sensitive data to an external AI provider
  ([ADR-0007](../adr/0007-governed-ai-gateway.md)).
- Cloud provider replaceable where practical; configurable Data
  Residency ([ADR-0009](../adr/0009-saas-first-on-premise-and-hybrid-ready.md)).
- No hardcoded locale/currency/timezone
  ([ADR-0010](../adr/0010-arabic-english-and-localization-first.md)).
- **Technology Baseline is frozen** — 33 entries (24 Engines including
  Kong Gateway, OpenBao, and PostgreSQL; 4 Libraries; 5 Reference
  Standards; `docs/architecture-review/02-TECHNOLOGY-BASELINE.md`). The
  SAD treats this as fixed input, not subject to re-selection (D-58,
  D-59) — Kong Gateway and OpenBao specifically are approved Version 1
  product selections requiring only implementation due diligence, not
  architectural re-evaluation.
- Eramba Community (GRC/Compliance) is a conditionally approved Version
  1 selection, not subject to re-evaluation during SAD authoring;
  implementation-time due diligence (license, security/maintenance,
  deployment fit, operational ownership, exit-strategy validation)
  remains outstanding (`R-01`).
- Home Collection specifically requires Offline Mode — "local-first
  capture + eventual sync" — Accepted with Constraints (D-48), scoped
  to Home Collection only. This is **not** a platform-wide offline
  requirement.
- Non-Functional Budgets (Constitution §51: latency, throughput,
  availability, RPO/RTO, etc.) are explicitly **Draft with no numeric
  targets** — correctly deferred pending real usage data
  (`.claude/context/open-questions.md` #4; D-54 records only a
  qualitative "launch-scale" Operational Assumption, not a number). The
  SAD must not invent numeric SLA/SLO/RPO/RTO targets to fill this gap;
  doing so would violate the No-Guessing Rule.
- No formal vendor exit-strategy procedure yet exists for any of the 7
  Tier-1 Engines (Keycloak, OPA, ERPNext, OpenBoxes, Kill Bill, Frappe
  HR, openIMIS) — `R-08`, an explicit deliverable of a later SAD Wave,
  not resolved here.

## 10. Assumptions

Only assumptions explicitly recorded as such in governing documents are
listed — nothing here is newly invented for this Wave:

- **D-54**: expected usage volume is a launch-scale Operational
  Assumption; no fixed number is assumed.
- **D-48**: Home Collection requires Offline Mode (local-first capture
  + eventual sync) — Accepted with Constraints, scoped to Home
  Collection only; not generalized to other workflows.
- **D-49**: the architecture assumes it must support all three
  candidate billing/insurance models (Direct, Reimbursement, Capitation)
  as Tenant-configurable, since no single model was confirmed as the
  only one required.
- The Expanded Vision items in `.claude/context/vision.md`
  ("Healthcare Operations Platform," White Label, Plans/Subscriptions,
  Usage/Entitlement Tracking) are treated as **Confirmed context**
  because they were given as explicit, direct user instruction — this
  is different from an ADR-backed Accepted architectural decision, and
  this Wave preserves that distinction rather than blurring it.

## 11. Out-of-Scope Items (of this Document)

- **Out of scope for Wave 1 specifically** (deferred to later Waves per
  `docs/sad/README.md`): Context Diagrams, Bounded Context detail,
  Building Block View, Runtime View, Deployment View, detailed API
  contracts, Quality Attribute numeric scenarios, and detailed Risk
  mitigation planning.
- **Out of scope for the SAD as a whole**, per Constitution §1
  Non-authority: selecting a programming language, framework, cloud
  provider, message broker, database product, AI provider, or frontend
  framework beyond what the Technology Baseline has already fixed;
  constituting legal, medical-regulatory, or compliance certification of
  any kind; replacing the Constitution itself.
- End-user Portal/UX design documentation is entirely out of scope of
  the SAD — that is product/UX documentation, not architecture.
- **Legacy system migration** (`.claude/context/open-questions.md` #13)
  remains a genuinely **Open**, unanswered question — Discovery Phase 08
  explicitly found no basis, confirmed or inferred, to answer it, and
  invented no legacy-system profile. This Wave records that the
  question is still open; it does **not** claim the question has been
  resolved or that no migration will be needed.

## 12. Document Governance and Ownership

Per Constitution §59, this document follows the **Document Lifecycle
Status** vocabulary (`Draft` → `Review` → `Accepted` →
`Deprecated`/`Archived`), a separate vocabulary from the Decision Status
taxonomy (`Draft`/`Proposed`/`Accepted`/`Rejected`/`Superseded`) used for
architectural decisions themselves — this document being in `Review`
status says nothing about whether the decisions it *references* are
Accepted (they are, per §4 above).

Per Constitution §57 (Architecture Review Board): **as a plain fact,
stated by the Constitution itself**, this project currently has one
project owner and no separate architecture team — the ARB is a
function/process fulfilled entirely by the project owner today. This
document's move from `Review` to `Accepted` therefore requires the
project owner's approval, consistent with how every prior Accepted
artifact in this repository (Constitution, all 14 ADRs) was approved.

Ownership of this document (and each subsequent Wave) rests with
whoever authors it, with the project owner as sole approval authority
until a real, multi-person ARB exists (Constitution §57, "Decision
Types and Required Process" table).

## 13. Relationship to the Constitution, ADRs, Baselines, Registers, and Prior Artifacts

| Source | Relationship |
|---|---|
| `docs/constitution/PROJECT-CONSTITUTION.md` (v2.1, Accepted) | Governs; the SAD operationalizes it and never restates or overrides it (§1 above). |
| `docs/adr/0001`–`0014` (14/14 Accepted) | Fixed architectural decisions the SAD designs against; none reopened in this Wave. |
| `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` (33 entries, frozen) | Fixed technology input; the SAD maps design to it, does not re-select from it. |
| `docs/certification/10-DECISION-REGISTER.md` (43 decisions tracked, ID range D-01–D-59, non-sequential) | Cited throughout this Wave for precise decision IDs. |
| `docs/certification/11-RISK-REGISTER.md` (15 risks tracked, 11 open) | Cited in §8–9 above for open Dependencies; full risk treatment is Wave 12. |
| `docs/api-platform/01`–`33` | Fixed API Platform Strategy input, referenced but not re-derived here. |
| `docs/certification/15-SAD-INPUT-PACKAGE.md` | The direct authorization and inheritance package this Wave draws from (§1, §2 above). |
| `docs/certification/23-SAD-READINESS-MATRIX.md` | Confirms input readiness per eventual SAD section; referenced in §2. |
| `.claude/context/*.md` (Context Store) | Draft/Proposed source material — cited with its actual status preserved (Draft/Inferred/Confirmed/Accepted), never silently promoted. |
| `docs/discovery/artifacts/*` | Source for stakeholder/persona and vision-expansion detail (§5, §6, §4.1) — not duplicated in full here. |

## 14. Wave 1 Traceability References

Every substantive claim in this Wave cites its source inline. Summary of
primary sources consulted in full for this Wave:

- `docs/constitution/PROJECT-CONSTITUTION.md` — §1, §2, §3, §4, §5 (principles list), §38, §39, §41, §44, §45, §46, §57, §59, and the "Consolidated Accepted Decisions" appendix.
- `.claude/context/vision.md`, `constraints.md`, `stakeholders.md`, `glossary.md`, `decisions.md`, `architecture-principles.md`, `module-catalog.md`, `open-questions.md`, `README.md`.
- `docs/certification/15-SAD-INPUT-PACKAGE.md`, `23-SAD-READINESS-MATRIX.md`, `10-DECISION-REGISTER.md`, `11-RISK-REGISTER.md`, `26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md`.
- `docs/adr/0001` through `0014` (index-level; full text not required for Wave 1's depth).

No source outside this repository (and the user's direct instructions in
this conversation) was used to produce this Wave.

---

## 15. Wave 1 Review Report

Performed before this Wave was marked ready for the project owner's
Accepted review, per the explicit review protocol given for this Wave.

### Files created

- `docs/sad/README.md` — SAD index and the 13-wave plan.
- `docs/sad/01-introduction-goals-constraints-stakeholders.md` — this
  document.

### Files modified

None. `git status` confirms only the two new files above are new;
nothing in `docs/constitution/`, `docs/adr/`, `.claude/context/`, or any
other existing path was changed.

### Sources consulted (full list)

See §14 above. In full: the Constitution (specific sections listed),
all 9 `.claude/context/` files, 5 certification documents
(`10`, `11`, `15`, `23`, `26`), and the `docs/adr/` index (all 14 titles
and statuses, via `.claude/context/decisions.md`'s ADR Index).

### Consistency and terminology review

- Cross-checked every `D-nn` and `R-nn` citation against
  `docs/certification/10-DECISION-REGISTER.md` and
  `11-RISK-REGISTER.md` directly. **One citation error was found and
  corrected during this review**: Result Verifier eligibility (§8) was
  first drafted citing `D-40` (which is actually the Core Domain
  decision); corrected to the right ID, `D-50`.
  A second inaccuracy was found and corrected in §13: the Decision
  Register was first described as "59 decisions" (the ID ceiling, not
  the count); corrected to "43 decisions tracked, ID range D-01–D-59,
  non-sequential," matching the Register's own Decision Quality
  Summary.
- Verified all 14 ADR links resolve to filenames that actually exist
  under `docs/adr/` (direct `ls` comparison — no broken links).
- Verified every Wave cross-reference (e.g., "Wave 8", "Wave 9") matches
  the exact title in `docs/sad/README.md`'s wave table — two instances
  were tightened to match exactly (Wave 8, Wave 9 rows in §6).
- Verified Status vocabulary is used consistently and never conflated:
  Decision Status (`Draft`/`Proposed`/`Accepted`/`Rejected`/`Superseded`,
  Constitution §40) is kept distinct from Document Status
  (`Draft`/`Review`/`Accepted`/`Deprecated`/`Archived`, Constitution
  §59) throughout — no synonym term ("Confirmed," "Final," "Locked")
  was introduced for either vocabulary beyond what a cited source itself
  already uses (e.g., `vision.md`'s own "Confirmed" labels are quoted,
  not treated as a third status system).
- Verified §4.1's "Confirmed" claims against `vision.md` directly and
  added a clarifying note that the file itself remains `Draft` overall
  even though specific content within it is internally marked
  `Confirmed` — this nuance was underspecified in the first draft and
  tightened during review.

### Points left explicitly incomplete or undecided (by design, not oversight)

Every item below is a genuine open Dependency inherited from prior
phases, not a gap this Wave failed to close — each is listed in §8–§10
above with its own citation:

- AGPL-3.0 legal review outcome (R-04).
- Egypt Cross-Border Transfer, Labor/Social Insurance, and National ID
  validation-rule research (R-13).
- Result Verifier eligibility values (mechanism only is Accepted, D-50).
- Vendor exit-strategy procedures for the 7 Tier-1 Engines (R-08).
- Numeric Non-Functional Budgets / SLA / SLO / RPO / RTO targets
  (Constitution §51, Open Question #4).
- Legacy system migration status — genuinely still Open, not resolved.
- Eramba Community implementation due diligence (R-01).

### Conflicts detected

**None.** No statement in this Wave contradicts an Accepted ADR, the
Constitution, the Technology Baseline, or either Register. No Accepted
decision was reopened, reinterpreted, or silently promoted from a
Draft/Proposed/Open status.

### Verdict

**PASS.**

Two citation-accuracy defects were found and corrected during this
Wave's own review pass (see "Consistency and terminology review"
above) — both fixed before this verdict was issued, not left as
conditions. No unresolved conflict, fabricated fact, or reopened
decision remains.
