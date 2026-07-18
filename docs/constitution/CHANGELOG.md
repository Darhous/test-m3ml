# Project Constitution — Changelog

## v1 — 2026-07-15

**Status:** Accepted

**Summary:** Initial Project Constitution. Establishes the governing
architecture rules for the platform ahead of the detailed Software
Architecture Document, covering: architecture principles (Modular Monolith
First, DDD, Event-Driven Integration, API-First), module/data ownership
rules, multi-tenancy and tenant isolation, authentication/authorization/data
scope, medical device integration, AI governance, localization, and
supporting engineering practices (testing, ADRs, git workflow, definition of
done, exception/amendment process).

**Decisions accepted in this version** (see `docs/adr/` for the individual
records): Modular Monolith First (0001), Domain-Driven Design (0002), Schema
per Module (0003), Event-Driven Integration (0004), Hybrid Tenant Isolation
(0005), Independent Device Gateway (0006), Governed AI Gateway (0007),
Unified Login and Policy-Based Access (0008), SaaS First / On-Premise and
Hybrid Ready (0009), Arabic/English and Localization First (0010).

**Context files updated alongside this version:**
`architecture-principles.md`, `decisions.md`, `glossary.md`,
`open-questions.md`, `constraints.md` (see each file's changes for detail;
history is preserved, not overwritten).

**Not included in this version (explicitly deferred):** final Module
Catalog, Roadmap, Tasks, any technology/language/framework/cloud/broker/
database/AI-provider selection, legal compliance certification.

## v2 — 2026-07-15

**Status:** Accepted

