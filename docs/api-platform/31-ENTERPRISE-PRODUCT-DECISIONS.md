# Enterprise Product Decisions

## Method

For each of the 7 categories this phase's Task assigns, this Board
asked: does this project's own evidence base (`docs/reuse/`,
`docs/architecture-review/`, this document set) plus well-established,
low-controversy general engineering knowledge support naming **one**
preferred solution without performing a fresh Build-vs-Buy research
pass (explicitly out of scope — see Exit Conditions)? Where the answer
required weighing license terms, security posture, self-hosting
constraints (ADR-0009), or localization support (ADR-0010) that this
Board cannot verify without guessing, the category is left **OPEN**,
per this phase's explicit instruction not to guess. This produced 3
Recommendations and 4 Open categories — a genuine, not reflexive,
split.

## 1. API Gateway — **OPEN at Part 2 authoring — Superseded 2026-07-18**

**Superseded**: Open Question #28 is resolved — **Kong Gateway is the
approved Version 1 API Gateway product selection**
(`docs/certification/20-OPEN-QUESTIONS-RESOLUTION.md`,
`25-PRE-SAD-CLEAN-CLOSURE.md`), now a Technology Baseline entry. The
original "OPEN, insufficient evidence" finding below is preserved as
the historical record of this document's own authoring — it is not
rewritten, only superseded.

**Insufficient evidence.** As already established in
`10-API-GATEWAY.md`, no Gateway product (Kong, Tyk, Envoy, KrakenD,
Apigee, cloud-native equivalents) has been evaluated against this
project's own 10-point Engine checklist (license, self-hosting per
ADR-0009, security posture, maintainability). This is a genuine
multi-vendor space with materially different licenses (Kong's OSS core
vs. Enterprise edition; Envoy's Apache-2.0/CNCF-Graduated status is
notably closer to this platform's demonstrated Apache-2.0 preference
pattern — E1 Keycloak, E2 OPA, E4 immudb, E9 Portkey, E10 Superset,
E21 Kill Bill are all Apache-2.0 — but this observation is a pattern,
not a Build-vs-Buy result, and naming Envoy on pattern-matching alone
would be exactly the guess this instruction forbids). **Recorded as
Open Question #28** (Part 1).

## 2. Secrets/Vault Engine — **OPEN at Part 2 authoring — Superseded 2026-07-18**

**Superseded**: Open Question #29 is resolved — **OpenBao is the
approved Version 1 Secrets Management product selection**
(`docs/certification/20-OPEN-QUESTIONS-RESOLUTION.md`,
`25-PRE-SAD-CLEAN-CLOSURE.md`), now a Technology Baseline entry,
directly consistent with this section's own original observation below
naming OpenBao "a credible open alternative." The original finding is
preserved as historical record, not rewritten.

