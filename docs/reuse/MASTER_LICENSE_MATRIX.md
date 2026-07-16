# Master License Matrix

Every candidate's license, obligations, and healthcare/commercial-SaaS
compatibility. Detail lives in each Feature's `04-license-review.md`.

**Compatibility legend:** `Clear` = permissive/weak-copyleft, no
obligation conflict with a closed-source or commercial SaaS offering.
`Conditional` = obligations exist (e.g., AGPL network-use clause,
attribution) that must be architecturally respected (isolation, separate
service boundary). `Blocked` = license terms conflict with the intended
commercial model as currently understood.

| Repository | License | SPDX ID | SaaS/AGPL Network Clause? | Compatibility | Note |
|---|---|---|---|---|---|
| Keycloak | Apache License 2.0 | `Apache-2.0` | No | Clear | |
| Open Policy Agent | Apache License 2.0 | `Apache-2.0` | No | Clear | |
| Zitadel | AGPL 3.0 (core, since 2025) | `AGPL-3.0` | **Yes** | Conditional | Commercial license available to remove obligation; not selected as primary for this reason among others |
| Authentik | MIT (core) + Enterprise commercial tier | `MIT` (core) | No (core) | Clear (core) / Conditional (Enterprise features) | Must track feature-by-feature if any Enterprise-tier capability is used |
| Ory (Kratos + Hydra) | Apache License 2.0 | `Apache-2.0` | No | Clear | |
| Casbin | Apache License 2.0 | `Apache-2.0` | No | Clear | |
| PostgreSQL | PostgreSQL License | `PostgreSQL` | No | Clear | Permissive, MIT/BSD-like |
| Citus | AGPL 3.0 (community edition) | `AGPL-3.0` | Yes | Conditional | Not selected — no measured sharding need |
| Unleash (OSS edition) | Apache License 2.0 | `Apache-2.0` | No | Clear | Enterprise-tier features under separate commercial license |
| Flagsmith | BSD 3-Clause | `BSD-3-Clause` | No | Clear | Not selected as primary (avoided as second flag engine) |
| OpenFeature | Apache License 2.0 | `Apache-2.0` | No | Clear | |
| immudb | Apache License 2.0 | `Apache-2.0` | No | Clear | |
| Trillian | Apache License 2.0 | `Apache-2.0` | No | Clear | Not selected |
| CISO Assistant | AGPL 3.0 | `AGPL-3.0` | Yes | Conditional | `Requires Legal Verification`; low-risk if used unmodified/internal-only |
| Eramba Community | GPL 3.0 (unverified this pass) | `GPL-3.0` (tentative) | No | Conditional | License string not independently re-confirmed — flagged |
| GovReady-Q | GPL 3.0 (unverified this pass) | `GPL-3.0` (tentative) | No | Conditional | Same caveat; not selected |
