# Integrations

**Scope note:** `03-API-DOMAIN-INVENTORY.md` (Part 1) identified 6
Partner API *candidates* across the Core Domain and Business/
Commercial Modules, explicitly marked "not designed." This document
designs the **architecture** those candidates share — not the specific
business terms of any one Partner relationship, which remains a
per-Partner commercial/legal matter outside this Board's authority.

## Partner APIs — The 6 Identified Candidates

| Module | Partner API Candidate |
|---|---|
| Practitioner and Clinic Management | Referring-clinic directory |
| Scheduling and Encounters | Home-collection-logistics booking (**blocked** on Open Question #6, unchanged from Part 1) |
| Diagnostic Ordering | Referring-physician order submission |
| Result Verification and Reporting | Referring-clinic result delivery |
| Procurement | Supplier-facing PO/RFQ |
| Supplier Management | Supplier self-service portal |
| Insurance and Corporate Contracts | Insurer/corporate-client claims submission (already partially real — openIMIS-backed) |
| SaaS Commercial Operations | Reseller/channel-partner (Future, Part-2-adjacent — see `24-MARKETPLACE.md`) |

## External APIs

External APIs (`03`'s definition: authenticated platform end users
through Portals) are already architecturally complete per Part 1 — this
document does not add new External API design, only clarifies how an
External API differs from a Partner API at the integration-certification
level below.

## Integration Contracts

Every Partner relationship, regardless of which Module owns it, uses
the same integration-contract shape — reusing `16-CONTRACT-FIRST.md`'s
OpenAPI/AsyncAPI discipline plus three Partner-specific additions:

1. **Scope declaration** — exactly which endpoints/event types
   (`18-ASYNCAPI-EVENTS.md`) and which Tenant/Organization the Partner
   integration is limited to, enforced at the Edge Gateway
   (`10-API-GATEWAY.md`'s coarse AuthZ) and re-checked at the Module
   boundary (`09-AUTHORIZATION.md`'s fine AuthZ) exactly like any other
   caller — a Partner is not a trusted network position, consistent
   with Zero Trust.
2. **Rate/quota tier** — provisioned per the Partner Quota mechanism
   already specified in `13-RATE-LIMITING.md`, not a new mechanism.
3. **Webhook subscription, where applicable** — a Partner that needs
   asynchronous notification (e.g., a referring clinic wanting result
   delivery) uses `19-WEBHOOKS.md`'s subscription model, not a
   bespoke polling contract per Partner.

## Compatibility

A Partner integration's compatibility guarantee follows
`07-VERSIONING.md`'s Deprecation Policy, with the same qualification
already flagged there: Partner-tier consumers receive advance notice
ahead of Internal/External consumers, and the exact minimum support
window remains an open ratification item (`07`), not invented here.

## Certification

**Recommendation.** Before a Partner integration is allowed to move
from Draft to Published (`04-API-GOVERNANCE.md`'s lifecycle, applied
here), it passes a Partner Certification checklist:

| Check | Verifies |
|---|---|
| Contract conformance | The Partner's actual traffic matches the Published OpenAPI/AsyncAPI contract, not an informally-agreed shape |
| Webhook signature verification (if applicable) | The Partner correctly validates `19-WEBHOOKS.md`'s signing before going live |
| Idempotency handling (if applicable) | The Partner correctly treats repeated `eventId`/`Idempotency-Key` deliveries as duplicates |
| Data-Scope boundary test | A test call confirms the Partner's credentials cannot reach data outside their declared scope (`14-MULTI-TENANCY.md`) |
| License/legal posture clear, where the integration exposes an AGPL-backed Engine's data (e.g., Insurance and Corporate Contracts' openIMIS-backed claims API) | `docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md` clearance, per `04-API-GOVERNANCE.md`'s Approval Workflow requirement, restated here because Partner APIs are exactly where this matters most |

Certification is a one-time gate before go-live, re-run whenever the
Partner's integration scope changes (a new endpoint/event type added
to their subscription) — not a recurring audit this document
specifies a cadence for (no number invented, consistent with the
No-Guessing Rule).

## Explicit Non-Design

This document does not design the commercial terms, SLAs
(`28-SLA.md` covers the general SLA framework, not per-Partner
contracts), or the Marketplace publishing flow (`24-MARKETPLACE.md`)
for any Partner relationship — those are separate concerns this
document hands off to, not absorbs.
