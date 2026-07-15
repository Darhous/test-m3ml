# 0002: Domain-Driven Design

## Status

Accepted

## Context

The platform is explicitly "not a plain CRUD system" (vision.md) and must
support meaningfully different domains (Laboratory, Identity/Access,
Organization, Patient, Device Integration, Billing, etc.) each with its own
rules and language, while still composing into one coherent, modular
platform (ADR 0001). A modeling approach is needed that keeps these domains
distinct in language and rules, without collapsing into either (a) one
unified anemic model for everything, or (b) fully independent services with
no shared discipline.

## Decision

The platform uses **Domain-Driven Design** as its modeling approach:
Bounded Contexts define model/language boundaries (not deployment units),
Ubiquitous Language is used in code/contracts/events, and within each
Bounded Context, Entities, Value Objects, Aggregates (small, single-root),
Domain Events, and Repositories are the standard building blocks. Module
boundaries (ADR 0001) are derived from Bounded Contexts.

## Alternatives Considered

- **Generic technical layering only (MVC-style, no domain modeling).**
  Rejected: produces anemic models and scattered business logic, directly
  conflicting with "not a plain CRUD system," and gives no principled way
  to draw module boundaries.
- **Data-model-first design (design database schema, derive everything
  from it).** Rejected: couples the domain model to storage details and
  tends to produce one shared schema/model across unrelated domains,
  conflicting with Schema per Module (ADR 0003).
- **Domain-Driven Design (Strategic + Tactical).** **Chosen.** Provides an
  explicit method for both drawing Bounded Context boundaries (Strategic)
  and structuring the code inside each one (Tactical), and is explicitly
  compatible with "Modular Monolith first" (a Bounded Context is a model
  boundary, not automatically a microservice).

## Positive Consequences

- Module boundaries have a principled basis (Bounded Contexts) rather than
  being arbitrary or purely technical.
- Ubiquitous Language reduces ambiguity between domain experts (e.g.,
  Laboratory Staff, Doctors) and the platform's model.
- Tactical patterns (Aggregates, Domain Events) give a concrete, consistent
  way to enforce consistency boundaries and enable event-driven integration
  (ADR 0004).

## Negative Consequences

- Requires ongoing collaboration with domain experts (Stakeholders) to keep
  the model accurate — a cost the team must actually pay, not just adopt in
  name.
- Learning curve for contributors unfamiliar with DDD terminology and
  patterns.

## Risks

- **Cargo-cult DDD**: adopting DDD vocabulary without genuine domain-expert
  collaboration, resulting in the same anemic-model problem under different
  names. Mitigated by the DDD Quick Diagnostic review at each Bounded
  Context's design time (Constitution Section 6).
- **Bounded Context misidentified as microservice**, undermining ADR 0001.
  Mitigated by explicit Constitution language (Section 6/7) and context
  mapping review.

## Verification

- DDD consistency review (Quick Diagnostic, 7-row checklist) performed for
  each new Bounded Context.
- Context Map document exists and labels every inter-context relationship
  with a named pattern (Constitution Section 7).

## Revisit Triggers

- A specific Bounded Context's domain proves too simple/generic to justify
  full tactical DDD (e.g., a pure Generic Subdomain) — in that case a
  lighter internal design may be used for that context specifically,
  without abandoning DDD platform-wide.
- Strategic Design work (identifying the Core Domain — Constitution Section
  46, item 14) may refine, but does not reverse, this decision.
