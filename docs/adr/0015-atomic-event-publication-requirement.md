# 0015: Atomic Event Publication Requirement

## Status

Proposed (registered by SAD Wave 10, `docs/sad/10-architecture-decisions-and-traceability.md` §6 — this ADR commits the platform to a *requirement*, not to a specific mechanism; mechanism selection is explicitly deferred, not decided here)

## Context

Every Module that raises an Integration Event first commits its own business-state change, then publishes the corresponding event (ADR-0004, Event-Driven Integration). Wave 5 (Runtime View, Accepted) identified a genuine, unresolved gap in this sequence: no Accepted source states what guarantees the platform makes about the window between the business-state commit and the event actually reaching the broker. If a Module commits its own database write and then crashes, restarts, or otherwise fails before publishing, the resulting event may be silently and permanently lost — with no signal to any downstream consumer that a fact they were entitled to see never arrived.

This gap has been independently flagged by three separate Waves as exceeding their own delegated authority: Wave 5 §9 (original identification, "Mandatory Pre-Implementation Architecture Decision"), Wave 6 §33 (restated, not re-decided), and Wave 7 §32 item 5 (restated, tied to THR-022's broader "eventual consistency of guarantees" concern). Wave 10 (Architecture Decisions & Traceability) is the SAD Wave explicitly assigned to register this gap and determine whether a formal Architecture Decision Record is required.

No Accepted source states which mechanism should close this gap. Four candidate approaches exist in general industry practice and are named (without endorsement) by Wave 5 §9's own text: a Transactional Outbox table, Change Data Capture (CDC) off the Module's own write-ahead log, direct integration between the database transaction and the broker's own transactional publish capability, or a recoverable publication log/retry mechanism external to both. Selecting among these requires an evaluation this project has not yet performed (throughput impact, operational complexity, broker-specific transactional support, failure-mode behavior under each) — inventing a choice here would violate the No-Guessing Rule (CLAUDE.md Rule 3) and this project's own established discipline against a single SAD Wave silently committing the platform to an unresearched technical choice.

## Decision

**The platform is required to guarantee that a committed business-state change eventually results in its corresponding Integration Event becoming publishable — there is no silent, permanent loss of an already-happened fact between business commit and event publication.** Duplicate publication of the same fact is explicitly acceptable under the platform's existing At-Least-Once delivery assumption (Wave 5 §10), provided consuming Modules apply the Constitution's own Idempotency Policy (§48).

**This ADR does not select the mechanism.** The specific approach (Transactional Outbox, CDC, broker-transactional integration, or a recoverable publication log) remains an open implementation-phase decision, to be resolved by a dedicated evaluation before any cross-module event-reacting workflow is implemented against an affected event path. This ADR's own Status remains `Proposed` — not `Accepted` — until that evaluation selects a mechanism and this ADR (or a superseding one) is updated to record it.

## Alternatives Considered

At the level of *whether to make this a formal ADR at all* (the actual decision this document records):

- **Leave the gap as a generically "Open" item inside whichever Wave next touches it, with no dedicated ADR.** Rejected: three separate Waves (5, 6, 7) each independently concluded this exceeds their own delegated authority and is platform-wide; leaving it perpetually "Open" inside a Wave whose own scope doesn't include event-reliability architecture (as Wave 6/7 both explicitly note) risks the requirement itself — not just its mechanism — being lost or diluted over time.
- **Invent a mechanism now, in this ADR, based on general industry convention (e.g., default to Transactional Outbox as the most common pattern).** Rejected: this would be exactly the kind of unresearched, single-Wave technical commitment this project's own No-Guessing Rule and established Wave-governance discipline exist to prevent — no source has evaluated Outbox against the platform's own actual broker (RabbitMQ), Module count, or throughput profile.
- **Register the requirement formally via a `Proposed`-status ADR, without selecting a mechanism.** **Chosen.** This closes the "is a decision required" half honestly (yes) without closing the "which mechanism" half dishonestly (guessing).

## Positive Consequences

- The requirement itself — no silent event loss — is now a durable, citable, platform-wide commitment rather than a recurring "Open" footnote restated by each Wave that touches it.
- Implementation teams have an explicit, unambiguous semantic target to design against, even before the specific mechanism is chosen.
- The mechanism-selection work is correctly scoped as its own dedicated evaluation, not smuggled into an unrelated Wave's own content.

## Negative Consequences

- This ADR alone does not unblock implementation of any cross-module event-reacting workflow that depends on the affected event paths — that remains blocked until the mechanism-selection evaluation completes and this ADR is updated or superseded.
- Carrying a `Proposed`-status ADR forward introduces a known, tracked administrative follow-up (updating this ADR's status) that must not be forgotten.

## Risks

- **The mechanism-selection evaluation is deprioritized indefinitely, leaving this ADR permanently `Proposed`.** Mitigated by recording it as a Mandatory Pre-Implementation Architecture Decision (Wave 5's own classification, preserved) with an explicit blocking point (cross-module event-reacting workflow implementation) and an owning authority (Architecture Review Board).
- **A future Wave or implementation effort selects a mechanism without updating this ADR, creating drift between this document and actual practice.** Mitigated by this ADR's own explicit instruction that mechanism selection must update or supersede it, not bypass it.

## Verification

- No cross-module event-reacting workflow proceeds to implementation on an affected event path until this ADR's status changes from `Proposed`.
- Once a mechanism is selected, a fault-injection test simulating a Module crash between business-commit and event-publish must confirm the event is not permanently lost (eventual delivery, possibly duplicate, per the At-Least-Once/idempotency framing above).

## Revisit Triggers

- Completion of the mechanism-selection evaluation — this ADR is updated in place (Status → `Accepted`, mechanism recorded) or superseded by a new ADR recording the chosen mechanism.
- A specific Module's own event-publication failure incident in production, which would elevate this from an architecture-level gap to an active reliability concern requiring expedited resolution.
