# Rate Limiting

All policy structure below is a **Recommendation** — no ADR governs
rate limiting, and the specific numeric thresholds are deliberately
left unfixed rather than invented, per the No-Guessing Rule (CLAUDE.md
Section 3). This document defines the *tiers and mechanism*; the exact
numbers are an implementation-time / SAD-time ratification, informed
by real usage data this Board does not have (Open Question #4, "ما حجم
الاستخدام المتوقع" — expected usage volume — remains open in
`.claude/context/open-questions.md`, and rate limits without usage
data would themselves be a guess).

## Why Rate Limiting Sits at the Gateway

Per `10-API-GATEWAY.md`, traffic control (including rate limiting) is
an explicit Gateway responsibility, enforced before a request reaches
any Module — this both protects every Module uniformly and keeps the
policy centrally auditable rather than reimplemented per Module.

## Tenant Quotas

Every Tenant (Hybrid Tenant Isolation, ADR-0005) has a request-rate
quota, tiered by the Tenant's plan/subscription level as managed by
SaaS Commercial Operations' entitlement model (Kill Bill + OPA,
already frozen and "directly usable as the API-tier-gating mechanism"
per `docs/architecture-review/13-READINESS-FOR-API-STRATEGY.md`'s own
finding — this document reuses that existing composition rather than
inventing a separate quota-storage mechanism). A Tenant on the shared
infrastructure tier and a Tenant on the dedicated-database tier may
reasonably have different default quotas, reflecting their different
isolation posture — but the specific numbers are not fixed here.

## Partner Quotas

Partner API consumers (`03-API-DOMAIN-INVENTORY.md`) receive a quota
scoped to their specific contract, independent of any Tenant's quota —
a Partner integration (e.g., an insurer's claims-submission traffic)
must not be able to consume a Tenant's own quota or vice versa. Partner
quotas are provisioned per-contract at onboarding, not inherited from a
generic default.

## Burst Limits

**Recommendation.** In addition to a sustained-rate quota, each tier
has a short-window burst allowance (a caller may briefly exceed its
sustained rate without being throttled, provided it returns to the
sustained rate) — standard token-bucket-style behavior. Exact bucket
size/refill rate: not fixed here, same reasoning as above.

## Abuse Protection

**Recommendation.** Distinct from ordinary rate limiting: repeated
authentication failures (credential-stuffing pattern), repeated `403`/
`404` responses on enumerable resource paths (scanning pattern), and
requests that bypass the Gateway attempting to reach a Module directly
are all treated as abuse signals, not merely quota events — they
trigger the identity/IP's quota to tighten automatically and generate
an Audit Event for the Audit and Compliance Module (`03`) rather than
simply being throttled silently.

## Rate Limiting Policies — Structure

| Dimension | Applies To | Governed By |
|---|---|---|
| Sustained quota | Tenant, Partner | Entitlement tier (Kill Bill + OPA) or per-contract provisioning |
| Burst allowance | Tenant, Partner | Same tier structure, short window |
| Abuse threshold | Any identity, including Internal | Independent of quota tier — a security control, not a commercial one |
| Response on exceed | All | `429 Too Many Requests` with a `Retry-After` header (`05-API-STANDARDS.md`) |

## Explicit Dependency

This document's structure is usable today; its numeric thresholds
depend on (a) Open Question #4 (expected usage volume, still open) and
(b) the eventual Gateway product selection (Open Question #28) for
mechanical enforcement. Neither dependency blocks defining the policy
shape — only its final numbers.
