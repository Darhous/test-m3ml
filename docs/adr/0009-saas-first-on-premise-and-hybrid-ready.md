# 0009: SaaS First, On-Premise Ready, and Hybrid Ready

## Status

Accepted

## Context

The platform must serve a range of tenants, from those comfortable with a
fully managed cloud service to large/regulated organizations that may
require on-premise or hybrid deployment for regulatory, data-residency, or
contractual reasons (`open-questions.md` #2, #3 remain open on the specifics
of local legal requirements and hosting model detail, but the decision to
support multiple deployment models is being made now as a v1 architectural
commitment). Cloud provider replaceability and configurable data residency
are also required.

## Decision

The platform is **SaaS First**, **On-Premise Ready**, and **Hybrid Ready**.
The primary delivery model is SaaS, but the architecture must not preclude
on-premise or hybrid deployment for tenants that need it. The cloud
provider must remain replaceable where practical, and data residency must
be configurable by market. This decision governs deployment-model
*readiness* at the architecture level; it does not select a specific cloud
provider, on-premise packaging technology, or hosting vendor.

## Alternatives Considered

- **SaaS-only, no on-premise/hybrid path.** Rejected: would block
  large/regulated tenants that may require on-premise or hybrid deployment,
  which the user has explicitly required readiness for.
- **On-premise-first design.** Rejected: conflicts with SaaS being the
  primary/default delivery model and would slow down the common-case
  tenant onboarding path.
- **Cloud-provider-locked architecture (deep, non-portable use of one
  provider's proprietary services).** Rejected: conflicts with the explicit
  "cloud provider must remain replaceable where practical" requirement.
- **SaaS First, On-Premise Ready, Hybrid Ready, replaceable cloud provider,
  configurable data residency.** **Chosen.** Matches the explicit,
  user-approved decision set exactly.

## Positive Consequences

- The common case (SaaS) is optimized for without closing the door on
  tenants needing on-premise/hybrid deployment.
- Avoiding deep cloud-provider lock-in preserves negotiating leverage and
  resilience to provider-specific outages/pricing changes.
- Configurable data residency supports future market expansion where data
  residency law varies.

## Negative Consequences

- "Replaceable where practical" and multi-deployment-model support add
  architectural discipline overhead (e.g., avoiding proprietary-service
  lock-in even where it would be the fastest path) compared to a
  single-cloud, SaaS-only design.
- On-Premise/Hybrid readiness must be validated even before the first
  concrete on-premise tenant exists, which is speculative effort ahead of
  measured need — bounded by "do not over-engineer prematurely"
  (Constitution Section, Scalability) applying here too: readiness is
  architectural (no precluding decisions), not a fully built on-premise
  installer in v1.

## Risks

- **Silent SaaS-only coupling** creeping in as convenient shortcuts are
  taken (e.g., a hard dependency on a SaaS-only managed service with no
  on-premise equivalent) that quietly forecloses On-Premise Ready.
  Mitigated by architecture review checking new infrastructure dependencies
  against replaceability/on-premise-readiness before adoption (SAD-level
  process, flagged here for that future review).
- **Data residency configurability being an afterthought.** Mitigated by
  treating it as a v1 requirement (this ADR), not a later feature.

## Verification

- Architecture review checklist item (applied at SAD time): no new
  infrastructure dependency is adopted without confirming it does not
  foreclose On-Premise/Hybrid readiness or hard cloud-provider lock-in,
  without an explicit documented exception.
- Data residency configuration point identified in the SAD before go-live
  in any new market.

## Revisit Triggers

- Answers to `open-questions.md` #2/#3 (legal requirements, hosting model
  detail) may add specific constraints per market but do not reverse this
  decision.
- A measured, specific tenant requirement that a "replaceable where
  practical" design cannot satisfy — handled as a scoped exception
  (Constitution Section 44), not a reversal of this ADR.
