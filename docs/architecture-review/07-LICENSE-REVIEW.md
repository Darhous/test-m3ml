# License Review — By License Family

Source: `MASTER_LICENSE_MATRIX.md` (80 rows, adopted and evaluated-
and-rejected candidates combined). This review re-organizes that data
by license family for Board sign-off and separates **Adopted**
(in the Technology Baseline) from **Evaluated, Not Selected** (informational only, no ongoing obligation).

## Apache License 2.0 — Clear, No Legal Action Required

**Adopted:** Keycloak, OPA, Unleash, immudb, RabbitMQ (MPL-2.0 actually
— see MPL section), Portkey Gateway, Apache Superset, ZXing, Kill Bill,
OpenPolicyAgent (dup), pgvector (PostgreSQL License, not Apache — see
below).

Correction — precise Apache-2.0 adopted list: **Keycloak, OPA, Unleash,
Portkey Gateway, Apache Superset, ZXing, Kill Bill, immudb.** No
network-use clause, no copyleft obligation conflicting with a closed-
source or commercial SaaS offering. **No legal action required.**

## MIT License — Clear, No Legal Action Required

**Adopted:** Prophet, FullCalendar (core), Omnipay (Reference only, not
a dependency). **No legal action required.**

## PostgreSQL License (Permissive, MIT/BSD-like) — Clear

**Adopted:** PostgreSQL RLS pattern (Reference), pgvector. **No legal
action required.**

## Eclipse Public License 1.0 — Clear

**Adopted:** OpenBoxes. Weak, file-level copyleft only — no network-use
trigger. **No legal action required.** This Board notes EPL-1.0 as the
single cleanest license of any whole-system Engine adoption in the
Baseline.

## GPL-3.0 — Clear for Self-Hosted Deployment, Distribution-Triggered

**Adopted:** ERPNext, Frappe HR, SENAITE (Reference source only, not
adopted wholesale).

**Legal consideration:** GPL-3.0's copyleft obligation triggers on
**distribution** of the software (or a derivative), not on network use.
Since the platform's deployment model is self-hosted/SaaS (running the
software, not distributing modified copies to third parties), this
Board confirms the reuse program's own finding: **Clear for the
platform's expected use, conditional only if the platform ever
distributes a modified ERPNext/Frappe HR build externally** (e.g., as a
downloadable on-premise installer with platform-specific patches). This
scenario is not currently planned per ADR-0009 (SaaS-first,
on-premise-and-hybrid-ready) but should be re-checked if an on-premise
distribution model is finalized in the SAD.

## GPL-2.0 — Reference Source Only, Not Adopted as a Dependency

**SENAITE** (GPL-2.0) is used only as a Reference source for its
Westgard-rules QC-module *design*, never as adopted code or a running
Engine (`laboratory-execution/worklist-management/10-final-decision.md`
explicitly rejected wholesale adoption). **No GPL-2.0 obligation
applies** — no SENAITE code is incorporated.

## LGPL-3.0 — Clear, Weaker Copyleft, One Unverified License String

**Adopted:** Alfresco Community Edition (unverified this pass — flagged
in `08-AGPL-LEGAL-CHECKLIST.md` despite not being AGPL, because the
license string itself was never independently re-confirmed, only
carried forward from general knowledge).

**Evaluated, not selected:** Odoo Inventory (Community).

LGPL's copyleft is library-level (modifications to the LGPL-licensed
component itself must be shared; the platform's own code linking
against it does not inherit the obligation). **Likely Clear**, pending
the one verification action in `08-AGPL-LEGAL-CHECKLIST.md`.

## MPL 2.0 — Clear, File-Level Copyleft

**Adopted:** RabbitMQ (unconditional), Mirth Connect 4.5.2 (conditional
— see the separate frozen-release finding in `03-ENGINE-BASELINE.md`
and `11-RISKS.md` R-02, which is a maintainability issue, not a license
issue).

**Legal consideration:** MPL-2.0 requires only that modifications to
MPL-licensed *files* be shared, not the platform's own surrounding code.
**Clear** for both adopted MPL-2.0 Engines.

## BSD-3-Clause — Clear (Evaluated Only, Not Adopted)

Flagsmith, Weaviate — both evaluated and not selected. No ongoing
obligation since neither is in the Technology Baseline.

## AGPL-3.0 — Conditional, Legal Review Required Before Production

**Adopted (13 repositories):** Zitadel is NOT adopted (evaluated only)
— the actual adopted AGPL-3.0 list is: **Cal.com, Atlas CMMS, openIMIS,
Frappe Helpdesk, Frappe CRM, OpenELIS Global (Reference source only, not
a running dependency — see note below), Metabase (NOT adopted, evaluated
only), Nextcloud (NOT adopted), OpenSign (NOT adopted, fallback only),
CISO Assistant (NOT adopted, fallback only), Lago (NOT adopted, fallback
only), Citus (NOT adopted).**

**Precise adopted-and-running AGPL-3.0 list: Cal.com, Atlas CMMS,
openIMIS, Frappe Helpdesk, Frappe CRM.** (OpenELIS Global is AGPL-3.0
but is Reference-only — no OpenELIS code runs in the platform, so its
AGPL terms do not apply to the platform's own deployment; it is
retained in this review for completeness since it appears in the
license matrix.)

**This license family receives dedicated, mandatory legal treatment —
see `08-AGPL-LEGAL-CHECKLIST.md`.**

## Unconfirmed / Requires Independent Verification (Not a Specific License Family)

Two adopted Engines (**Novu**, **Documenso**) never had their license
independently confirmed by the reuse program — logged honestly as
"unconfirmed this pass" rather than guessed. This is a **documentation
gap, distinct from a known-AGPL risk**, but carries the same practical
consequence: no legal sign-off is possible until the actual license text
is read. Treated with equal urgency to the AGPL items in
`08-AGPL-LEGAL-CHECKLIST.md`.

## Board Summary

| License Family | Adopted Count | Legal Status |
|---|---|---|
| Apache-2.0 | 8 | Clear |
| MIT | 3 | Clear |
| PostgreSQL License | 2 | Clear |
| EPL-1.0 | 1 | Clear |
| GPL-3.0 | 2 | Clear for self-hosted; re-check if distribution model changes |
| GPL-2.0 | 0 (Reference only) | Not applicable — no code adopted |
| LGPL-3.0 | 1 | Likely Clear, 1 verification action pending |
| MPL-2.0 | 2 | Clear (1 carries a separate frozen-release maintainability flag) |
| AGPL-3.0 | 5 | **Conditional — mandatory legal review, see `08-AGPL-LEGAL-CHECKLIST.md`** |
| Unconfirmed | 2 | **Mandatory verification, see `08-AGPL-LEGAL-CHECKLIST.md`** |

**Total license issues requiring action before production: 8**
(5 AGPL-3.0 repositories + 2 unconfirmed-license repositories + 1
LGPL-3.0 string-verification action).
