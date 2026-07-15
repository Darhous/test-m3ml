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
