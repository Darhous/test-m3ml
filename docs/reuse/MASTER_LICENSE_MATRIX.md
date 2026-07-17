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
| Mirth Connect 4.5.2 | MPL 2.0 | `MPL-2.0` | No | Clear, but **frozen** — no free patches past this version | 4.6+ requires a NextGen commercial license |
| Apache Camel | Apache License 2.0 | `Apache-2.0` | No | Clear | |
| RabbitMQ | MPL 2.0 | `MPL-2.0` | No | Clear | |
| Apache Kafka | Apache License 2.0 | `Apache-2.0` | No | Clear | Not selected (scale mismatch) |
| NATS + JetStream | Apache License 2.0 | `Apache-2.0` | No | Clear | Not selected |
| Novu | Permissive-leaning (unverified this pass) | TBC | Unknown | `Requires Legal Verification` | Same honesty caveat as Eramba/GovReady-Q |
| Portkey Gateway | Apache License 2.0 (since March 2026) | `Apache-2.0` | No | Clear | Recent full-OSS status, worth a quick re-check at implementation time |
| LiteLLM | MIT | `MIT` | No | Clear | Not selected (close alternative) |
| Langfuse | MIT (core) | `MIT` | No | Clear | Some Enterprise features gated |
| pgvector | PostgreSQL License | `PostgreSQL` | No | Clear | |
| Qdrant | Apache License 2.0 | `Apache-2.0` | No | Clear | Not selected (no measured scale trigger) |
| Weaviate | BSD 3-Clause | `BSD-3-Clause` | No | Clear | Not selected |
| Apache Superset | Apache License 2.0 | `Apache-2.0` | No | Clear | ASF-governed |
| Metabase (Community) | AGPL 3.0 | `AGPL-3.0` | Yes | Conditional | Not selected; white-label also paywalled regardless |
| Lightdash | MIT | `MIT` | No | Clear | Not selected |
| Prophet | MIT | `MIT` | No | Clear | |
| Alfresco Community | LGPL v3 (unverified this pass) | `LGPL-3.0` (tentative) | No (LGPL) | Likely Clear, `Requires Legal Verification` | |
| Nextcloud Hub | AGPL 3.0 | `AGPL-3.0` | Yes | Conditional | Not selected |
| Documenso | Unconfirmed this pass | TBC | Unknown | `Requires Legal Verification` | |
| OpenSign | AGPL 3.0 | `AGPL-3.0` | Yes | Conditional | Credible free fallback |
| Cal.com | AGPL 3.0 (core) | `AGPL-3.0` | Yes | Conditional | `Requires Legal Verification`; commercial license available |
| Cal.diy | MIT | `MIT` | No | Clear | Credible fallback, feature parity unconfirmed |
| FullCalendar | MIT (core) | `MIT` | No | Clear | Premium plugins separately licensed |
| HL7 FHIR `Specimen` resource | HL7 FHIR License | `HL7-FHIR` (specification license, not code copyleft) | No | Clear | Same license class as other FHIR resources already logged |
| ZXing | Apache License 2.0 | `Apache-2.0` | No | Clear | General-knowledge basis, `Requires Legal Verification`-style re-confirmation before implementation |
| SENAITE | GPL 2.0 | `GPL-2.0-only` | Yes (distribution-triggered) | Clear | Not selected wholesale — Reference source only |
| OpenELIS Global | AGPL 3.0 | `AGPL-3.0-only` | Yes (network-use-triggered) | Conditional, `Requires Legal Verification` | Not selected wholesale — Reference source only; would be a materially larger question if ever adopted as a whole-system Engine |
| Atlas CMMS | AGPL 3.0 (dual, commercial available) | `AGPL-3.0-only` | Yes (network-use-triggered) | Conditional, `Requires Legal Verification` | Selected as whole-system Engine (Asset and Maintenance); commercial license is a documented escape hatch |
| openMAINT | AGPL | `AGPL-3.0-only` | Yes (network-use-triggered) | Conditional, `Requires Legal Verification` | Not selected — credible fallback only |
| OpenBoxes | Eclipse Public License 1.0 | `EPL-1.0` | Weak — file-level, not network-use | Clear | Selected as whole-system Engine; cleanest license of any Engine adoption in the program |
| Odoo Inventory (Community) | LGPL 3.0 | `LGPL-3.0-only` | Weak — library-level | Clear | Not selected — credible fallback only |
| ERPNext | GPL 3.0 | `GPL-3.0-only` | Strong — distribution-triggered | Clear (self-hosted) | Selected as whole-system Engine (Procurement); clear for self-hosted use |
| OpenProcurement | Apache License 2.0 | `Apache-2.0` | No | Clear | Not selected — government-tender scale mismatch |
| Omnipay | MIT | `MIT` | No | Clear | Architecture Reference only, not a code dependency |
| Nafezly/payments | MIT | `MIT` | No | Clear | Not selected — confidence, not license |
| openIMIS | AGPL 3.0 | `AGPL-3.0-only` | Yes (network-use-triggered) | Conditional, `Requires Legal Verification` | Selected as whole-system Engine (module-level adoption) |
| Frappe HR | GPL 3.0 | `GPL-3.0-only` | Yes (distribution-triggered) | Clear for self-hosted use | Same posture as ERPNext |
| Frappe Helpdesk | AGPL 3.0 | `AGPL-3.0-only` | Yes (network-use-triggered) | Conditional, `Requires Legal Verification` | **License-drift finding**: distinct from ERPNext/Frappe HR (GPL-3.0) despite same vendor — not inherited clearance |
| Frappe CRM | AGPL 3.0 | `AGPL-3.0-only` | Yes (network-use-triggered) | Conditional, `Requires Legal Verification` | Same license-drift caveat as Frappe Helpdesk |
| Kill Bill | Apache License 2.0 | `Apache-2.0` | No | Clear | Selected as whole-system Engine; cleanest license of any Engine in the program alongside OpenBoxes |
| Lago | AGPL 3.0 | `AGPL-3.0-only` | Yes (network-use-triggered) | Conditional, `Requires Legal Verification` | Not selected — credible modern fallback |

**Program complete.** `Requires Legal Verification` recurs for: Novu,
Cal.com, Zitadel (not selected), OpenELIS Global (Reference only),
Alfresco, Documenso, OpenSign (not selected), Atlas CMMS, openMAINT (not
selected), OpenBoxes uses the cleaner EPL-1.0, ERPNext/Frappe HR use
GPL-3.0 (clear for self-hosted), Frappe Helpdesk/CRM, openIMIS, Lago —
this list should be the starting point for the SAD's formal legal
review pass, not re-derived from scratch.