**Insufficient evidence**, and one specific piece of general knowledge
this Board surfaces as directly relevant rather than silently omits:
HashiCorp Vault — the most widely recognized product in this
category — changed its license from MPL-2.0 to the Business Source
License (BUSL) 1.1 in 2023, a licensing-posture shift materially
similar in kind (though not identical in mechanism) to the AGPL
network-use concerns this project has already applied significant
scrutiny to (`docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md`).
OpenBao (the Linux Foundation's MPL-2.0 fork of pre-BUSL Vault) is a
credible open alternative, but this Board has not run it through this
project's own license/maturity/community-health checklist and will not
name it as "the" recommendation on that basis alone. **Recorded as Open
Question #29** (Part 1).

## 3. Developer Portal — **OPEN**

**Insufficient evidence.** Candidate approaches span a wide spectrum
(a fully custom-built Portal vs. an open-source platform like
Backstage vs. a Gateway-vendor-bundled portal). This decision is
further entangled with Question #1 (API Gateway) above — several
commercial Gateway products bundle a Developer Portal, meaning this
category may not even be independently decidable before the Gateway
question resolves. Additionally, ADR-0010's Arabic/RTL requirement is
a genuine, unverified evaluation criterion here (does a candidate
Portal product render RTL correctly?) this Board cannot confirm without
guessing. **New Open Question #30** (added below).

## 4. API Documentation Platform — **RECOMMENDATION, CONDITIONAL**

**Sufficient evidence for a conditional recommendation.** This is a
lower-risk, lower-lock-in category than the three above: a
documentation renderer consumes the OpenAPI document
(`17-OPENAPI-GOVERNANCE.md`) as its only input and produces no
persistent state or vendor-specific data — switching renderers later
carries near-zero migration cost, unlike a Gateway or Secrets Engine.
**This Board recommends Redoc** (MIT license — consistent with this
project's demonstrated preference for permissive licenses, single
static-site output, no backend dependency, purpose-built for OpenAPI
3.x rendering, matching `17`'s mandated notation exactly) as the
default renderer for `22-DEVELOPER-PORTAL.md`'s Interactive Docs.

**Explicit condition, mirroring the precedent already set for ZXing
(Technology Baseline L4, "APPROVED — general-knowledge basis... re-
confirm specific library and license at implementation time")**: this
Board has **not verified** Redoc's Arabic/RTL rendering quality against
ADR-0010's Accepted localization requirement, and does not assert it
without evidence. This recommendation is conditional on that
verification passing at implementation time; if it fails, Swagger UI
(Apache-2.0, the credible fallback in this same low-lock-in category)
is the documented alternative to re-evaluate, not a full fresh search.

## 5. API Analytics — **OPEN**

**Insufficient evidence to decide whether a dedicated tool is needed at
all**, not just which one. `27-OBSERVABILITY.md` already recommends
reusing the already-ratified Apache Superset (E10) for API dashboards.
Whether Superset's general-purpose BI capability is *sufficient* for
API-specific analytics (per-consumer breakdowns, anomaly detection,
API-product-level reporting a specialized tool like Moesif or a
Gateway-bundled analytics module might offer more natively) is a
question this Board cannot answer without real production API traffic
data that does not yet exist — the same dependency `28-SLA.md` already
names for numeric SLA targets. **New Open Question #31** (added
below).

## 6. Contract Testing Platform — **RECOMMENDATION**

**Sufficient evidence.** Pact (Pact Foundation, MIT license) is the
dominant, purpose-built implementation of the Consumer-Driven Contract
pattern this Board already specified architecturally in
`16-CONTRACT-FIRST.md` — there is no comparably mature, license-clean
alternative built specifically for that pattern (as opposed to generic
API-testing tools that were not designed for the consumer/provider
verification loop `16` describes). This Board recommends **Pact** with
a self-hosted Pact Broker (consistent with ADR-0009's on-premise/
hybrid-ready requirement — the Broker is itself a lightweight,
self-hostable component, not a mandatory SaaS dependency). Risk: Low —
this is a development-time/CI-time tool, not a runtime production
dependency, so its blast radius if reconsidered later is small.

## 7. SDK Generation Platform — **RECOMMENDATION**

**Sufficient evidence.** OpenAPI Generator (Apache-2.0, the actively-
maintained community fork of the earlier Swagger Codegen project) is
the dominant, license-clean, multi-language open-source generator built
directly for OpenAPI 3.x input — matching `17-OPENAPI-GOVERNANCE.md`'s
mandated notation exactly, with no comparably mature, permissively-
licensed alternative offering equivalent language breadth. This Board
recommends **OpenAPI Generator** for `20-SDK-STRATEGY.md`'s generation
pipeline. Risk: Low — same reasoning as Contract Testing: a build-time
tool, easily reconsidered later without touching any already-shipped
API contract.

## Summary

| Category | Outcome | Confidence |
|---|---|---|
| API Gateway | OPEN at authoring, **Superseded 2026-07-18 — Kong Gateway approved** | — (historical) |
| Secrets/Vault | OPEN at authoring, **Superseded 2026-07-18 — OpenBao approved** | — (historical) |
| Developer Portal | OPEN (#30, new) | — |
| API Documentation Platform | Redoc, **conditional** on RTL verification | Medium |
| API Analytics | OPEN (#31, new) — question is need, not just product | — |
| Contract Testing Platform | **Pact** | High |
| SDK Generation Platform | **OpenAPI Generator** | High |

**3 of 7 categories closed with a named recommendation; 4 left
honestly open.** No category was guessed to force a tidier outcome.
