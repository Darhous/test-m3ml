# License Review — Authentication

| Candidate | License | SPDX | Network/SaaS Clause | Compatibility for This Platform |
|---|---|---|---|---|
| Keycloak | Apache License 2.0 | `Apache-2.0` | None | **Clear** — permissive, no obligation conflict with a closed-source or commercial multi-tenant SaaS deployment. |
| Zitadel | AGPL 3.0 (core, since 2025) | `AGPL-3.0` | Yes — network-use clause | **Conditional** — running Zitadel as a networked service normally triggers source-disclosure obligations for modifications; commercial license available from ZITADEL GmbH to remove this. Must be architecturally isolated (used unmodified, as a separate deployed service, not embedded/modified) if adopted under AGPL terms. |
| Authentik | MIT (core) + separate Enterprise license for advanced features | `MIT` core | None on core | **Clear** on core MIT-licensed functionality; **Conditional** if any Enterprise-tier feature is used (separate commercial terms apply — must be tracked feature-by-feature, not assumed). |
| Ory (Kratos + Hydra) | Apache License 2.0 | `Apache-2.0` | None | **Clear** — same profile as Keycloak. |

## Governing Consideration

The platform's Confirmed direction includes White-Label and multi-tenant
SaaS commercial operation (Discovery Wave 1). AGPL's network-use clause
is the single most consequential license fact in this Feature's research
— it does not block Zitadel outright (used-as-a-service, unmodified, is a
common and legally clean AGPL usage pattern), but it removes the option
to fork/modify Zitadel's core without triggering disclosure, unless the
commercial license is purchased. This is `Requires Legal Verification`
before final adoption — not a blocking finding, but not silently waved
through either, consistent with this program's evidence-based licensing
discipline.
