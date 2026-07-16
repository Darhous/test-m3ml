# Vision, Scope, and Operating Model — Healthcare Operations Platform (Wave 1)

**Status: Confirmed (User-Directed, this session)** for the direction
itself — this Wave's content is not Inferred; it restates and structures
the explicit "Confirmed Strategic Direction" the user gave in this
program's authorization prompt (priority 4 in the Source-of-Truth order,
above Proposed ADRs and Discovery Artifacts). Where this Wave adds
structure/organization beyond the user's literal words, that structuring
is tagged `Recommended` (professional judgment, per the Stakeholder
Confirmation Policy), never `Confirmed`.

## Platform Vision

**Confirmed:** the product is **not** a LIMS, a Laboratory Management
System, a Patient Results Portal, or a Billing System alone. It is a
**Healthcare Operations Platform** — a SaaS Multi-Tenant Platform that
manages the operation of healthcare and diagnostic institutions, starting
from Laboratory Management and expanding to the full operating scope listed
below.

## Market Scope

**Confirmed:**
- First target market: **Egypt**.
- Architecture must carry **readiness for additional markets** — not
  built as an Egypt-only system.
- Any Egyptian legal/regulatory requirement not independently verified is
  classified **`Requires Legal Verification`**, never `Confirmed
  Compliance Requirement` (Constitution Section 31 already forbids
  asserting compliance; this Wave applies that rule specifically to
  Egypt).

## Customer Types (Confirmed — must be supported or support-ready)

Independent laboratory · Laboratory chain · Hospital · Medical center ·
Clinic · Medical group · Corporate Healthcare Provider · Multi-branch
diagnostic entity · Partner / external API client.

**Recommended structuring (not in the user's literal list, added for
clarity):** these 9 types cluster into 3 **Organization Models** —
(a) **Single-Facility** (independent lab, single clinic), (b)
**Multi-Facility / Chain** (lab chain, hospital, multi-branch diagnostic
entity, medical group, corporate provider), (c) **Ecosystem / External**
(partner, API client) — because each cluster implies materially different
Tenant/Organization/Branch shapes (Constitution Section 18) and different
onboarding flows. This clustering is `Recommended`, not `Confirmed`.

## Business Scope — 32 Domains (Confirmed list, restated verbatim in English)

Laboratory Operations · Patient Operations · Doctor and Practitioner
Operations · Clinic and Facility Operations · Scheduling and Appointments ·
Home Visits and Sample Collection · Device and Analyzer Operations ·
Quality and Accreditation Operations · Inventory and Reagent Management ·
Procurement and Supplier Management · Billing and Collections · Payments
and Refunds · Expenses and Treasury · Accounting and Financial Control ·
Insurance and Corporate Contracts · Human Resources · Attendance and
Scheduling · Payroll · Training and Competency · Asset and Maintenance
Management · CRM and Customer Support · Complaints and Feedback ·
Notifications and Reminders · Document and File Operations · Analytics and
Business Intelligence · AI-Assisted Operations · Integration Operations ·
Security and Compliance Operations · SaaS Subscription and Commercial
Operations · Partner and Marketplace Operations · Platform Administration ·
Tenant, Organization and Branch Operations.

**Baseline Discovery (Phases 02–12) covered, in real depth, only:**
Laboratory Operations, a slice of Patient/Doctor Operations (as Actors, not
owned domains), Device and Analyzer Operations, a shallow slice of Billing,
Notifications, and a first AI pass. **28 of the 32 domains above are new or
substantially shallow** — this is precisely what Waves 3–12 close.

## Operating Model

**Confirmed:** Unified Login; Role + Permission + Policy + Data Scope
(already Accepted, Constitution Section 20/21); configurable workflows;
configurable result-verification policies (not one fixed rule — see Wave 6
for the full policy model); medical device integration from the first
architecture generation (already Accepted, ADR 0006); Arabic and English,
RTL and LTR (already Accepted, ADR 0010); Multi-Tenant, Multi-Organization,
Multi-Branch (already Accepted, Constitution Section 18); White Label;
Plans and Subscriptions; Usage and Entitlement Tracking; SaaS billing
readiness; On-Premise and Hybrid readiness (already Accepted, ADR 0009).

**New commitments this Wave adds to Confirmed Context (not previously
stated anywhere in this project):** White Label, Plans/Subscriptions,
Usage/Entitlement Tracking, SaaS billing readiness — none of these
contradict any Accepted Constitution rule or ADR (cross-checked: ADR 0009's
SaaS-First posture is a natural home for all four; no conflict found).

## Business Model / SaaS Model

**Confirmed direction, not yet a priced/packaged decision:** the platform
is commercialized as SaaS with tiered plans, usage-based or seat-based
entitlements (mechanism not chosen — **Recommended: defer the specific
metering mechanism to the SAD**, since it is an implementation detail, not
a Discovery-level architectural commitment), and White Label as a product
capability for Partner/Reseller customer types.

## Partner Ecosystem

**Confirmed:** the platform must support Partner and API Client customer
types and a "Partner and Marketplace Operations" domain. **Recommended
(not yet Confirmed):** treat Partner integration as an extension of the
already-Accepted External API Partner pattern (Constitution Section 14–15,
already used for the Insurance/Payer integration in the Baseline Discovery)
rather than inventing a separate mechanism — Wave 9/10 formalizes this.

## Success Outcomes (Recommended, drafted for user confirmation — not
literally dictated in the authorization prompt)

- A healthcare institution can go from signed contract to first live
  transaction (`Tenant-to-Go-Live`, Wave 4) without custom code per tenant.
- A verified result is never released without passing its context-
  appropriate verification policy (Wave 6), regardless of organization
  type or country.
- A Partner/API Client can integrate against a stable, versioned contract
  without needing platform-team involvement per integration.

**These are Recommended candidates for the future SAD's own success
criteria — explicitly not Confirmed**, since no real business KPI was
stated by the user.

## Non-Goals and Scope Boundaries (Recommended, explicit exclusions)

- **Not** a general-purpose Hospital Information System (HIS) covering
  inpatient bed management, surgical scheduling, or pharmacy dispensing —
  those are plausible future domains but were not named in the Confirmed
  Business Scope list above; excluded unless the user adds them.
- **Not** a full financial ERP by default (explicit user instruction: "لا
  تفترض بالضرورة بناء ERP مالي كامل" — do not assume a full financial ERP
  is built natively; Wave 3/10 draws the Native-vs-Integration-vs-Deferred
  line explicitly for Finance).
- **Not** a general-purpose e-commerce or retail platform, despite sharing
  some Inventory/Procurement concepts with one.

## Cross-Check Against Constitution and Accepted ADRs

No item in this Wave was found to contradict Constitution Sections 5–37 or
ADRs 0001–0010. The expansion is additive: it broadens *what* the platform
covers, not *how* it must be governed — the governing rules (Modular
Monolith First, DDD, Schema per Module, Backend-Enforced Authorization,
etc.) apply identically to every new domain named here.
