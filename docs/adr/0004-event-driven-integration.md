# 0004: Event-Driven Integration

## Status

Accepted

## Context

With Schema per Module (ADR 0003) forbidding direct cross-module data
access, modules still need to react to what happens in other modules (e.g.,
Billing reacting to a Laboratory result being verified, Notification
reacting to a sample being collected). A cross-module communication style
is needed that preserves module autonomy (no caller depending on callee's
internals) and tolerates modules evolving independently within a single
deployable (ADR 0001).

## Decision

Cross-module side effects that other modules react to are expressed as
**Domain Events (internal to a Bounded Context) and Integration Events
(cross Bounded Context/Module)**. Integration Events are immutable, past-
tense facts, explicitly versioned, and published through a deliberate
translation from internal Domain Events — never broadcast as-is. Direct
synchronous request/response through an approved API contract remains
available when a caller needs an immediate answer (e.g., an authorization
check), but is not used for propagating side effects across module
boundaries.

## Alternatives Considered

- **Synchronous calls only (module A calls module B's internal service
  directly for every interaction).** Rejected: creates tight coupling,
  makes failure handling and consistency reasoning harder as more modules
  are added, and directly undermines Module Dependency Rules (no depending
  on another module's internals).
- **Shared database triggers/polling for cross-module reaction.**
  Rejected: conflicts with Schema per Module (ADR 0003) and hides the
  integration contract inside database internals instead of an explicit,
  reviewable event schema.
- **Event-Driven Integration via explicit, versioned Integration Events,
  synchronous API calls reserved for immediate-answer needs.** **Chosen.**
  Matches the platform's stated API-First/Event-Driven direction
  (vision.md) and keeps modules temporally decoupled for side effects while
  still allowing synchronous calls where genuinely needed.

## Positive Consequences

- Modules can evolve and fail independently for asynchronous side effects
  (e.g., Notification being briefly down does not block Laboratory result
  verification).
- Natural audit/traceability trail: the event stream documents what
  happened across the platform (supports Section 23, Audit and
  Traceability Rules).
- New modules can subscribe to existing events without the publishing
  module changing.

## Negative Consequences

- Requires designing for eventual consistency between modules — a
  correctness mental-model shift from purely synchronous systems.
- Requires event schema versioning discipline; without it, breaking changes
  ripple silently to consumers.

## Risks

- **Ordering/duplicate delivery assumptions**: consumers built assuming
  exactly-once, in-order delivery when no such guarantee is documented.
  Mitigated by Constitution Section 34 (Reliability and Resilience Rules)
  requiring idempotent, redelivery-tolerant consumers unless a stronger
  guarantee is explicitly documented for a specific event.
- **Domain event leaking as integration contract**, coupling consumers to
  another module's internal model. Mitigated by Constitution Section 12
  requiring deliberate translation from Domain Event to Integration Event.

## Verification

- Event catalog listing every Integration Event's owning module, schema,
  version, and consumers.
- Contract tests on published event schemas.
- Idempotency tests on event consumers (Constitution Section 34).

## Revisit Triggers

- A specific interaction proves to genuinely require strong/immediate
  consistency across modules that eventual consistency cannot satisfy —
  handled as a scoped exception (Constitution Section 44) or a
  synchronous-API design for that one interaction, not a reversal of this
  ADR.
- Event throughput/ordering needs grow beyond what a documented delivery
  guarantee can satisfy, prompting a dedicated event-infrastructure design
  in the SAD (no specific broker is chosen by this ADR).
