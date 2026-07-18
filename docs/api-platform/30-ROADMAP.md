# Roadmap

## Basis for Sequencing

**No calendar dates or durations are asserted** — this platform has no
staffing, budget, or scheduling input in `.claude/context/` or from the
user that would let this Board fix dates without guessing. Sequencing
below is derived purely from **dependency structure already established
in this document set** — what genuinely cannot start before what — not
from an estimate of effort or a target date.

## Platform Evolution — Horizons

### Near-Term (Foundational — blocks everything after it)

- `16-CONTRACT-FIRST.md` through `18-ASYNCAPI-EVENTS.md`: the
  Contract-First discipline and OpenAPI/AsyncAPI standards must be in
  force before any generated artifact (SDKs, Interactive Docs, the
  Catalog) has anything real to generate from.
- `23-API-CATALOG.md`: every downstream document (Portal, Marketplace,
  Billing's client registry) reads from the Catalog — it must exist
  first.
- Resolution of the three Build-vs-Buy gaps this document set has
  surfaced and left honestly open (`10`, `12`, and the items in
  `31-ENTERPRISE-PRODUCT-DECISIONS.md`) — a Gateway and Secrets Engine
  are load-bearing infrastructure every subsequent capability sits on.

### Mid-Term (Developer Enablement — depends on Near-Term)

- `22-DEVELOPER-PORTAL.md` and `20-SDK-STRATEGY.md`: both require the
  Catalog and Published contracts to already exist in volume.
- `21-INTEGRATIONS.md`'s Partner Certification becoming operational for
  the 6 identified Partner API candidates — contingent on each
  candidate Module actually designing its specific Partner contract
  (explicitly not done by this document set, which only inventoried
  the candidates).
- `19-WEBHOOKS.md`'s Dispatcher becoming a real, deployed Independent
  Component.
- `27-OBSERVABILITY.md`'s metrics/logging/tracing pipeline reaching
  production maturity — required before `28-SLA.md` can respond to
  real numbers.

### Long-Term (Commercial Ecosystem — depends on Mid-Term)

- `24-MARKETPLACE.md` and `25-MONETIZATION.md`/`26-BILLING.md`'s full
  commercial loop — requires a track record of Certified Partner
  integrations (Mid-Term) before a Marketplace has anything credible
  to list.
- Any eventual Public API type (`03-API-DOMAIN-INVENTORY.md`'s
  currently-unpopulated column) — contingent on a business Decision
  this Board does not make, not an engineering sequencing question.
- `28-SLA.md`'s numeric commitments — only knowable once
  `27-OBSERVABILITY.md` has produced real operating data and Open
  Question #4 (expected usage volume) is answered.

## What This Roadmap Deliberately Does Not Contain

- Specific target quarters, sprint counts, or team-sizing estimates —
  none of this Board's inputs supports asserting them.
- A commitment that Long-Term items *will* happen — Marketplace,
  Monetization, and Public API access all remain contingent on
  business Decisions (per each document's own "not designed here"
  notes) this architecture phase does not have the authority to make.
- Any reopening of Discovery/Build-vs-Buy sequencing — this Roadmap
  sequences *this document set's own* dependency graph only, not the
  underlying Module build order, which remains the Software
  Architecture Document's responsibility (explicitly out of scope —
  see Exit Conditions).

## Relationship to Part 1's Readiness Findings

`docs/architecture-review/13-READINESS-FOR-API-STRATEGY.md` flagged two
items blocking *finalization* of specific contracts: R-06 (FHIR version
unpinned) and the AGPL legal review outcome. Both remain open
dependencies for the Near-Term horizon above wherever a specific
contract touches a FHIR-shaped resource (Patient Management, Result
Verification and Reporting) or an AGPL-backed Engine
(`21-INTEGRATIONS.md`'s Certification checklist already encodes this).
This Roadmap does not resolve either — it inherits them as still-open,
exactly as Part 1 left them.
