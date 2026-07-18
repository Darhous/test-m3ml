# Unified Enterprise Risk Register

Consolidates `docs/architecture-review/11-RISKS.md`'s R-01 through R-08,
`docs/api-platform/33-PART2-EXECUTIVE-SUMMARY.md`'s Part 2 risks, and
this audit's own security/governance findings into one register. No
risk is newly invented here beyond what prior phases already
identified — this is a consolidation and status re-verification, not a
new risk-discovery exercise (beyond the 3 documentation defects logged
as resolved in `09-SAFE-FIXES-APPLIED.md`, which were risks in the
sense of certification-audit findings, not enterprise architecture
risks, and are excluded from this register accordingly).

| ID | Title | Description | Likelihood | Impact | Severity | Mitigation | Owner | Status | Related Documents |
|---|---|---|---|---|---|---|---|---|---|
| R-01 | Eramba Community low-confidence GRC decision | Compliance-tracking Engine selected with the program's lowest-confidence rating; no stronger alternative found across 28 Modules | Medium | Medium | Medium | Reconsider at SAD time with a focused re-search (permitted exception to no-market-scan rule) | Audit and Compliance | Open | `docs/architecture-review/11-RISKS.md`, `03-ENGINE-BASELINE.md` |
| R-02 | Mirth Connect frozen-release risk | Last free release (4.5.2); no free security patches going forward | High | High | **High** | Apache Camel documented as evaluated fallback; budget migration path in SAD | Device Integration Gateway | Open | `docs/architecture-review/11-RISKS.md` |
| R-03 | ERPNext concentration risk | Single Engine spans 5 Modules (Procurement, Supplier Mgmt, Billing, Payments/Treasury, Accounting) | Low | High | Medium | Document as Tier-1-criticality dependency with exit-strategy review (see R-08) | Cross-cutting (Procurement) | Open | `docs/architecture-review/11-RISKS.md` |
| R-04 | AGPL-3.0 legal exposure (5 running Engines) | Cal.com, Atlas CMMS, openIMIS, Frappe Helpdesk, Frappe CRM — network-use clause unreviewed | Medium | High | **High** | Formal legal review, early SAD-phase workstream (top recommendation, unchanged) | Enterprise legal/compliance | Open | `docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md`, `docs/api-platform/21` |
| R-05 | Frappe ecosystem license drift and operational sprawl | 4 Frappe-family apps, 2 different licenses, 4 independent upgrade cadences | Medium | Medium | Medium | Treat as 4 independently-versioned deployments, not one platform unit | Workforce Mgmt, CRM and Support, Procurement | Open | `docs/architecture-review/11-RISKS.md` |
| R-06 | FHIR resource version not pinned | No FHIR version (R4/R4B/R5) explicitly stated across 7 Modules referencing FHIR resources | Low | Medium | Medium | **Resolved 2026-07-18: FHIR R4 pinned (D-43)** | Cross-cutting (Patient Management) | **Closed** | `docs/architecture-review/11-RISKS.md`, `20-OPEN-QUESTIONS-RESOLUTION.md` |
| R-07 | Unconfirmed licenses (Novu, Documenso) | 2 running Engines with unconfirmed license terms | Medium | Medium-High | Medium-High | Same legal-review workstream as R-04 | Notification Service, Document Management | Open | `docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md` |
| R-08 | No formal vendor exit strategy documented | Fallback candidates named for every Tier-1 Engine, but no actual exit/migration procedure exists | N/A | Medium-High | Medium-High | SAD to include dedicated Exit Strategy section per Tier-1 Engine | SAD authors | Open | `docs/architecture-review/11-RISKS.md` |
| R-09 | API Gateway product not selected | No Gateway Engine in Technology Baseline; blocks finalizing Edge-layer implementation | Medium | Medium | Medium | **Resolved 2026-07-18: Kong Gateway selected (D-44)** | SAD authors | **Closed** | `docs/api-platform/10, 31`, `20-OPEN-QUESTIONS-RESOLUTION.md` |
| R-10 | Secrets/Vault Engine not selected | No Secrets Engine in Technology Baseline; HashiCorp Vault's 2023 BUSL license change is a relevant complicating factor | Medium | Medium | Medium | **Resolved 2026-07-18: OpenBao selected (D-45)** | SAD authors | **Closed** | `docs/api-platform/12, 31`, `20-OPEN-QUESTIONS-RESOLUTION.md` |
| R-11 | SLA commitments cannot yet be made honestly | No production telemetry exists to set real numeric targets | N/A | Medium | Medium | Defer all numeric SLA/SLO targets until `27-OBSERVABILITY.md` pipeline is live and Open Question #4 answered | SAD authors | Open | `docs/api-platform/28, 30` |
| R-12 | Marketplace/Public API access contingent on unmade business decision | Architecture does not presuppose the platform will monetize a public developer ecosystem | N/A | Low (no commitment made) | Low | No architecture work should proceed on Marketplace/Public API until the business decision is made | Product/Business function (outside this Board's authority) | Open | `docs/api-platform/24, 30` |
| R-13 | Egypt regulatory research incomplete | Cross-Border Transfer (Law 151/2020), Labor Law/Social Insurance impact on Payroll, National ID field requirement all `Requires Legal Verification` | Medium | Medium-High | Medium | Dedicated legal research pass, not yet performed | Legal/Compliance | Open | `.claude/context/open-questions.md` #25-27 |
| R-14 | Home-collection-logistics Build-vs-Buy classification pending | **Resolved 2026-07-18: Open Question #6 answered (Offline Mode = Required, D-48); 0 architectural blockers remain.** Residual scope narrowed to an implementation-level Build-vs-Buy micro-assessment (which local-first sync library/engine) — not an architectural question | N/A | Low-Medium | Low-Medium | Scoped implementation-level micro-assessment during SAD/implementation phase | Specimen Operations, Scheduling and Encounters | **Reduced (Open, non-architectural)** | `docs/reuse/home-collection-logistics/10-final-decision.md`, `20-OPEN-QUESTIONS-RESOLUTION.md` |
| R-15 | Core Domain (ADR-0011) and Bounded Context Map (ADR-0012) remain Proposed | Business-strategy question (Specimen Management alternative) not yet resolved by any architecture phase | N/A | Medium (SAD-readiness impact) | Medium | **Resolved 2026-07-18: both ADRs confirmed Accepted via explicit user review in Open Questions Resolution phase (D-40, D-41); Specimen Management alternative gap disclosed, not concealed, in ADR-0011's own Amendment section** | User / Product Strategy | **Closed** | `docs/adr/0011, 0012`, `20-OPEN-QUESTIONS-RESOLUTION.md` |

## Governance Enhancement — Resolution Gates for High and Medium-High Risks

Added this closure pass, per explicit instruction to strengthen
governance information without changing any risk's Description,
Likelihood, Impact, Severity, Mitigation, Owner, or Status — all five
fields above remain exactly as the certification audit recorded them.
This table adds four new governance fields for the 5 risks rated High
or Medium-High.

| ID | Resolution Gate | Expected Resolution Phase | Required Approval Authority | Closure Evidence |
|---|---|---|---|---|
| R-02 | An Apache Camel migration path is budgeted and scheduled (or upstream Mirth Connect resumes free security patching) | SAD (budgeting/scheduling decision) — full technical resolution at Implementation | Device Integration Gateway Module Owner + Architecture Review Board | SAD's Device Integration Gateway section documents an approved migration path with a committed trigger condition, OR a dated upstream vendor announcement resuming free patching is filed against this risk |
| R-04 | Formal legal counsel opinion issued on all 5 AGPL-3.0 Engines' network-use posture | Before SAD finalizes terms-of-service language for any AGPL-backed API Product (early SAD-phase workstream, per this Board's standing top recommendation) | Enterprise Legal/Compliance function (outside this Board's authority) | A signed, dated legal opinion per Engine filed against `docs/architecture-review/08-AGPL-LEGAL-CHECKLIST.md`, with each of the 5 items marked Cleared or Rejected-with-rationale |
| R-07 | License confirmed (directly or via legal counsel) for both Novu and Documenso | Same legal-review workstream as R-04, before SAD finalizes the Notification Service / Document Management API Products | Enterprise Legal/Compliance | Confirmed SPDX license identifier recorded for both Engines, updating `08-AGPL-LEGAL-CHECKLIST.md` items 6-7 from Unconfirmed to a named license |
| R-08 | An Exit Strategy subsection is drafted and approved for each of the 7 Tier-1 Engines (Keycloak, OPA, ERPNext, OpenBoxes, Kill Bill, Frappe HR, openIMIS) | During SAD — already named in `docs/architecture-review/11-RISKS.md` as an explicit SAD-authored deliverable | Architecture Review Board | SAD contains a dedicated Exit Strategy subsection per Tier-1 Engine, each specifying data-export format, API-compatibility assumptions, and cutover sequencing |
| R-13 | A dedicated legal research pass is completed for all 3 Egypt-market items (Cross-Border Transfer/Law 151-2020, Labor/Social Insurance impact on Payroll, National ID field requirement) | Item 1 (data residency): Before SAD finalizes data-residency architecture. Item 2 (Payroll): Before SAD finalizes the Payroll Module, or During/After SAD if Payroll is confirmed non-v1-critical. Item 3 (National ID): Before SAD finalizes the Patient Management data model | Egypt-market Legal Counsel | Each of the 3 findings recorded in `.claude/context/open-questions.md` #25-27, moved from Open to Answered with a citation to the underlying legal source |

**No risk's substantive assessment changed.** This table is purely
additive governance metadata, verifiable against the unmodified risk
table above.

## Risk Summary by Severity

**Updated 2026-07-18 (Open Questions Resolution):** R-06, R-09, R-10,
and R-15 are now Closed (see their rows above). **Further updated
2026-07-18 (Pre-SAD Baseline Correction):** R-14's architectural
blocker is resolved; it remains Open only as a non-architectural,
implementation-level tracking item (severity unchanged, Low-Medium) —
not counted as Closed since a real (smaller) residual item remains.
Counts below reflect open risks only.

| Severity | Count | IDs |
|---|---|---|
| High | 2 | R-02, R-04 |
| Medium-High | 2 | R-07, R-08 |
| Medium (open) | 4 | R-01, R-03, R-05, R-13 |
| Low / Low-Medium | 2 | R-12, R-14 |
| **Closed this phase** | 4 | R-06, R-09, R-10, R-15 |

**Total risks tracked: 15 (11 open, 4 closed).** The 2 remaining
High-severity risks (R-02 Mirth Connect, R-04 AGPL exposure) and R-13
(Egypt regulatory) are genuine Legal/Regulatory/vendor dependencies
this Board cannot close by architectural decision — correctly left
open, not forced.

## Risks Blocking SAD Work From *Starting*

**None.** Consistent with every prior readiness assessment in this
repository (`docs/architecture-review/13-READINESS-FOR-API-STRATEGY.md`,
`14-READINESS-FOR-SAD.md`), no risk above is a hard blocker to
*beginning* SAD work. **R-15 is now Closed** (Core Domain/Bounded
Context Map confirmed Accepted, 2026-07-18). The remaining two
highest-severity items, R-02 and R-04, are blockers to *finalizing*
specific SAD sections (Device Integration exit strategy, AGPL-backed
API terms of service respectively), not to starting the SAD phase
generally.
