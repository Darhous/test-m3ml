# Authentication

## Identity Architecture

**Fact.** Keycloak (Technology Baseline E1, Apache-2.0, ADR-0008
Accepted) is the platform's single Identity Provider (OIDC). ADR-0008
("Unified Login and Policy-Based Access") requires a single login
surface routing every user to the correct Portal/Dashboard — Keycloak
is the ratified engine implementing that requirement, and this
document does not re-select or re-evaluate it.

Every human, service, and machine identity on the platform is issued
through this single Identity Provider — there is no second, parallel
authentication system for any Module, including AGPL-licensed or
externally-sourced Engines (ERPNext, Frappe HR, openIMIS, Cal.com,
etc.), which are all reached through this platform's own
Anti-Corruption Layer, never authenticated to directly by an end user.

## OAuth2

**Recommendation**, standard OAuth2 grant selection by client type,
consistent with Zero Trust (this phase's assigned Architectural
Principle):

| Client Type | Grant | Rationale |
|---|---|---|
| Interactive (Portal/Dashboard web, mobile) | Authorization Code + PKCE | No client secret can be safely embedded in a browser or mobile app |
| Service identity (Module-to-Module, Independent Component) | Client Credentials | No human user is present; the service itself is the subject |
| Partner (business-relationship machine-to-machine) | Client Credentials, scoped to the specific Partner contract | Mirrors service identity pattern but with narrower, contract-specific scope |

## OIDC

**Recommendation.** ID Tokens carry authentication proof; the
`UserInfo` endpoint (Keycloak-provided) carries profile claims. Access
Tokens (below) carry authorization-relevant claims (Tenant,
Organization, Branch, Role) — kept separate from the ID Token per
standard OIDC practice, so authorization data changes do not force
re-authentication.

## JWT

**Recommendation.** Access tokens are JWT-encoded and short-lived. The
exact TTL is **not asserted as a specific number** by this Board — no
`.claude/context/` file or user instruction fixes one, and inventing a
number (e.g., "15 minutes") would violate the No-Guessing Rule. The
qualitative requirement is: short enough that a leaked token has a
bounded blast radius, refreshed transparently via the refresh-token
flow below. The exact figure is left for API Governance/SAD
ratification.

Claims minimally include: subject (user or service identity), Tenant
ID, Organization ID, Branch ID (where applicable), Role(s), and token
expiry — the claims that Layer 2 (`02-API-FIRST-ARCHITECTURE.md`)
needs to resolve routing without an extra round-trip to Identity and
Access for every request.

## Refresh Tokens

**Recommendation.** Rotating refresh tokens (each use issues a new
refresh token and invalidates the previous one), revocable through
Keycloak's own session management — this is standard Keycloak
capability, not a new build. A revoked session invalidates all
outstanding refresh tokens for that session immediately, which is the
mechanism Break-Glass Access's "time-limited" requirement
(`.claude/context/glossary.md` Accepted Definition) can rely on.

## Human Identities

Patients, practitioners, and staff are each Keycloak-managed
identities. Their mapping into Tenant/Organization/Branch structure
follows ADR-0005's Hybrid Tenant Isolation model — the exact
realm-per-Tenant vs. shared-realm-with-tenant-claim implementation
choice is tied to Open Question #15 (shared-tier partitioning
technology), which remains open; this document does not resolve it, it
only records the dependency explicitly rather than assuming an answer.

## Service Identities

Every Module and every Independent Component (Device Integration
Gateway, Notification Service, AI Operations Gateway, Analytics,
Document Management, Public API Gateway, Background Workers — the
Accepted Independent Component list, Constitution Section 11) has its
own dedicated Client-Credentials-based service identity. A service
identity never shares credentials with a human identity, and never
authenticates as a human's session on that human's behalf without an
explicit, audited delegation mechanism — this is the Zero Trust
principle applied concretely to service-to-service calls, not just
human-to-API calls.

## Machine Identities

Devices (lab instruments, analyzers) are **not** directly
Keycloak-authenticated end users. They are mediated entirely through
the Device Integration Gateway's own Anti-Corruption Layer
(ADR-0006, Accepted) — the Gateway holds whatever device-facing
credential/protocol scheme is appropriate (HL7/ASTM-level, via Mirth
Connect/Apache Camel), and only the Gateway's own service identity
(above) ever calls into the rest of the platform. This is a deliberate
boundary, not an oversight: it keeps device-credential diversity fully
contained behind one Anti-Corruption Layer rather than teaching every
Module how to authenticate a device.

## SSO

**Fact.** Unified Login across all Portals/Dashboards is an explicit
project requirement (CLAUDE.md project description) and an Accepted
ADR-0008 decision. A single Keycloak-issued session authenticates a
user across every Portal they are authorized to route to — there is no
per-Portal login. The specific realm/tenant-partitioning mechanics that
implement this at the Keycloak configuration level remain tied to Open
Question #15, as noted above under Human Identities.
