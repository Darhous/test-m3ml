# Final Decision — Authentication

## Decision: **ENGINE + ADAPTER**

**Engine:** Keycloak (Apache-2.0, CNCF Incubating).
**Adapter:** a thin, platform-owned Anti-Corruption Layer inside the
Identity and Access Bounded Context (Wave 9, Context 27), speaking
OIDC/OAuth2 + Admin REST API to Keycloak and exposing the platform's own
Ubiquitous-Language contract outward.

## Why Not the Alternatives

- **Zitadel:** strong architecture, but AGPL 3.0's network-use clause
  introduces a `Requires Legal Verification` licensing complication for a
  White-Label multi-tenant commercial SaaS product (Discovery Wave 1)
  that Keycloak's Apache-2.0 license avoids entirely. Not rejected as a
  product — rejected as the *first* choice given a cleaner-licensed peer
  exists with equal or better enterprise adoption evidence.
- **Authentik:** excellent admin UX, but thinner regulated-industry
  production-adoption evidence than Keycloak, and its open-core model
  means some advanced features fall under a separate commercial license
  that would need to be tracked feature-by-feature.
- **Ory:** most architecturally flexible, but its microservices
  decomposition (separate Kratos/Hydra/etc. services with no unified
  admin console) adds more integration surface than this Feature's scope
  justifies, working against the Modular Monolith direction
  (`CLAUDE.md` Section 7).
- **Build In-House:** rejected — lowest weighted score, primarily driven
  by Security (building credential storage, brute-force protection, and
  session handling correctly from scratch is one of the highest-risk
  places to reinvent mature software), consistent with this program's
  "never rebuild mature software without documented justification" rule.

## Confidence

**High** — this is a Confirmed-pattern decision (mature category, clear
license, verifiable enterprise adoption), not `Inferred`. Still requires
user/Architecture Review Board sign-off before treated as Accepted (this
program does not itself grant architectural authority — see
`13-upgrade-strategy.md` and the program's own Stop Conditions).
