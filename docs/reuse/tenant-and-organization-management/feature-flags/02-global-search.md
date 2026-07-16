# Global Search Log — Feature Flags

## Query Run

`open source feature flag platform Unleash vs Flagsmith vs OpenFeature
2026 enterprise`

## Landscape Notes

Three-tier landscape found: (1) full management platforms — **Unleash**
(12,000+ GitHub stars — noted as context only, not a scoring dimension
per this program's rules; 500+ contributors; weekly releases; adopters
including FINN.no, NAV/Norwegian government, Telenor, Getty Images —
genuine enterprise/regulated-sector adoption evidence) and **Flagsmith**
(combines feature toggles with remote configuration, server-side identity/
trait storage, real-time propagation); (2) the vendor-neutral
specification layer — **OpenFeature** (CNCF), explicitly "not a
management platform... you assemble the rest yourself" — both Unleash and
Flagsmith support OpenFeature providers, meaning adopting either does not
lock the platform out of the vendor-neutral standard; (3) GrowthBook,
Flipt, PostHog feature flags — surfaced as credible alternatives but with
less enterprise-governance depth (change-request approval workflows,
audit logging) than Unleash specifically offers.

## Candidates Carried Forward

Unleash, Flagsmith — the two credible full-platform candidates with
real enterprise-governance features (both matter for a Sensitive-
Operation-adjacent gate like "Elevated Audit tier feature-gating," per
Wave 6's candidate tier).
