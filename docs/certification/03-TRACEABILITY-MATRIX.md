# Traceability Matrix

Full chain verification: Vision → Business Goals → Enterprise
Objectives → Architecture Principles → Constitution → ADRs → Discovery
→ Reuse Intelligence → Technology Baseline → API Strategy → Roadmaps →
Architecture Decisions → Future SAD Inputs. Every link below is cited
by exact file path; a missing link is explicitly called out, not
silently skipped.

## The Chain

| Layer | Artifact | Traces From | Traces To |
|---|---|---|---|
| Vision | `.claude/context/vision.md` | Original project description (CLAUDE.md project description) | Constitution §3 (Vision) |
| Business Goals / Enterprise Objectives | `.claude/context/vision.md` "Expanded Vision" section, `docs/discovery/artifacts/W1-vision-scope-operating-model.md` | Vision | Discovery's 32-Business-Domain scope, Constitution §2 (Scope) |
| Architecture Principles | `.claude/context/architecture-principles.md` (19 original + 6 v2 principles) | Vision, Constitution v1/v2 | Constitution §5 (Architecture Principles); each Accepted principle links to its ADR |
| Constitution | `docs/constitution/PROJECT-CONSTITUTION.md` (62 sections, v1+v2) | Architecture Principles, user-approved decisions | ADRs 0001-0010 (v1), Constitution §48-62 (v2, no new ADRs) |
| ADRs | `docs/adr/0001`-`0012` | Constitution decisions (0001-0010), Discovery Wave 7/9 findings (0011-0012) | Discovery's use of the Bounded Context Map, Reuse program's Core-Domain-preservation logic, API Platform's `15-ADR-REVIEW.md` |
| Discovery | `docs/discovery/` (99 files: 12 baseline phases + 15 Gap Closure waves) | Vision, Constitution, `domain-driven-design` Skill methodology | `.claude/context/module-catalog.md`'s 28-Module Catalog, `docs/reuse/MASTER_FEATURE_CATALOG.md`'s 106-Feature scope |
| Reuse Intelligence | `docs/reuse/` (1,396 files: 18 Master + 28 Module dirs) | Discovery's 28-Module/106-Feature scope | `docs/architecture-review/02-TECHNOLOGY-BASELINE.md`'s frozen 30-entry table |
| Technology Baseline | `docs/architecture-review/` (14 files, EARB phase) | Reuse Intelligence (ratification, not re-research) | API Platform Parts 1-2 (`docs/api-platform/`), this Certification Audit |
| API Strategy | `docs/api-platform/` (34 files, Parts 1-2) | Constitution, ADRs, Technology Baseline (all as fixed input) | `docs/api-platform/30-ROADMAP.md`, `31-ENTERPRISE-PRODUCT-DECISIONS.md`, this Certification Audit |
| Roadmaps | `docs/api-platform/30-ROADMAP.md` | API Strategy's own dependency graph | Future SAD (Near/Mid/Long-Term horizons) |
| Architecture Decisions (consolidated) | `docs/certification/10-DECISION-REGISTER.md` (this audit) | Every layer above | Future SAD Input Package (`15-SAD-INPUT-PACKAGE.md`) |
| Future SAD Inputs | `docs/certification/15-SAD-INPUT-PACKAGE.md` | This entire chain | Software Architecture Document (next phase, not started here) |

## Traceability by Specific Decision Thread (worked examples)

### Thread: Multi-Tenancy

