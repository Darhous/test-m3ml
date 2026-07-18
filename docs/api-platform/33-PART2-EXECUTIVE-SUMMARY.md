# API Platform & Developer Ecosystem Strategy — Part 2 Executive Summary

**Authority:** Enterprise API Architecture Board. **Scope:** completes
the Enterprise Developer Platform and Commercial API Ecosystem on top
of Part 1's API Foundation, the frozen Technology Baseline, and every
Accepted ADR — none of which is re-derived, contradicted, or
re-evaluated here.

## Executive Summary

Part 2 adds Contract-First tooling discipline (OpenAPI/AsyncAPI),
webhook delivery, an outbound SDK strategy, Partner integration
architecture, a Developer Portal, a live API Catalog, a Marketplace,
and the full commercial loop (Monetization → Billing → Observability →
SLA), plus a platform-level release-lifecycle and roadmap framing —
18 documents in total, all grounded in Part 1's five-layer API
architecture and the already-ratified Kill Bill + OPA entitlement
composition. A dedicated product-decision pass evaluated 7 tooling
categories: 3 received a named recommendation (Pact, OpenAPI
Generator, and a conditional Redoc), 4 were left honestly open because
this project's own evidence base does not support naming one solution
without guessing.

## Architecture Decisions

- **Contract-First is now tooling-concrete**: OpenAPI 3.1.x (REST) and
  AsyncAPI 3.x (events) are the mandatory contract notations, with
  Consumer-Driven Contract testing recommended for Internal (Module-
  to-Module) traffic and provider-side testing for Partner traffic.
- **Webhooks deliver at-least-once**, signed, SSRF-protected, and
  idempotency-keyed by the underlying event's own `eventId` — no
  exactly-once guarantee is claimed, honestly.
- **SDKs are generated, never hand-written**, from the same Published
  OpenAPI documents the Developer Portal and Catalog already read from
  — one source of truth across documentation, SDKs, and contract
  testing.
- **Monetization and Billing reuse, rather than replace, the already-
  ratified Kill Bill + OPA composition** — no new commercial engine
  is introduced; the Edge Gateway is where entitlement, rate limiting,
  and usage metering all converge.
- **A new architectural role — the Webhook Dispatcher and the
  Developer Portal — are introduced as Independent-Component-pattern
  roles**, consistent with the existing Constitution Section 11 model,
  without pre-selecting their implementing product.

## Developer Platform Summary

The Developer Portal (`22`) reads from a generated, always-current API
Catalog (`23`) — never a hand-maintained document — and provides
Interactive Docs, a Sandbox using synthetic-data-only Tenants (never
real Patient/clinical/financial data, per CLAUDE.md Section 13),
self-service credential and webhook-subscription management, and a
Partner-Certification-gated onboarding flow (`21`). SDK generation
(`20`) and Contract Testing (`16`) both build on the same Published
contracts, keeping documentation, generated clients, and verified
compatibility mechanically in sync rather than independently
maintained.

## Commercial Platform Summary

The Marketplace (`24`) is a further-filtered, commercially-packaged
view over the Catalog, listing only Published, Certified API Products.
Monetization (`25`) defines Plans/Products/Subscriptions on the
existing Kill Bill + OPA engine; Billing (`26`) defines the metering
pipeline (emitted at the Gateway, not per-Module) that feeds it, plus
API Key and OAuth Client Management built on the existing Keycloak
identity layer. No pricing figures, quota numbers, or SLA percentages
are asserted anywhere in this set — every numeric commitment is
explicitly deferred pending real usage data this platform does not yet
have (Open Question #4, still open).

## Open Questions

- **Carried from Part 1, unchanged:** #28 (API Gateway product), #29
  (Secrets/Vault Engine).
- **New this phase:** #30 (Developer Portal product — entangled with
  #28), #31 (whether a dedicated API Analytics tool is needed beyond
  the already-ratified Apache Superset).
- **Not closed, and explicitly not attempted:** whether the platform
  will ever open general Public/self-service API access
  (`24-MARKETPLACE.md`) — a business Decision, not an architecture
  question this Board can or should answer.
- **Every numeric target deferred, not guessed:** deprecation-window
  duration (`07`, carried into `29`), secret-rotation cadence (`12`),
  rate-limit thresholds (`13`), and every SLA/SLO number (`28`) — all
  explicitly left for ratification once real usage/production data
  exists, consistent with the No-Guessing Rule applied throughout both
  Part 1 and Part 2.

## Risks

| Risk | Description | Carried From |
|---|---|---|
| Gateway/Secrets/Portal selection remains open | Three load-bearing infrastructure decisions (#28, #29, #30) block finalizing several Near-Term Roadmap items until resolved | New this phase, though #28/#29 originate in Part 1 |
| SLA commitments cannot yet be made honestly | No production telemetry exists to set real numbers; premature commercial commitments would outrun the evidence | New this phase (`28-SLA.md`) |
| AGPL/FHIR blockers still apply to specific Partner contracts | Insurance and Corporate Contracts' openIMIS-backed claims API, and any FHIR-shaped Partner/External API, remain gated by `docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md` and R-06 respectively | Reaffirmed, not new — inherited from Part 1/EARB |
| Marketplace/Public API access is contingent on an unmade business Decision | This architecture does not presuppose the platform will monetize a public developer ecosystem — building toward it without that Decision would be premature investment | New this phase (`24`, `30`) |
| Vault-style license risk (HashiCorp BUSL) | A specific, named risk this Board surfaced proactively rather than defaulting to the most recognizable product name | New this phase (`31`) |

## Recommendations

1. Resolve Open Questions #28–#31 through a scoped, dedicated
   Build-vs-Buy micro-assessment (not a full program re-run) before
   the Mid-Term Roadmap horizon begins in earnest.
2. Adopt Pact and OpenAPI Generator as recommended (`31`) — both are
   low-risk, build-time-only tools with minimal switching cost if
   reconsidered later.
3. Verify Redoc's RTL/Arabic rendering before finalizing it as the
   Developer Portal's documentation renderer; fall back to Swagger UI
   if it fails.
4. Do not commit to specific SLA numbers, rate-limit thresholds, or
   deprecation-window durations until `27-OBSERVABILITY.md`'s pipeline
   has produced real data and Open Question #4 is answered.
5. Treat this document set, like the Technology Baseline before it, as
   frozen input for the eventual Software Architecture Document — not
   as a substitute for it.

## Commit Hash

Recorded in the final commit message below, per this phase's Output
requirement.
