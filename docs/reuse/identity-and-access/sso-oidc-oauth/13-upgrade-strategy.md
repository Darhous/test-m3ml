# Upgrade Strategy — SSO / OIDC / OAuth

Inherits `../authentication/13-upgrade-strategy.md` — same Engine, same
Adapter, same upgrade/exit path. No feature-specific deviation; OIDC/
OAuth2 standard-conformance means the exit path is, if anything, cleaner
for this Feature specifically (any OIDC-certified replacement IdP is a
drop-in at the protocol level, though Admin-API/federation-configuration
migration work would still apply).