**Summary:** Enterprise Architecture Constitution upgrade. v2 is a strict
superset of v1 — no rule, ADR, or Accepted decision from v1 was changed,
reversed, or reinterpreted. v2 adds 15 new sections (48–62) so the future
Software Architecture Document can cite this Constitution instead of
re-deriving engineering/governance rules: Engineering Principles (23
cross-cutting policies: error handling, logging, observability,
configuration/secrets management, versioning/compatibility, retry/
idempotency/cache/scheduling/background-job/file-processing/integration-
reliability policies), Architecture Fitness Functions (13 automatable/
repeatable checks proving Sections 5–48 hold), Architecture Decision Matrix
(comparative restatement of ADR 0001–0010, no new decisions), Non-Functional
Budgets (all Draft pending real measurement data — no invented numbers),
Architecture Quality Gates (mandatory reviews per artifact type), Module
Acceptance Checklist, Architecture Radar (Adopt/Trial/Assess/Hold, patterns
only, no vendors), Evolution Strategy (measurable triggers for Module→Service
extraction, database splitting, CQRS, Event Sourcing, Search, Cache, Read
Models, Analytics Platform), Repository Governance (CODEOWNERS, templates,
issue labels, release/versioning/commit/PR standards, branch protection,
Definition of Ready — extends Sections 40–43), Architecture Review Board
(decision-type/ADR/RFC/collective-approval matrix), Risk Governance
(Technical/Operational/Clinical/Security/Privacy/Drift/Vendor-Lock-in/
Knowledge risk categories with owners), Documentation Governance (a
document-lifecycle status vocabulary distinct from the decision-status
vocabulary), Glossary Governance, ADR Governance (extends Section 39's
lifecycle with `Draft` and `Deprecated` states), and Constitution Self
Validation (mandatory self-review, answered in Section 62 and in
`REVIEW-REPORT.md`'s v2 Addendum).

**No new ADRs were created and no existing ADR was modified in v2** — v2 is
governance/process structure built entirely on the 10 already-Accepted
decisions (see Section 50, Architecture Decision Matrix).

**Context files:** no new top-level Accepted architectural decision emerged
from this upgrade, so `.claude/context/decisions.md` records this as a note
rather than a new decision row (see that file's v2 note). No other context
file required a substantive update beyond that note — v2 did not answer any
existing Open Question, and no principle changed status.

**Review:** `docs/constitution/REVIEW-REPORT.md` "v2 Addendum" — 2
contradictions found and resolved (Document Status vs. Decision Status
vocabularies; ADR lifecycle extension), 3 new Open Risks logged (R6–R8,
none blocking), v1's R1/R2 (DoS/rate-limiting, incident response) remain
open and unaddressed by design (out of this task's scope).

**Not included in this version (still explicitly deferred):** final Module
Catalog, Roadmap, Tasks, Software Architecture Document, Discovery work, any
technology/language/framework/cloud/broker/database/AI-provider selection,
legal compliance certification, and all numeric Non-Functional Budgets
(Section 51, Draft pending real data).

## v2.1 — 2026-07-18

**Status:** Accepted

**Amendment type:** minor, non-substantive — per Section 45 (Constitution
Amendment Process). Authorized by explicit user instruction (the "Final
Pre-SAD Semantic Consistency Correction" mission).

**Reason:** a semantic consistency review (2026-07-18) found active
governing text in this Constitution that no longer reflected the current
architecture baseline, though it was accurate when v2 was written:
Section 51's Non-Functional Budgets table stated, for the RTO and RPO
rows, that disaster-recovery design and database-engine selection were
entirely undesigned/unchosen — stale once ADR-0013 (PostgreSQL as the
Primary Relational Database) and ADR-0014 (Disaster Recovery and Business
Continuity Baseline) were Accepted, both 2026-07-18. Separately, Section 6
and the Section 47 Glossary stated the Core Domain was "not yet
identified" and Section 46 presented its 14-item Open Questions list as
"still Open" — both stale once the Core Domain (ADR-0011) and all 31
tracked Open Questions were resolved, also 2026-07-18, in the Open
Questions Resolution phase. In every case, only the *reason a value is
still Draft/Open* was corrected; no numeric value was introduced and no
Constitution rule was reversed.

**Exact sections changed:**
- Title, Status line, and "v2 note" paragraph (version metadata: v2 → v2.1;
  added a v2.1 note describing this amendment's scope).
- Section 51 (Non-Functional Budgets): the RTO and RPO rows' *Reason /
  Basis* column only. The *Value* (`Not set`) and *Status* (`Draft`)
  columns are unchanged — no numeric RTO, RPO, availability, retention, or
  topology figure was introduced. No other row in Section 51 was touched.
- Closing statement ("End of Project Constitution...") updated to v2.1 and
  to note the database/DR cross-references without changing its underlying
  claim that this Constitution does not itself state a product choice as
  one of its own rules.
- Section 6 (Strategic Design area): the Core Domain "Recommendation (not
  yet a Rule)" paragraph now carries an update note — the Core Domain was
  identified and Accepted (ADR-0011, "Patient-to-Result Orchestration") in
  the Open Questions Resolution phase. The underlying principle (Core
  Domain warrants the deepest modeling investment, no anemic Core Domain
  objects) is unchanged.
- Section 47 Glossary table: the "Core Domain" row's Status column updated
  from "Open — not yet identified" to Accepted, citing ADR-0011.
- Section 46 (Open Questions): a header-level update note added stating all
  14 listed items were subsequently resolved (`20-OPEN-QUESTIONS-
  RESOLUTION.md`). The 14-item list itself is preserved unmodified as the
  historical record of what was open at v1/v2 authoring — individual items
  were not rewritten, per the smallest-compliant-amendment principle.
- `docs/constitution/README.md`'s Version line, corrected from a
  pre-existing stale "v1" to the current version (a documentation-currency
  fix discovered while reviewing README as required by Section 45, not
  itself part of the RTO/RPO substance).

**References:** `docs/adr/0011-core-domain-test-processing-and-result-
verification.md`, `docs/adr/0013-postgresql-as-primary-relational-
database.md`, `docs/adr/0014-disaster-recovery-and-business-continuity-
baseline.md`, `docs/certification/20-OPEN-QUESTIONS-RESOLUTION.md`,
`docs/certification/26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md`.

**Confirmation:** no architectural principle, ADR, or previously Accepted
rule was reversed, reopened, or reinterpreted. Sections 1–50 and 52–62 are
unchanged in substance. No new ADR was created by this amendment — it
documents two already-Accepted ADRs, it does not decide anything new.

**Not included in this version (still explicitly deferred):** everything
listed as deferred in v2 above, unchanged. Numeric RTO, RPO, Availability,
and all other Non-Functional Budgets remain Draft pending real measurement
data, business approval, regulatory validation, and deployment-topology
decisions.
