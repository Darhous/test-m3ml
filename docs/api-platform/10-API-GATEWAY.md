# API Gateway

## An Explicit, Honest Gap First

**Fact, surfaced directly rather than silently assumed away:** the
Technology Baseline's 21 ratified Engines (`docs/architecture-review/
02-TECHNOLOGY-BASELINE.md`) contain **no dedicated API Gateway
product** — no Kong, Tyk, KrakenD, Envoy, Apigee, or equivalent has
been evaluated or ratified. The "Public API Gateway" named in
Constitution Section 11's Accepted Independent Component list is an
**architectural role**, not yet a **technology decision** — those are
two different things this Board is careful not to conflate.

Selecting a specific Gateway product is a Build-vs-Buy act, and this
phase's Do-Not list explicitly forbids re-evaluating or extending the
Technology Baseline. This document therefore defines the Gateway's
**architectural responsibilities and boundaries only** — what any
eventual Gateway product must do — and records the product-selection
gap as a new item in `.claude/context/open-questions.md` (#28) rather
than guessing a product, consistent with the No-Guessing Rule
(CLAUDE.md Section 3).

## Routing

The Gateway is the single entry point for every External, Partner,
Public, and Admin API call (`03-API-DOMAIN-INVENTORY.md`); Internal
APIs are never Gateway-routable (`02-API-FIRST-ARCHITECTURE.md`'s
boundary rules). It resolves the target Module contract from the
request path's version and resource segment
(`07-VERSIONING.md`, `06-NAMING-CONVENTIONS.md`) and forwards to the
Routing Layer (Layer 2) for Tenant/Organization/Branch resolution.

## Authentication

The Gateway validates the `Authorization` bearer JWT against Keycloak
(`08-AUTHENTICATION.md`) on every request before any routing decision
is made. An invalid or expired token is rejected at the Gateway — it
never reaches a Module.

## Authorization

The Gateway performs the coarse RBAC-level OPA decision
(`09-AUTHORIZATION.md`) before routing. It does **not** perform the
fine-grained ABAC/Data-Scope decision — that remains the owning
Module's responsibility, by design (defense in depth, not gap).

## Caching

**Recommendation.** Response caching is permitted only for endpoints
that are both (a) explicitly marked cacheable by the owning Module and
(b) not Tenant/Data-Scope-sensitive in a way that caching could leak
across callers (e.g., a public test-catalog reference list is a
reasonable caching candidate; any Patient- or TestResult-scoped
response is not). No blanket caching policy is set at the Gateway
level — each Module opts in explicitly.

## Transformation

The Gateway may perform protocol- and version-level transformation
only: legacy-version compatibility shims during a deprecation window
(`07-VERSIONING.md`), request/response compression, and correlation-ID
injection. It performs **no business-logic transformation** — that
would violate the Layer responsibility split in
`02-API-FIRST-ARCHITECTURE.md` and make the Gateway a hidden, ungoverned
extension of Module logic.

## Traffic Control

The Gateway enforces rate limits (`13-RATE-LIMITING.md`) and applies
circuit-breaking toward downstream Modules/Independent Components that
are unavailable or degraded, returning `503` rather than hanging a
caller indefinitely.

## Gateway Responsibilities — Summary

| Responsibility | In Scope for the Gateway | Explicitly Not |
|---|---|---|
| TLS termination | ✓ | — |
| AuthN (token validation) | ✓ | — |
| Coarse AuthZ (RBAC) | ✓ | Fine-grained ABAC/Data-Scope (Module's job) |
| Routing | ✓ | Business-logic dispatch |
| Rate limiting | ✓ | — |
| Protocol/version transformation | ✓ | Business-logic transformation |
| Caching (opt-in per Module) | ✓ | Blanket/default caching |
| Correlation ID assignment | ✓ | Distributed tracing (Part 2, Observability) |
| Sensitive Operation / HITL gating | — | Always the owning Module's Aggregate layer |

## Dependency on Open Question #28

Every item above describes the Gateway's **required behavior**, which
holds regardless of which product eventually fills the role. Selecting
that product is explicitly out of this Board's authority this phase —
see `.claude/context/open-questions.md` #28 and
`00-SKILLS-AND-TOOLS-USED.md`'s tool-limitations note.
