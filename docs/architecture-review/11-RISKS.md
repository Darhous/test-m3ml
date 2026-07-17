# Risk Register

Consolidated from every risk flagged across `docs/reuse/`'s 106 Feature
files plus this Board's own review findings. Each risk is rated
Likelihood × Impact (Low/Medium/High), consistent with the reuse
program's own per-Feature risk tables.

## R-01 — Eramba Community low-confidence GRC decision

**Likelihood:** Medium. **Impact:** Medium. **Source:**
`audit-and-compliance/compliance-tracking/12-risk-analysis.md`, this
Board's `03-ENGINE-BASELINE.md`. **Description:** The platform's
compliance-tracking Engine was selected with the program's own
lowest-confidence rating, and no stronger alternative has surfaced
across the full 28-Module program (Quality Management's Module 16
search also found nothing better). **Mitigation:** Reconsider at SAD
time with a dedicated, focused re-search (permitted — this is exactly
the "verify a blocker" exception to this phase's no-market-scan rule,
though this Board judged it not yet a blocker). **Owner:** Audit and
Compliance.

## R-02 — Mirth Connect frozen-release risk

**Likelihood:** High (already realized — the freeze is a present fact,
not a future possibility). **Impact:** High. **Source:**
`device-integration-gateway/hl7-integration-engine/12-risk-analysis.md`,
re-confirmed in `03-ENGINE-BASELINE.md`. **Description:** Mirth Connect
4.5.2 is the last free release; NextGen's March 2025 shift means no
free security patches going forward. **Mitigation:** Apache Camel
remains a documented, evaluated fallback (Apache-2.0, actively
maintained). **Recommendation: budget a Camel migration path explicitly
in the SAD rather than treating Mirth 4.5.2 as a permanent fixture.**
**Owner:** Device Integration Gateway.

## R-03 — ERPNext concentration risk (single-Engine footprint across 5 Modules)

**Likelihood:** Low (ERPNext is mature and actively maintained).
**Impact:** High if realized (an ERPNext-level failure or vendor
discontinuation would simultaneously affect Procurement, Supplier
Management, Billing, Payments and Treasury, and Accounting).
**Source:** New finding, this Board (`MASTER_DEPENDENCY_MATRIX.md`'s
own ERPNext row already documents the breadth; the *concentration risk
framing* is this Board's addition, not carried from the reuse program
verbatim). **Description:** No single reuse decision is wrong, but the
cumulative effect of consistently reusing the same Engine across 5
Modules creates a single point of organizational dependency the
original per-Module decisions did not individually surface. **Mitigation:**
Not a reason to reverse any individual decision (each was independently
justified) — but the SAD should document ERPNext as a
Tier-1-criticality dependency with an explicit exit-strategy review
(see R-08), not treat its breadth as a merely incidental efficiency win.
**Owner:** Cross-cutting (Procurement holds the Single Adoption Point).

## R-04 — AGPL-3.0 legal exposure (5 running Engines)

