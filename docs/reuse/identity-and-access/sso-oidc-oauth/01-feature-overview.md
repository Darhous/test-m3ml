# Feature: SSO / OIDC / OAuth

**Module:** Identity and Access (Platform Kernel)
**Source (Discovery):** Wave 3 Capability "Security"; Wave 8
Assumption #19 (Insurance/Payer integration pattern, ACL + Conformist) —
external payer/partner SSO is a related but distinct integration surface.

## What This Feature Covers

Single Sign-On across the platform's own Portals/Dashboards (per
`CLAUDE.md`'s "unified login... routing to the right Portal/Dashboard"),
federation with external Identity Providers a customer organization may
already run (hospital/corporate-provider SSO, per the 9 Confirmed
customer types), and acting as an OIDC/OAuth2 Provider for the platform's
own partner/API clients (the 9th customer type).

## Relationship to `authentication`

Same candidate pool and same Engine decision as the `authentication`
Feature (see `../authentication/`) — this is the textbook Cross-Feature
Dependency case the program's instructions describe (one repository
solving multiple Features). This Feature's files focus on what is
*specific* to SSO/OIDC/OAuth rather than re-deriving the shared research.
