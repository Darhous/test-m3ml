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