`.claude/context/vision.md` ("SaaS Multi-Tenant") → Constitution §18-19
(Multi-Tenancy Rules, Tenant Isolation Rules) → ADR-0005 (Hybrid Tenant
Isolation, Accepted) → Discovery Phase 09 (`09-saas-platform-report.md`,
tenancy-technology analysis) → `.claude/context/open-questions.md` #15
(partitioning technology, still Open) → `docs/reuse/tenant-and-
organization-management/` research → `docs/architecture-review/
02-TECHNOLOGY-BASELINE.md` R4 (PostgreSQL RLS, Reference only) →
`docs/api-platform/14-MULTI-TENANCY.md` (API-layer application,
explicitly partitioning-technology-agnostic). **Unbroken, with the one
genuine open link (#15) explicitly carried forward at every step, never
silently closed.**

### Thread: Core Domain

Discovery Phase 04 (`04-subdomain-map.md`, Inferred) → Gap Closure Wave
7 (`GAP-CLOSURE-07-DOMAIN-CLASSIFICATION.md`, re-evaluated against 6
alternatives) → ADR-0011 (Proposed — Amended) → `.claude/context/
open-questions.md` #14 (still Open) → EARB `docs/architecture-review/
10-ADR-REVIEW.md` (re-confirmed Proposed, verified no Core Domain
leakage across 7 Modules) → API Platform `docs/api-platform/
15-ADR-REVIEW.md` (independently re-verified: no architectural
conflict, but "fully supported by all previous phases" bar not met,
still not promoted). **Unbroken, and notably the same conclusion was
independently re-derived three separate times (Discovery, EARB, API
Platform) rather than merely copy-forwarded — the strongest possible
traceability signal for a still-open item.**

### Thread: AGPL Licensing

`docs/reuse/MASTER_LICENSE_MATRIX.md` (original per-repository finding)
→ `docs/reuse/MASTER_READINESS_REPORT.md` Section 3 (flagged as
requiring legal verification) → `docs/architecture-review/
07-LICENSE-REVIEW.md` (EARB license-family review) → `08-AGPL-LEGAL-
CHECKLIST.md` (7-item actionable checklist) → `11-RISKS.md` R-04/R-07
→ `13-READINESS-FOR-API-STRATEGY.md` (named as a blocking item for
*finalizing* specific contracts) → `docs/api-platform/
21-INTEGRATIONS.md`'s Partner Certification checklist (requires this
clearance before Publish) → `docs/certification/11-RISK-REGISTER.md`
(this audit, carried forward unresolved). **Unbroken across 8 documents
spanning 3 phases.**

### Thread: API Gateway / Secrets Vault Product Selection

Emerged fresh in `docs/api-platform/10-API-GATEWAY.md` and
`12-SECRETS-AND-KEYS.md` (Part 1) → `.claude/context/open-questions.md`
#28-29 → `docs/api-platform/31-ENTERPRISE-PRODUCT-DECISIONS.md` (Part
2, evaluated, left Open with justification) → this audit's
`12-OPEN-QUESTIONS-REGISTER.md` (carried forward, flagged as
SAD-blocking for finalization, not SAD-blocking for starting). **New
thread, correctly originated at the point the gap was first discovered
(no retroactive insertion into an earlier phase), and consistently
tracked since.**

## Missing Links — Explicitly Highlighted

| Gap | Where It Breaks | Severity |
|---|---|---|
| Business Goals / Enterprise Objectives have no dedicated top-level artifact distinct from Vision | The mission's abstract chain names "Business Goals" and "Enterprise Objectives" as distinct layers; this repository's actual practice folds them into `vision.md` and Discovery's Business Discovery phase (`docs/discovery/reports/02-business-discovery-report.md`) rather than maintaining a separate document | Low — content exists, only the naming/document-separation the abstract chain implies is absent. Not a defect the repository's own conventions require fixing; noted for the SAD to decide whether a dedicated Business Goals artifact is warranted. |
| No single document lists "Requirements" as a distinct artifact type | This repository uses Discovery's Business Rules (`docs/discovery/reports/07-business-rules-report.md`) and Constitution's rule-sections as the requirements-equivalent; no separate "Requirements" document exists | Low — same reasoning as above; requirements are distributed by design (DDD-aligned, not a monolithic requirements doc), consistent with Constitution's own architecture-principles-first approach |
| ADR-0011/0012 → downstream "Accepted" state | Genuinely absent, not a broken link — these ADRs remain Proposed by design, and every downstream document correctly reflects that rather than assuming a future Accepted state | Medium — tracked as the single most important open item for SAD readiness, not a traceability defect |

## Traceability Verdict

**Full traceability confirmed** for every decision thread checked, with
the two "missing links" being intentional structural choices (content
exists, distributed differently than the abstract chain's naming
implies) rather than actual breaks, and the one genuine open node
(ADR-0011/0012 Proposed status) being correctly and consistently
represented as open at every point in the chain rather than silently
closed anywhere.
