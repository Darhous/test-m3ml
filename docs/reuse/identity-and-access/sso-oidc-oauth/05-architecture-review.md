# Architecture Review — SSO / OIDC / OAuth

Builds on `../authentication/05-architecture-review.md`. Feature-specific
note: Keycloak's Identity Brokering maps external-IdP claims to local
Keycloak users via configurable Mappers — directly usable for a
hospital-chain customer that wants its staff to log in with their
existing corporate IdP while the platform still enforces its own
Role/Organization model on top. This composes cleanly with the
Organizations multi-tenancy primitive already selected in the
`authentication` Feature — one Keycloak instance, tenant-scoped
Organizations, per-Organization optional Identity Brokering. No
architectural conflict found between this Feature's requirement and the
Engine already selected.