**Likelihood:** Medium (depends on legal review outcome, not yet known).
**Impact:** High (could require re-opening a Build-vs-Buy decision for
one or more of Cal.com, Atlas CMMS, openIMIS, Frappe Helpdesk, Frappe
CRM if legal review finds the network-use clause unacceptable).
**Source:** `08-AGPL-LEGAL-CHECKLIST.md`. **Mitigation:** Formal legal
review scheduled as an explicit early SAD-phase workstream (this
Board's top recommendation). **Owner:** Enterprise legal/compliance
function (outside this Board's authority to assign further).

## R-05 — Frappe ecosystem license drift and operational sprawl

**Likelihood:** Medium. **Impact:** Medium. **Source:**
`crm-and-support/helpdesk-ticketing/02-global-search.md`, this Board's
`07-LICENSE-REVIEW.md`. **Description:** The platform now runs 4
separate Frappe-family applications (ERPNext, Frappe HR, Frappe
Helpdesk, Frappe CRM) under 2 different licenses (GPL-3.0 for the first
2, AGPL-3.0 for the latter 2) — same vendor, same framework, different
legal posture. Operationally this means 4 independent upgrade cadences
despite shared tooling; legally it means the AGPL items cannot inherit
the GPL items' clearance. **Mitigation:** Already reflected in
`08-AGPL-LEGAL-CHECKLIST.md`'s per-Engine treatment; this Board adds the
explicit recommendation that SAD-phase infrastructure planning treat
these as 4 independently-versioned deployments, not one "Frappe
platform" unit. **Owner:** Workforce Management (Frappe HR), CRM and
Support (Helpdesk/CRM), Procurement (ERPNext).

## R-06 — FHIR resource version not explicitly pinned

**Likelihood:** Low. **Impact:** Medium. **Source:** New finding, this
Board. **Description:** `MASTER_REPOSITORY_DATABASE.md` and every
Feature file referencing FHIR resources (Patient, ServiceRequest/Task,
Encounter, Specimen, DiagnosticReport, Claim/Coverage) never explicitly
states which FHIR version (R4, R4B, R5) is assumed — the reuse program
consistently used FHIR as a Reference pattern without version-pinning.
**Mitigation:** The SAD must explicitly pin a FHIR version (R4 is the
most likely candidate given its current dominance in the referenced
production systems — OpenELIS Global, openIMIS, HL7 Europe Laboratory
Report IG — but this Board does not assert R4 as decided, only as the
evidence-weighted default worth stating explicitly rather than leaving
implicit). **Owner:** Cross-cutting (Patient Management holds the
originating Reference Adoption Point).

## R-07 — Unconfirmed licenses on 2 running Engines (Novu, Documenso)

**Likelihood:** Medium. **Impact:** Medium-High (Documenso is Sensitive-
Operation-adjacent). **Source:** `08-AGPL-LEGAL-CHECKLIST.md` items 6-7.
**Mitigation:** Same legal-review workstream as R-04. **Owner:**
Notification Service (Novu), Document Management (Documenso).

## R-08 — No formal vendor exit strategy documented for any Engine

**Likelihood:** N/A (a documentation gap, not a probabilistic risk).
**Impact:** Medium-High if a Tier-1 Engine (ERPNext, Keycloak, Kill
Bill, OpenBoxes) needed to be replaced under time pressure without a
pre-considered path. **Source:** New finding, this Board (Task 16).
**Description:** Every Engine decision in `MASTER_DECISION_REGISTER.md`
names a fallback *candidate* (e.g., Apache Camel for Mirth Connect,
Lago for Kill Bill, Odoo for ERPNext) but none of the 106 Feature files
documents an actual **exit/migration procedure** (data-export format,
API-compatibility assumptions, cutover sequencing). Fallback candidates
being named is necessary but not sufficient for a genuine exit strategy.
**Mitigation: this Board recommends the SAD include a dedicated "Exit
Strategy" section per Tier-1 Engine** (Keycloak, OPA, ERPNext, OpenBoxes,
Kill Bill, Frappe HR, openIMIS — the 7 Engines whose data/identity model
is deepest-embedded) rather than treating the fallback candidates listed
in `02-TECHNOLOGY-BASELINE.md` as if they already constitute a plan.
**Owner:** SAD authors (not resolvable at this phase).

## Architectural Conflict Verification (Task 13)

**Finding: No architectural conflict found between any two ratified
technologies.** Verified by cross-checking every Engine pairing that
shares a domain boundary against `MASTER_DEPENDENCY_MATRIX.md`'s
Detected Duplicate Features log (9 of 9 resolved) plus this Board's own
`03-ENGINE-BASELINE.md` Boundaries column (all `✓` except the ERPNext
concentration note, which is a risk-management finding, not a conflict).

## Upgrade Compatibility Between Major Engines (Task 14)

**Finding: no cross-Engine upgrade-compatibility conflict identified**,
with one caveat this Board flags explicitly (not present in the reuse
program's own record): **ERPNext and Frappe HR/Helpdesk/CRM share the
Frappe Framework** — a major-version upgrade to the underlying Frappe
Framework itself would need to be coordinated across all 4 applications
simultaneously, not rolled out independently, since they are framework
siblings, not independent products. This is a **new operational
constraint this Board is surfacing**, not a reuse-program finding — no
`docs/reuse/` file discusses Frappe Framework version coupling across
its 4 consuming apps. **Recommendation:** the SAD's upgrade-policy
section should treat "the Frappe Framework" as a single upgrade unit
spanning 4 Engines, not 4 independent upgrade policies.

## Vendor Lock-In Verification (Task 15)

**Finding: no technology creates *unacceptable* vendor lock-in**, with
the concentration risk (R-03) and Frappe-framework coupling (Task 14
finding above) noted as **elevated but not unacceptable** lock-in,
given: (a) every Tier-1 Engine is open-source and self-hostable (no
Engine requires an ongoing SaaS relationship with its vendor to keep
running), and (b) every Engine decision names at least one evaluated
fallback candidate. **This Board does not find any single-vendor
proprietary dependency in the Technology Baseline** — the closest cases
(Fawry, Paymob, WhatsApp BSP) are explicitly logged as Vendor/commercial
decisions outside the OSS Build-vs-Buy scope, not Baseline-frozen
technology choices, and by design are abstracted behind the platform's
own `payment-gateway-abstraction` BUILD layer specifically to avoid
lock-in to any one gateway.

## Risk Summary

| Risk | Likelihood | Impact | Status |
|---|---|---|---|
| R-01 Eramba low confidence | Medium | Medium | Open, monitored |
| R-02 Mirth Connect frozen | High | High | Open, mitigation identified (Camel) |
| R-03 ERPNext concentration | Low | High | Open, documentation recommendation |
| R-04 AGPL-3.0 legal exposure | Medium | High | Open, legal review required |
| R-05 Frappe ecosystem sprawl | Medium | Medium | Open, documentation recommendation |
| R-06 FHIR version unpinned | Low | Medium | Open, SAD action item |
| R-07 Unconfirmed licenses (Novu, Documenso) | Medium | Medium-High | Open, legal review required |
| R-08 No formal exit strategy | N/A | Medium-High | Open, SAD action item |

**Risks requiring attention before API Strategy: 6** (R-01, R-02, R-04,
R-05, R-07, R-08 — R-03 and R-06 are SAD-phase, not API-Strategy-phase,
concerns).
