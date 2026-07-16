# Discovery Book — Digital Healthcare Platform (Laboratory Management)

**Status:** Discovery Complete (Assumption-Driven Autonomous Run) —
Candidate/Proposed content throughout, pending user review. **This is not
a Software Architecture Document** and does not authorize starting one.
**Execution mode note (read first):** this entire Discovery Program ran
without live stakeholder access, under a user-approved
"Assumption-Driven Autonomous Run" (see `reports/
00-discovery-program-status-report.md`). Every finding not explicitly
Confirmed in `.claude/context/` before this run is tagged `Inferred —
Industry Reference` in `artifacts/ASSUMPTION-REGISTER.md`. Read this book
as a well-structured *hypothesis*, not a confirmed business reality.

---

## 1. Executive Summary

Discovery ran all 12 playbooks (`docs/discovery/prompts/01`–`12`) in the
governed order, producing a complete candidate domain model for the
platform's Laboratory Management starting point: 20 business capabilities,
4 traced value streams, 26 domain events, 11 candidate subdomains (1 Core,
7 Supporting, 3 unevidenced), 8 formal Bounded Contexts with a fully-labeled
Context Map, a full business-rules/state-machine layer with 3 identified
Sensitive Operations, an integration inventory (2 device, 1 external payer,
1 explicit empty legacy placeholder), a tenancy/localization gap analysis,
and 7 accepted + 1 rejected + 1 not-ready AI use case. Phase 11 Validation
found zero unresolved contradictions and zero unmitigated/unowned security
threats. Phase 12 authored 2 new ADRs (0011, 0012) — both **Proposed, not
Accepted**, because the entire evidentiary base is Inferred, not
stakeholder-confirmed.

**Readiness for Software Architecture work:** see
`reports/12-discovery-completion-report.md`, Section "Readiness
Assessment," for the full honest breakdown (process readiness vs. content
confirmation readiness are reported separately, not blended into one
number).

## 2. Business Context

**Source:** `artifacts/02-business-capability-map.md`,
`artifacts/02-value-streams.md`, `.claude/context/stakeholders.md`
(Discovery Phase 02 section), `artifacts/12-persona-catalog.md`.

20 business capabilities spanning Order Management, Specimen Management,
Test Processing, Notification, Billing, Device Integration, Quality
Control, Staff/Operations, Identity, and Organization — classified into
Candidate Core/Supporting/Generic tiers. 4 value streams traced: Walk-in
Test Order (VS1), Home Sample Collection (VS2), Specimen Rejection/
Recollection (VS3), and Insurance Claim Billing (VS4, the least evidenced).
All 15 stakeholder categories from `stakeholders.md` refined with candidate
needs; 4 personas detailed at higher fidelity (Patient, Doctor, Laboratory
Staff, Laboratory Management).

## 3. Event Model

**Source:** `artifacts/03-event-storming-board.md`,
`artifacts/12-command-catalog.md`, `diagrams/03-event-storming-timelines.md`.

26 domain events (plus 4 later-identified gaps: `ResultCorrected`,
`ClaimDenied`, `TestProcessingFailed`, `HomeVisitFailed`) across the 4
value streams, with 5 candidate Pivotal Events (`ResultVerified`,
`ResultReleased`, `SpecimenAccessioned`, `SpecimenRejected`,
`ClaimAdjudicated`) and 10 Hotspots, all resolved at the modeling level or
explicitly left Open (see `artifacts/07-business-rules-catalog.md`'s
Hotspot Resolution Summary).

## 4. Subdomain Map

**Source:** `artifacts/04-subdomain-map.md`, `diagrams/04-subdomain-map.md`.

11 candidate Subdomains. **Core (Proposed, ADR 0011):** Test Processing and
Result Verification. **Supporting (well-evidenced):** Order Management,
Specimen Management, Billing and Claims, Device and Equipment Integration.
**Generic:** Notification and Communication, Identity and Access,
Organization and Branch Management. **Supporting (weak evidence, flagged,
not tactically modeled):** Inventory and Reagent Management, Quality
Control and Accreditation Compliance, Staff and Operations Management.

