# 0006: Independent Device Gateway

## Status

Accepted

## Context

Medical Device Integration is included from the first architecture version
(user-provided decision), and must support a range of protocols/technologies
over time: HL7, HL7 v2, FHIR, ASTM, TCP/IP, Serial Communication, File-Based
Integration, and Vendor APIs. Device communication is inherently different
from the platform's core business logic: it is protocol-heavy,
vendor-specific, and prone to malformed/partial data. Placing this directly
inside the Laboratory (or any other business) module's Core would couple
business rules to device/protocol specifics and risk core data corruption
from device-side failures.

## Decision

Device integration is handled by an **independent Device Integration
Gateway** (one of the Independent Components, Constitution Section 11),
using Vendor Adapters and Protocol Adapters that sit outside the business
Core, translating device data into Integration Events consumed by the
relevant business modules (e.g., Laboratory) through an Anti-Corruption
Layer. Every imported result retains source and provenance. A device/adapter
failure must not corrupt core business data — failures are isolated, logged,
and surfaced for review.

## Alternatives Considered

- **Device adapters embedded inside the Laboratory module.** Rejected:
  couples business/domain logic to protocol/vendor specifics, makes adding
  a new device type a change to core business code, and risks a malformed
  device payload directly corrupting verified business state.
- **One generic, unstructured "integration" module for all external
  systems (devices, AI providers, partners) with no dedicated gateway.**
  Rejected: device integration has distinct protocol/reliability/provenance
  needs (Constitution Section 24) that warrant a dedicated, named component
  rather than being folded into a generic catch-all.
- **Independent Device Integration Gateway with Vendor/Protocol Adapters
  and an Anti-Corruption Layer to the business Core.** **Chosen.** Isolates
  protocol/vendor churn and failure modes away from business logic while
  still integrating cleanly via Integration Events (ADR 0004).

## Positive Consequences

- New device vendors/protocols are added at the Gateway without touching
  business module logic.
- Core business data is protected from malformed/partial device payloads
  by construction (isolation + Anti-Corruption Layer), not just by
  discipline.
- Every imported result's provenance is preserved for traceability and
  dispute resolution.

## Negative Consequences

- Adds an operationally independent component to run/monitor from v1,
  rather than deferring device integration entirely.
- Requires an Anti-Corruption Layer to be designed and maintained for each
  vendor/protocol, which is extra work compared to naive direct parsing
  inside the business module.

## Risks

- **Business logic creeping into an adapter** (e.g., an adapter that
  "helpfully" interprets a result instead of just translating format).
  Mitigated by Constitution Section 24's explicit prohibition and
  Anti-Corruption Layer review.
- **Silent data loss on adapter failure.** Mitigated by the requirement
  that failures be isolated, logged, and surfaced (not silently dropped) —
  verified via fault-injection tests (Constitution Section 24).

## Verification

- Anti-Corruption Layer review at the Device Gateway boundary.
- Fault-injection tests simulating malformed/partial device payloads,
  asserting core data integrity is preserved.
- Provenance-field presence check on every imported result.

## Revisit Triggers

- A specific protocol/vendor integration proves the generic Gateway
  abstraction insufficient, prompting a scoped design refinement (not a
  reversal of the Gateway's independence).
- Device integration volume/criticality grows enough to justify splitting
  the Gateway further (e.g., per-protocol sub-components) — a Selective
  Service Extraction decision under ADR 0001's process, not this ADR's.
