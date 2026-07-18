# API Vision

**Authority:** Enterprise API Architecture Board, acting after and
subject to the Enterprise Adoption Review (`docs/architecture-review/`)
and the frozen Technology Baseline. This document does not redesign,
re-derive, or contradict any Accepted Constitution section, ADR, or
Baseline entry — it defines the API surface that sits on top of them.

## Vision Statement

The platform's API is not an add-on to a web application — it **is**
the platform. Per the project's own description (CLAUDE.md), the
long-term goal is "a broad, extensible healthcare platform with a
central backend, a unified login, and role/permission/data-scope/
organization/branch-based routing to the right Portal/Dashboard." Every
Portal, every Dashboard, every future Module, and every external
integration is, and must remain, a consumer of the same governed API
surface — there is no privileged internal shortcut that bypasses API
contracts. (**Fact**, derived directly from the project description and
from Architecture Principle #9, API-First Design, Accepted via
ADR-0001's decision block.)

## Goals

1. **One backend, many front doors.** A single, consistent, versioned
   API surface serves web Portals, mobile clients, Admin Dashboards,
   and (in a later phase) Partner and Public consumers — never a
   Portal-specific backend fork. (**Fact**, Constitution-derived: "a
   central backend... routing to the right Portal/Dashboard.")
2. **Contracts before code.** Every API is designed as an explicit,
   reviewable contract before implementation, consistent with the
   Contract-First principle this phase is required to apply.
   (**Recommendation** — the specific contract notation, e.g. OpenAPI,
   is explicitly Part 2 scope; this phase commits only to the
   *discipline*, not the tooling.)
3. **Domain-aligned, not database-aligned.** API resources map to
   Bounded Context Aggregates (`TestOrder`, `Specimen`, `TestResult`,
   `Invoice`, ...) as named in `.claude/context/glossary.md`, never to
   raw database tables. (**Fact**, ADR-0002 Domain-Driven Design,
   Accepted.)
4. **Zero Trust by default.** No API call — internal, Partner, or
   Public — is trusted by network position alone; every call is
   authenticated and authorized at the boundary. (**Recommendation**,
   this phase's assigned Architectural Principle, not yet an
   independent ADR.)
5. **Multi-tenant safe by construction.** Every API response is
   provably scoped to the caller's Tenant/Organization/Branch/Data
   Scope — cross-tenant leakage is a defect class the API layer is
   designed to make structurally hard, not merely tested for. (**Fact**,
   ADR-0005 Hybrid Tenant Isolation, Accepted; extended architecturally
   here.)
6. **Backward-compatible evolution.** The platform will run for years
   and accumulate Modules; the API layer must let new Modules and new
   API versions ship without breaking existing Portal/Partner
   consumers. (Architecture Principle #19, currently **Draft** per
   `.claude/context/architecture-principles.md` — this phase treats it
   as a working design goal, not a silently-promoted Accepted
   principle; see `15-ADR-REVIEW.md`.)
7. **Enterprise-grade developer experience for internal teams first.**
   Before any external Partner or Public developer touches this
   platform (Part 2 scope), the platform's own Module teams must
   experience the API layer as consistent, predictable, and
   well-governed. Internal DX is the proving ground for external DX.

## Non-Goals (for this Board, this phase)

- **Not** designing OpenAPI/Swagger specifications, SDKs, a Developer
  Portal, a Marketplace, billing/monetization of API access, Webhooks,
  an Event Catalog, Integration Contracts, Observability tooling, SLAs,
  API analytics, or an API roadmap — all explicitly reserved for
  **Part 2** per this phase's Stop Conditions.
- **Not** re-opening Discovery, Build-vs-Buy, or the Technology
  Baseline. Every Engine cited in this document set (Keycloak, OPA,
  RabbitMQ, Kill Bill, etc.) is treated as frozen input.
- **Not** selecting an API Gateway product or a Secrets/Vault Engine —
  neither has a ratified Technology Baseline entry (see `10` and `12`);
  selecting one would be a Build-vs-Buy act this Board is not
  authorized to perform in this phase.
- **Not** changing Bounded Contexts, the Module Catalog, or any ADR's
  Decision section. Where ADR-0011/0012 remain Proposed, they remain
  Proposed (see `15-ADR-REVIEW.md`).

## API Philosophy

**API-First, Contract-First, Domain-Driven.** Concretely:

- An API is designed from the consumer's need and the domain model
  first; the implementation is fit to the contract, not the reverse.
- REST (resource-oriented, HTTP-semantic) is the default paradigm for
  this platform's APIs. (**Recommendation**: no ADR has evaluated
  REST against GraphQL for this platform specifically; REST is
  recommended because it is the paradigm implicitly assumed throughout
  `docs/reuse/`'s Engine API surfaces — Keycloak, ERPNext, OPA, Kill
  Bill, openIMIS all expose REST APIs — and adopting a second paradigm
  platform-wide would add integration complexity with no documented
  driver. This is a Recommendation for API Governance to ratify, not
  a Decision this Board can unilaterally make final.)
- Every external Engine (the 21 ratified Engines in the Technology
  Baseline) is wrapped behind this platform's own API and an
  Anti-Corruption Layer — no Engine's native API is ever exposed
  directly to a Portal, Partner, or Public consumer. (**Fact**,
  Constitution's Accepted "Anti-Corruption Layer" definition, ADR-0006/
  ADR-0007.)

## Platform Positioning

The platform's API is positioned as **enterprise infrastructure**, not
a thin CRUD wrapper — consistent with CLAUDE.md's explicit framing
("Not a plain CRUD system"). It is the single integration point for:

- Internal Portals/Dashboards (today).
- Device data ingestion via the Device Integration Gateway (today,
  Independent Component).
- AI-assisted operations via the governed AI Operations Gateway
  (today, Human-in-the-Loop enforced).
- Future Partner integrations (referring clinics, insurers, corporate
  clients) and a future Public developer surface (Part 2).

## Developer Experience Vision

For the platform's own engineers (the only audience in scope for Part
1): a Module team should be able to answer, from this document set
alone and without asking another team, (1) what type of API their
Module is allowed to expose, (2) what it must be named, (3) how it is
versioned, (4) how a caller is authenticated and authorized, and (5)
what security and multi-tenancy guarantees they must uphold. Meeting
that bar for internal teams first is the necessary foundation for any
future external-developer-facing DX work in Part 2.
