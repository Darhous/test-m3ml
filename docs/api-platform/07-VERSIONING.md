# Versioning

## Versioning Strategy

**Recommendation.** URL-path major versioning (`/v1/test-orders`, not
header- or query-parameter-based) is the recommended default, chosen
over the other two strategies the `api-design-principles` Skill
documents (header versioning, query-parameter versioning) for three
reasons specific to this platform:

1. **Partner/Integration legibility.** `03-API-DOMAIN-INVENTORY.md`
   identifies multiple Partner and Integration API surfaces (insurer
   claims submission, referring-clinic APIs) where the consuming
   party is an external organization, not just this platform's own
   Portals. A version visible in the URL is unambiguous to an external
   integrator without needing to inspect headers.
2. **Cache and Gateway simplicity.** The Edge Gateway
   (`10-API-GATEWAY.md`) can route and cache purely on path, without
   parsing headers for version-dependent behavior.
3. **Consistency with the platform's own ratified Engines.** Every
   Engine in the Technology Baseline that exposes a REST API (Keycloak,
   ERPNext, OPA, Kill Bill) uses path- or otherwise URL-visible
   versioning, not header versioning — matching the pattern already
   implicitly present across the platform's own dependencies avoids
   introducing a second convention with no driver.

This is a Recommendation for API Governance to ratify, not a Decision
this Board finalizes unilaterally — no ADR currently governs API
versioning strategy specifically.

## Compatibility Policy

- **Non-breaking (additive) changes do not bump the major version.**
  New optional fields, new endpoints, new optional query parameters.
- **Breaking changes require a new major version**, per the definition
  in `04-API-GOVERNANCE.md`'s Breaking Change Policy.
- A Module may run `/v1` and `/v2` of its own contract concurrently;
  versioning is per-Module-contract, not a single platform-wide version
  number — this follows directly from ADR-0001's Modular Monolith
  boundary (a version bump in Billing's contract does not force a
  version bump in Patient Management's).

## Deprecation Policy

- A version entering **Deprecated** status (`04-API-GOVERNANCE.md`
  lifecycle) must be announced with (a) the retirement date, (b) the
  replacement version, and (c) a migration note, before any consumer
  is required to move.
- **The exact minimum deprecation-window duration is not decided by
  this Board.** Per the No-Guessing Rule (CLAUDE.md Section 3), this
  Board does not invent a specific number of days/months not stated
  anywhere in `.claude/context/` or by the user. This is recorded as a
  new item for API Governance to ratify, not silently assumed — see
  `.claude/context/open-questions.md` addition below, and treat any
  number appearing in future planning as Proposed until ratified.
- Until that number is ratified, the operating default is: **no
  version may be Retired while it has any known active Partner
  consumer**, which is a qualitative floor, not a quantitative one.

## Support Windows

Tied to the same unresolved duration above. What is decided: a
Deprecated version continues to receive security patches (never
feature changes) until Retirement; a Retired version returns `410
Gone`. What is not yet decided: how long that window lasts, and
whether it differs by API type (e.g., a shorter window for Internal
APIs consumed only by the platform's own Modules under this Board's
control, versus a longer, contractually-committed window for Partner
APIs consumed by an external organization this Board does not control
the release cadence of).

## Migration Rules

- A breaking change ships with a written migration note describing
  every field/endpoint/behavior difference between the old and new
  version.
- Dual-version support is mandatory during the deprecation window (no
  "big bang" cutover for any API type other than Internal, where the
  owning Module controls both producer and consumer).
- Partner-tier consumers (business-relationship APIs,
  `03-API-DOMAIN-INVENTORY.md`) receive advance notice ahead of
  Internal/External consumers, reflecting that this Board does not
  control a Partner's release cadence the way it controls the
  platform's own Portal release cadence.
- A version bump on an API that exposes an AGPL/unconfirmed-license
  Engine (`docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md`) does
  not itself require a new legal review — but a version bump that
  changes *what data is exposed* through that API does, since the
  legal review's scope is about the exposure, not the version number.
