# Global Search Log — Session Management

No new search round — session/token lifecycle is core OIDC/OAuth2
functionality already covered by `../authentication/
02-global-search.md`'s candidate set. The one Feature-specific item
already surfaced in `../authentication/06-security-review.md` is directly
relevant here: **CVE-2026-1035 (refresh token reuse via TOCTOU race
condition, fixed in Keycloak 26.5.6)** — a session-management-class
vulnerability, cross-referenced rather than re-researched.