## 5. Domain Model

**Source:** `artifacts/05-candidate-aggregates.md`,
`diagrams/05-candidate-aggregates.md`, `.claude/context/glossary.md`
(Discovery sections).

Candidate Aggregates: `TestOrder`/`TestCatalogEntry` (Order Management),
`Specimen` (Specimen Management), `TestResult` (Test Processing — smallest,
most tightly guarded consistency boundary in the model), `Invoice`/`Claim`
(Billing and Claims, kept separate), `NotificationRequest` (Notification,
deliberately shallow per Generic-Subdomain modeling discipline),
`DeviceImportRecord` (Device Integration). Every Entity/Value-Object
classification passed its DDD test explicitly; no Aggregate embeds another
by object reference.

## 6. Bounded Contexts and Context Map

**Source:** `artifacts/06-bounded-contexts.md`, `artifacts/
06-context-map.md`, `diagrams/06-context-map.md`,
`diagrams/06-c4-system-context.md`.

8 Bounded Contexts (ADR 0012, Proposed), 11 Context Map relationships, zero
unlabeled. Confirmed acyclic Module Dependency graph. The Specimen
Management / Test Processing split was the single most consequential
judgment call in Discovery (see ADR 0012's Alternatives Considered) — kept
separate on Core/Supporting classification + actor + Pivotal Event
evidence, flagged for scrutiny (Risk #8). Patient and Doctor remain
cross-context Actors with no owned Bounded Context (Risk #7) — a possible
gap, not a confirmed finding.

## 7. Business Rules

**Source:** `artifacts/07-business-rules-catalog.md`,
`artifacts/07-workflow-state-machines.md`, `diagrams/07-state-machines.md`.

Full invariant catalog and 4 state machines (`TestOrder`, `Specimen`,
`TestResult`, `Claim`), every transition explicitly actor-gated. 3
Sensitive Operations identified — `ResultVerified`, `ResultReleased`,
`ResultCorrected` — all concentrated in the Core Subdomain, all gated to a
dedicated **Result Verifier Role** distinct from general Laboratory Staff
(eligibility criteria itself remains Open, `open-questions.md` #19, flagged
as the single highest-priority Open Question in this Discovery run given
its direct clinical-safety weight).

## 8. Integrations

**Source:** `artifacts/08-integration-inventory.md`,
`diagrams/08-integrations.md`.

2 device integrations (Lab Analyzer, Portable Collection Device), 1
external payer integration (Anti-Corruption Layer + Conformist pattern), 1
explicit empty Legacy System placeholder (zero basis to invent one), 5
candidate notification channels. Every external boundary has an assigned
Context Mapping pattern and a first-pass (later completed in Phase 11)
STRIDE note.

## 9. SaaS Platform Findings

**Source:** `artifacts/09-tenancy-analysis.md`, `artifacts/
09-localization-analysis.md`, `artifacts/12-saas-opportunity-report.md`,
`diagrams/09-tenant-isolation.md`.

Every candidate Aggregate found missing explicit Tenant-scoping (expected
at this modeling stage, flagged for mandatory SAD-level addition). 2
localization gaps found and design-proposed (`Money` Value Object,
dual-timestamp pattern). `open-questions.md` #15/#16 narrowed to 2
data-partitioning categories and a trigger-type, with no number invented.
#3/#4 (hosting detail, scale) explicitly left unnarrowed — no evidence
existed to narrow them.

## 10. AI Use Cases

**Source:** `artifacts/10-ai-use-case-catalog.md`,
`diagrams/10-ai-use-cases.md`.

7 AI use cases accepted (all within Constitution Section 28's Permitted
list, each with an explicit Human-in-the-Loop or Data-Scope-filtering
design), 1 rejected outright (auto-verifying normal results — a direct
Forbidden-list match), 1 flagged Not Ready (notification summarization —
Permitted by the literal rule text but carrying a practical risk the
Forbidden list doesn't address; escalated as possible Constitution feedback
in the Completion Report, not resolved unilaterally by Discovery).

## 11. Validation Summary

**Source:** `reports/11-validation-report.md`, `reports/
11-stride-mitigation-mapping.md`.

3 contradictions found, all resolved (2 correctly identified as
non-violations, 1 as a genuine Constitution coverage gap correctly
escalated rather than patched). 0 duplications. DDD Consistency: 6 PASS, 1
Partial (expected). Full STRIDE: 29 threats across 4 integration surfaces +
2 AI patterns (corrected 2026-07-16, Gap Closure Wave 0; previously
miscounted as 32), all mitigated or explicitly accepted-with-owner (2 accepted
risks tie to the pre-existing Denial-of-Service policy gap already logged
in `docs/constitution/REVIEW-REPORT.md` Open Risk R1 — not a new gap).
27/27 diagrams pass syntax validation. 11/11 touched Open Questions
accurately reflected. Reader Test passed.

## 12. New ADRs (Proposed, Not Accepted)

- **ADR 0011** — Core Domain: Test Processing and Result Verification.
- **ADR 0012** — Candidate Bounded Context Map (8 Contexts).

Both explicitly `Proposed` rather than `Accepted` — see each ADR's "Why
Proposed, Not Accepted" section. This is a deliberate deviation from
Playbook 12's default instruction, made because the No-Guessing Rule
outranks a Discovery-execution-mode default when the two conflict.

## 13. Full Deliverable Index

| Requested Deliverable | Location |
|---|---|
| Business Discovery Book | This document |
| Stakeholder Catalog | `.claude/context/stakeholders.md` (Discovery Phase 02 section) |
| Persona Catalog | `artifacts/12-persona-catalog.md` |
| Capability Catalog | `artifacts/02-business-capability-map.md` |
| Value Stream Catalog | `artifacts/02-value-streams.md` |
| Customer Journey Catalog | `artifacts/02-value-streams.md` (closest equivalent — no separate emotional/UX journey data was gathered; would require real user research, not fabricated here) |
| Event Catalog | `artifacts/03-event-storming-board.md` |
| Command Catalog | `artifacts/12-command-catalog.md` |
| Policy Catalog | `artifacts/07-business-rules-catalog.md` (Cross-Aggregate Policies section) |
| Business Rule Catalog | `artifacts/07-business-rules-catalog.md` |
| Domain Catalog | `artifacts/04-subdomain-map.md` |
| Domain Models | `artifacts/05-candidate-aggregates.md`, `diagrams/05-candidate-aggregates.md` |
| Ubiquitous Language | `.claude/context/glossary.md` (Discovery Phase 03–06 sections) |
| Aggregate Catalog | `artifacts/05-candidate-aggregates.md` |
| Context Map | `artifacts/06-context-map.md` |
| Integration Catalog | `artifacts/08-integration-inventory.md` |
| Device Catalog | `artifacts/08-integration-inventory.md` (Device Integration sections) |
| AI Opportunity Report | `artifacts/10-ai-use-case-catalog.md` |
| SaaS Opportunity Report | `artifacts/12-saas-opportunity-report.md` |
| Risk Register | `artifacts/RISK-REGISTER.md` |
| Assumption Register | `artifacts/ASSUMPTION-REGISTER.md` |
| Open Questions Register | `artifacts/OPEN-QUESTIONS-REGISTER.md` + `.claude/context/open-questions.md` |
| Candidate Module Catalog | `.claude/context/module-catalog.md` (Candidate Contexts from Discovery section) |
| Discovery Readiness Report | `reports/12-discovery-completion-report.md`, Section "Readiness Assessment" |

## 14. What This Book Deliberately Does Not Contain

No Software Architecture Document content, no API design, no database
design, no deployment design, no programming language/framework/cloud
provider/AI-provider selection, no production code — identical boundary to
the Constitution itself (Section 1) and explicitly required by this
Discovery task's own instructions.
