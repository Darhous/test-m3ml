# SLA

## No Numbers Invented

Consistent with the No-Guessing Rule applied throughout this document
set (`07-VERSIONING.md`'s deprecation window, `12-SECRETS-AND-KEYS.md`'s
rotation cadence, `13-RATE-LIMITING.md`'s thresholds): this document
defines the **SLA/SLO/SLI structure and tiering mechanism**, not
specific commitment numbers (e.g., "99.9% availability"). No
`.claude/context/` artifact or user instruction fixes an availability,
latency, or support-response target, and this platform has no
production traffic history to derive one from. Inventing a number here
would be exactly the failure mode CLAUDE.md Section 3 exists to
prevent — a fabricated commitment that later gets silently treated as
real.

## SLA, SLO, SLI — Definitions Applied to This Platform

| Term | Meaning Here |
|---|---|
| **SLI** (Indicator) | A measured value from `27-OBSERVABILITY.md`'s metrics pipeline — e.g., "Edge Gateway p99 latency," "successful-response rate per Module." |
| **SLO** (Objective) | An internal target for an SLI, used to drive engineering priority — e.g., "Result Verification and Reporting's `ResultReleased` path should stay under target latency X," with X left unfixed here. |
| **SLA** (Agreement) | An externally-committed subset of SLOs, attached to a Plan (`25-MONETIZATION.md`) as a contractual tier, with consequences (credits, escalation) if missed. |

## Availability

**Recommendation (structure only).** Availability is measured per API
type (`03-API-DOMAIN-INVENTORY.md`), not platform-wide as a single
number — an Admin API's availability target need not match a Partner
API's, since their consequence-of-downtime profiles differ (an internal
Admin outage inconveniences staff; a Partner API outage breaches an
external commercial commitment). Sensitive-Operation-adjacent paths
(`ResultVerified`/`ResultReleased`) are tracked separately from
CRUD-shaped endpoints, since their criticality is clinical, not merely
commercial.

## Latency

**Recommendation (structure only).** Latency SLIs are measured at the
Edge Gateway (end-to-end, what the caller actually experiences) and
independently at each Module boundary (isolates whether a slowdown is
Gateway-side or Module-side) — mirroring the two-PEP defense-in-depth
pattern already used for authorization (`09-AUTHORIZATION.md`), applied
here to performance measurement instead.

## Reliability

**Recommendation.** Reliability commitments for any API exposing an
Engine already flagged with a standing risk in
`docs/architecture-review/11-RISKS.md` (Mirth Connect's frozen-release
status, R-02; Eramba's low-confidence rating, R-01) explicitly carry
that risk forward into the SLA tier for the affected API Product — a
Partner-facing SLA built on top of a Conditionally Approved Engine
cannot honestly promise a reliability figure this platform's own Risk
Register has already flagged as uncertain. This is not a new risk
finding; it is this document refusing to let an SLA silently paper
over a risk Part 1/EARB already surfaced.

## Support

**Recommendation (structure only).** Support tiers (response-time
commitment by severity) are attached to a Plan the same way Rate
Limiting and Availability tiers are (`25-MONETIZATION.md`) — support
severity classification reuses the platform's own Sensitive Operation
distinction (an incident affecting `ResultVerified`/`ResultReleased`
is inherently higher severity than an Admin-API cosmetic issue), rather
than inventing a separate severity taxonomy.

## Dependency on Real Usage Data

Every numeric SLA target in a future revision of this document depends
on production telemetry this platform does not yet have
(`27-OBSERVABILITY.md`'s pipeline, once live) and on the same expected-
usage-volume Open Question (#4, still open) already noted as blocking
precise Rate Limiting numbers in `13-RATE-LIMITING.md`. This document's
structure is usable today; its numbers are not yet knowable honestly.
