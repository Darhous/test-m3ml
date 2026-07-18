# Monetization

## Foundation — Reused, Not Reinvented

**Fact**, carried forward from both Part 1 and the EARB phase: SaaS
Commercial Operations' entitlement model — **Kill Bill (Technology
Baseline E21, Apache-2.0) + OPA (E2)** — is already frozen and was
already identified in `docs/architecture-review/
13-READINESS-FOR-API-STRATEGY.md` as "directly usable as the
API-tier-gating mechanism." This document does not select a billing
engine (already done, EARB phase) — it defines how the *API layer*
uses that already-ratified engine to express commercial API access.

## Commercial API Strategy

**Recommendation.** An API Product's commercial terms are expressed as
an OPA policy input (entitlement) backed by a Kill Bill subscription —
the same two-engine composition already used for the platform's
general SaaS subscription model, applied specifically to API access
tiers rather than introducing a separate, parallel commercial engine
for APIs. This directly satisfies `01-API-VISION.md`'s "Vendor Neutral"
and "Enterprise Grade" principles by reusing proven infrastructure
instead of adding a new dependency for a narrower purpose.

## Plans

**Recommendation**, structure only — no specific price points are
invented here (No-Guessing Rule; no `.claude/context/` artifact or user
input fixes pricing). A Plan bundles: one or more API Products
(`24-MARKETPLACE.md`), a Rate Limiting tier
(`13-RATE-LIMITING.md`'s Tenant/Partner quota structure), and an SLA
tier (`28-SLA.md`). Plans are versioned independently of the API
contracts they grant access to — changing a Plan's price or quota does
not require a new API major version, and vice versa; this deliberate
decoupling means `07-VERSIONING.md`'s Breaking Change Policy and this
document's commercial changes never force each other's hand.

## Subscriptions

A Tenant's or Partner's subscription to a Plan is a Kill Bill
subscription object; its current state (active, past-due, canceled) is
the input OPA's entitlement policy reads at the Edge Gateway's coarse
authorization step (`09-AUTHORIZATION.md`, `10-API-GATEWAY.md`) — a
lapsed subscription results in a `403` at the Gateway, before the
request reaches a Module, using the exact same PEP mechanism already
specified for Role/Policy-based authorization, not a separate billing-
specific enforcement path.

## API Products (Commercial Framing)

Complements `24-MARKETPLACE.md`'s architectural definition: from the
Monetization document's perspective, an API Product is the unit Kill
Bill actually bills against. A single Module's contract can appear in
multiple API Products at different tiers (e.g., a "Basic" Product
exposing read-only Diagnostic Ordering status lookups vs. a "Premium"
Product also exposing order-submission) — the underlying contract does
not change per tier; only the OPA-enforced entitlement scope does.

## Partner Monetization

Where the counterparty is a Partner rather than a subscribing Tenant
(`21-INTEGRATIONS.md`), the same Kill Bill + OPA composition applies,
with the subscription attached to the Partner's own account rather
than a Tenant. Revenue-sharing or reseller arrangements
(`24-MARKETPLACE.md`'s reseller/channel-partner Future candidate) are
explicitly not designed here — that requires a specific commercial
model decision this Board has no evidence for, consistent with the
No-Guessing Rule, and is left for the business/product function to
define before any architecture work proceeds on it.

## Explicit Boundary With Billing

`26-BILLING.md` covers the *operational* side (usage metering, API
keys, quota consumption tracking) that feeds the entitlement decisions
described here. This document covers the *commercial structure*
(Plans, Products, Subscriptions); `26` covers the *metering pipeline*
that measures against it. Together they complete the Kill Bill + OPA
composition's two halves — commercial definition and consumption
measurement — without duplicating either.
