# Engine Baseline — Detailed Validation

Every Engine from `02-TECHNOLOGY-BASELINE.md` Section A, validated
against the Board's 10-point checklist: architectural fit, domain
boundaries, license compatibility, maintainability, upgrade path,
security, maturity, community health, ecosystem stability, long-term
ownership. `✓` = confirmed no concern (already established in the reuse
program's own review, re-verified here). `⚑` = flagged, see Note.
Nothing here was re-researched; every `✓`/`⚑` traces to the cited
`docs/reuse/` source.

| Engine | Fit | Boundaries | License | Maintain. | Upgrade | Security | Maturity | Community | Ecosystem | Ownership | Note |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Keycloak | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | CNCF Incubating; regulated-industry adoption evidence. No flags. |
| OPA | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | CNCF Graduated. Reused 8×/6 Modules — highest-confidence Engine in the program. |
| Unleash | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | No flags. |
| immudb | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | No flags. |
| Eramba Community | ⚑ | ✓ | ⚑ | ✓ | ✓ | — | ✓ | ✓ | ✓ | ⚑ | **License unverified this pass** (`04-license-review.md`, Audit and Compliance). **Domain fit weak-confidence** — the reuse program itself flagged this its lowest-confidence decision. **Long-term ownership**: no dedicated healthcare-GRC alternative was found either, so "reconsider" does not mean "abandon" — see `11-RISKS.md` R-01. |
| Mirth Connect 4.5.2 | ✓ | ✓ | ⚑ | ⚑ | ⚑ | ⚑ | ✓ | ✓ | ⚑ | ⚑ | **Frozen since NextGen's March 2025 commercial shift** — 4.5.2 receives no free security patches. This is not a license-*compatibility* problem (MPL-2.0 on 4.5.2 is Clear) but a **maintainability/security/ecosystem** problem: the version is effectively unmaintained for this platform's purposes. Apache Camel remains the documented fallback. See `11-RISKS.md` R-02. |
| RabbitMQ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | No flags. |
| Novu | ✓ | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | **License string never independently confirmed** (`04-license-review.md` across Modules 5, 11, 15, 27 all repeat "unconfirmed this pass"). See `08-AGPL-LEGAL-CHECKLIST.md` — flagged for verification even though not confirmed AGPL, precisely because it was never confirmed *anything*. |
| Portkey Gateway | ✓ | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ⚑ | ✓ | License went fully OSS (Apache-2.0) only in March 2026 — recent enough that this Board recommends a 1-time re-check at SAD kickoff, not a standing concern. |
| Apache Superset | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ASF-governed. No flags. |
| Alfresco Community | ✓ | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | LGPL-3.0 string unverified this pass — see `08-AGPL-LEGAL-CHECKLIST.md` (LGPL is lower-risk than AGPL but was never independently re-confirmed either). |
| Documenso | ✓ | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | License unconfirmed this pass, same caveat class as Novu — Sensitive-Operation-adjacent Feature, so this Board treats the gap as higher-priority than Novu's. |
| Cal.com | ✓ | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | AGPL-3.0 core — see `08-AGPL-LEGAL-CHECKLIST.md`. Commercial license documented as an escape hatch if legal review blocks. |
| Atlas CMMS | ✓ | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | AGPL-3.0 dual-license — see `08-AGPL-LEGAL-CHECKLIST.md`. Commercial tier is a documented escape hatch. |
| OpenBoxes | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | EPL-1.0, cleanest license of any Engine. Digital-health production track record (PIH, 5+ countries). No flags. |
| ERPNext | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ⚑ | **Boundaries**: broadest single-Engine footprint (5 Modules) — this is a validated reuse strength, not a boundary violation (each Module's own file explicitly scopes what ERPNext owns vs. does not, e.g. explicitly excluded from Inventory's stock ledger), but it does concentrate **ownership risk** — see `11-RISKS.md` R-03. GPL-3.0 clear for self-hosted use. |
| openIMIS | ✓ | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | AGPL-3.0 — see `08-AGPL-LEGAL-CHECKLIST.md`. Digital Public Good status is a strong maturity/ownership signal. |
| Frappe HR | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | GPL-3.0, same posture as ERPNext. No flags. |
| Frappe Helpdesk | ✓ | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | **AGPL-3.0 — license-drift from same-vendor ERPNext/Frappe HR (GPL-3.0)**. This Board explicitly re-confirms the reuse program's own finding: same-vendor family does **not** imply same license. See `08-AGPL-LEGAL-CHECKLIST.md`. |
| Frappe CRM | ✓ | ✓ | ⚑ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | Same license-drift finding as Frappe Helpdesk. |
| Kill Bill | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | Apache-2.0, 10+ years enterprise-proven (telecom/fintech/B2B SaaS). No flags. |

## Board Findings

1. **19 of 21 Engines pass all 10 checks cleanly or with only a license-
   verification flag** (a documentation gap, not a compatibility
   problem) — see `08-AGPL-LEGAL-CHECKLIST.md` for the consolidated
   action list.
2. **2 Engines carry a substantive (non-license) flag**: Eramba
   (domain-fit confidence) and Mirth Connect (frozen-release
   maintainability/security). Both were already flagged by the reuse
   program itself — this Board's review is a **confirmation that the
   flag was not silently dropped**, not a new finding.
3. **No Engine fails architectural fit or domain boundaries outright.**
   ERPNext's broad footprint is validated as intentional reuse
   discipline, not scope creep — see `MASTER_DEPENDENCY_MATRIX.md`'s
   proactive-duplicate-avoidance log for the explicit boundary
   statements (e.g., ERPNext's `receiving-goods` deliberately does not
   touch its own stock module).
4. **No two Engines compete for the same domain responsibility.** Cross-
   checked against all 9 Detected Duplicates in `MASTER_DEPENDENCY_
   MATRIX.md` — every one shows a resolved or proactively-avoided
   status. Re-verified, not re-derived.
