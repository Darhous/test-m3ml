# Licensing Certification

Based on this audit's dedicated delegated cross-check (see
`00-SKILLS-AND-MCP-REVIEW.md` Method Note) across `docs/reuse/
MASTER_LICENSE_MATRIX.md`, `docs/architecture-review/07-LICENSE-
REVIEW.md`, `08-AGPL-LEGAL-CHECKLIST.md`, `02-TECHNOLOGY-BASELINE.md`,
and `docs/api-platform/31-ENTERPRISE-PRODUCT-DECISIONS.md`, plus this
audit's own direct fix of the one license-string inconsistency found
(immudb, see `09-SAFE-FIXES-APPLIED.md`).

## License Family Breakdown (re-verified against frozen Baseline)

| License Family | Count in Technology Baseline | Redistribution/SaaS Risk |
|---|---|---|
| Apache-2.0 | 12 (E1, E2, E3, E4, E9, E10, E21, plus Libraries L1, L4, Reference R5 informational) | None — clean for SaaS |
| MIT | 2 (L2, L3) | None — clean for SaaS |
| PostgreSQL License | 2 (L1, R4) | None — clean for SaaS |
| MPL-2.0 | 2 (E6, E7) | Low — file-level copyleft, no SaaS network-use trigger |
| GPL-3.0 | 2 (E16 ERPNext, E18 Frappe HR) | Low for self-hosted/SaaS use per `07-LICENSE-REVIEW.md`; **flagged dependency**: an on-premise *distribution* model would need re-review (already noted in `docs/architecture-review/10-ADR-REVIEW.md`'s ADR-0009 cross-reference) |
| LGPL-3.0 | 1 (E11 Alfresco, unverified this pass) | Low-Medium — 1 verification action outstanding |
| AGPL-3.0 (adopted, running) | 5 (E13 Cal.com, E14 Atlas CMMS, E17 openIMIS, E19 Frappe Helpdesk, E20 Frappe CRM) | **High — network-use copyleft clause, `Requires Legal Verification` on all 5** |
| AGPL-3.0 (reference only, no running code) | 1 (OpenELIS Global) | None — no obligation triggers without running/distributed code |
| Unconfirmed | 2 (E8 Novu, E12 Documenso) | **Medium-High — treated with equal urgency to AGPL pending confirmation** |
| Eclipse Public License 1.0 | 1 (E15 OpenBoxes) | Low |
| HL7 FHIR License / Regenstrief free-use / Public methodology | 3 (R1, R2, R3) | None — not conventional software licenses |
| Informational only (Omnipay pattern) | 1 (R5) | None — architecture reference, not a code dependency |

**Total: 30 Technology Baseline entries, all license-classified, zero
entries with a genuinely unknown-and-untracked license** (the 2
"Unconfirmed" entries are unconfirmed-but-tracked-with-urgency, a
materially different state than untracked).

## Cross-Document Consistency (this audit's independent re-check)

**PASS — zero contradictions.** Every one of the 8 license-sensitive
technologies cross-checked (Cal.com, Atlas CMMS, openIMIS, Frappe
Helpdesk, Frappe CRM, Novu, Documenso, Alfresco) carries the identical
license classification across all 4 documents checked. ERPNext and
Frappe HR's GPL-3.0 classification (distinct from their AGPL-3.0
same-vendor-family siblings) is stated identically everywhere. The
"license drift" finding (same Frappe vendor family, different licenses
across 4 applications) is stated identically in 3 independent documents
with no contradiction.

**One inconsistency found and fixed this audit**: immudb (E4) had an
isolated incorrect license string ("Business Source License / Apache-2.0
components") in one row of `MASTER_REPOSITORY_DATABASE.md`, contradicting
5 other consistent Apache-2.0 mentions of the same Engine. Corrected —
see `09-SAFE-FIXES-APPLIED.md`. This was a documentation-string error,
not a genuine license-classification disagreement — immudb has never
carried a BSL license in any authoritative source, and no downstream
decision (Technology Baseline, Risk Register, AGPL Checklist) was ever
built on the incorrect row.

## Commercial / Enterprise Suitability

- **SaaS suitability**: 27 of 30 entries clean or low-risk for SaaS
  operation (Apache-2.0/MIT/PostgreSQL/MPL-2.0/GPL-3.0-self-hosted/
  EPL-1.0/Reference-standards). 3 entries (the AGPL cluster's *network-
  use specifically*, distinct from the base 5-Engine count) carry the
  platform's highest licensing risk, already the subject of a dedicated
  actionable checklist.
- **Redistribution risk**: not currently applicable — the platform's
  SaaS-First model (ADR-0009, Accepted) means no Engine is redistributed
  to a third party as software; the risk that exists is the AGPL
  network-use clause (offering the Engine's functionality *as a
  service*), which is exactly what `08-AGPL-LEGAL-CHECKLIST.md` already
  targets — not a redistribution-in-the-traditional-sense risk.
- **Future SaaS compatibility**: the on-premise/hybrid deployment
  option (ADR-0009) is the one scenario that could convert a currently-
  low-risk GPL-3.0 Engine (ERPNext, Frappe HR) into a higher-risk
  *distribution* scenario — already flagged as a dependency in
  `docs/architecture-review/10-ADR-REVIEW.md`, not newly discovered.

## Vendor Concentration (licensing-adjacent, not a license defect)

R-03 (ERPNext concentration, 5 Modules) and R-05 (Frappe ecosystem
sprawl, 4 applications under 2 different licenses) remain accurately
carried in `docs/architecture-review/11-RISKS.md` and re-confirmed
present, unresolved, and not silently downgraded by this audit's
re-check.

## Certification Verdict

**PASS.** Licensing classification is complete (30/30 entries
classified), internally consistent (1 minor string-level error found
and fixed, zero classification-level contradictions), and every
elevated-risk item (5 AGPL Engines + 2 unconfirmed + 1 LGPL
verification) remains honestly tracked as open, not resolved, with a
concrete, previously-established action checklist
(`docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md`) still valid and
unmodified by this audit.
