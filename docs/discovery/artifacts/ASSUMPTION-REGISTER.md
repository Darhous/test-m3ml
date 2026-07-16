# Assumption Register

**Purpose:** every fact used in Discovery that is not directly Confirmed by
the user or an existing Accepted document is logged here as
`Inferred — Industry Reference`, with its source and the phase that
introduced it. Nothing in this register is `Accepted` project fact — it is
working material for Discovery, explicitly separated from Confirmed content
per the user's chosen execution mode (Assumption-Driven Autonomous Run,
approved at Discovery Program start). Every entry must be reviewed and
either Confirmed, corrected, or rejected by the user before any Software
Architecture Document work begins (Constitution Section 2/46 already
requires this kind of settling before final documents).

**Status vocabulary for this register (distinct from the Context Store's
Decision Status vocabulary, same separation principle as Constitution
Section 59):**
- `Inferred — Industry Reference`: standard, well-established laboratory/
  healthcare industry practice, not specific to this company; used to make
  Discovery executable without live stakeholder interviews per the user's
  chosen mode.
- `Inferred — Extrapolated`: derived from a Confirmed fact by reasonable
  extension (cited).
- `Pending User Confirmation`: explicitly flagged for the user to confirm/
  reject in a future review pass.

| # | Assumption | Status | Source / Basis | Phase Introduced | Confidence |
|---|---|---|---|---|---|
| 1 | The Business Capability Map's 20 capabilities (Test Ordering, Specimen Collection, Accessioning, Rejection/Recollection, Processing, Verification, Reporting, etc.) | Inferred — Industry Reference | Standard laboratory information system (LIS) operational model | 02 | Medium-High (well-established industry pattern, but not confirmed for this specific platform) |
| 2 | Core/Supporting/Generic candidate tags in the Capability Map | Inferred — Industry Reference | DDD Strategic Design lens applied to Assumption #1 | 02 | Low (explicitly Candidate; Phase 04 re-derives from real event evidence, not this tagging) |
| 3 | Four traced Value Streams (VS1–VS4) and their step outlines | Inferred — Industry Reference | Standard LIS + billing workflow pattern | 02 | Medium |
| 4 | 15 stakeholder categories' "Candidate Primary Needs" (see `.claude/context/stakeholders.md`, Discovery Phase 02 section) | Inferred — Industry Reference | Standard healthcare/lab stakeholder needs pattern | 02 | Low-Medium (needs real confirmation per category; explicitly flagged in the file itself) |
| 5 | A supplier/procurement value stream was NOT traced (gap, not an assumption) | N/A — explicit gap | Deliberately left untraced pending real input | 02 | N/A |
| 6 | Full event/command/actor chain for VS1–VS4 (26 events total) | Inferred — Industry Reference | Standard LIS event flow | 03 | Medium |
| 7 | Rejection reason taxonomy (Insufficient Volume, Hemolyzed, Clotted, Mislabeled, Wrong Container, Contaminated) | Inferred — Industry Reference | Standard specimen-QC practice | 03 | Medium-High (very standard in lab QC, but exact taxonomy for this platform unconfirmed) |
| 8 | 5 candidate Pivotal Events (`ResultVerified`, `ResultReleased`, `SpecimenAccessioned`, `SpecimenRejected`, `ClaimAdjudicated`) | Inferred — derived from Assumption #6 via handoff analysis | Event Storming method applied to Assumption #6 | 03 | Medium |
| 9 | 4 candidate missing events (equipment-failure event, failed-home-visit event, chain-of-custody handoff event, claim-denial event) were identified as gaps, not fabricated | N/A — explicit gap, logged as Hotspots H2/H4/H5/H9 | Deliberately left as gaps | 03 | N/A |
| 10 | 11 candidate Subdomains and their Core/Supporting/Generic classification | Inferred — DDD Strategic Design applied to Assumptions #1/#6 | `domain-driven-design` skill Strategic Design method | 04 | Medium for Subdomains #1–8; **Low** for #9–11 (no Event Storming evidence) |
| 11 | Core Domain proposed as "Test Processing and Result Verification" | Inferred — Extrapolated (Domain Vision Statement reasoning) | Constitution Section 4 Core Value ("Human accountability"), Section 21/23 Sensitive-Operation weight | 04 | Medium — genuinely competing hypothesis (Specimen Management / Home Collection) explicitly noted, pending real business-strategy input |
| 12 | `module-catalog.md`'s "Laboratory Modules" category likely splits into 3 finer Subdomains; "Insurance Modules" folded into "Billing and Claims" | Inferred — derived from event clustering | Phase 04 clustering exercise | 04 | Medium |
| 13 | Candidate Aggregates for Subdomains 1, 2, 3, 5, 7 (TestOrder, Specimen, TestResult, Invoice/Claim, DeviceImportRecord) | Inferred — DDD tactical patterns applied to Phase 03 events | `domain-driven-design` skill, Entity/Value Object tests | 05 | Medium |
| 14 | Subdomains 9–11 have NO candidate Aggregates (explicit gap, not fabricated) | N/A — explicit gap | Zero Event Storming evidence | 05 | N/A |
| 15 | `ResultCorrected` and `ClaimDenied`/`ClaimRejected` identified as missing events | Inferred — Extrapolated from DDD event-immutability practice + Constitution Section 12's own example | Standard event-sourcing/DDD practice | 05 | Medium-High (well-established pattern, but existence in this platform unconfirmed) |
| 16 | All invariants, state machines, and cross-Aggregate Policies in `07-business-rules-catalog.md` | Inferred — Industry Reference + DDD/Constitution rule application | Standard LIS business rules + direct application of Constitution Section 21/23/25/26 | 07 | Medium (rule *shape* well-grounded in Constitution; specific *thresholds/criteria* explicitly Open, not assumed) |
| 17 | Result Verifier Role established as a distinct authorization gate for `ResultVerified`/`ResultCorrected` | Inferred — direct application of Constitution Section 21 (Sensitive Operations require elevated controls) | Constitution Section 21 (Accepted) | 07 | High for the *rule shape* (directly derived from an Accepted Constitution rule); Low for the *eligibility detail* (fully Open, #19) |
| 18 | Device protocol categories (HL7v2, ASTM, Vendor API), notification channel candidates (SMS/Push/Email/Portal/WhatsApp) | Inferred — Industry Reference, partially derived from Constitution Section 24's already-Accepted readiness list | Constitution Section 24 (Accepted) + LIS industry practice | 08 | Medium (categories well-grounded; specific selection unconfirmed) |
| 19 | Insurance/Payer integration pattern (Anti-Corruption Layer + Conformist) | Inferred — Extrapolated from standard payer-integration DDD practice | `domain-driven-design` skill Context Mapping patterns | 08 | Medium |
| 20 | Chain-of-custody record design (handoff sequence with timestamp/actor/confirmation) | Inferred — Extrapolated, design proposal only | Standard logistics chain-of-custody practice | 08 | Low-Medium — explicitly a proposal, not a requirement confirmation |
| 21 | Legacy system integration profile — explicitly NOT invented | N/A — explicit gap | Zero basis found anywhere in context | 08 | N/A |
| 22 | Every Phase 05 Aggregate is missing explicit Tenant-scoping fields (Gap, not a design choice) | N/A — explicit gap found via review | Constitution Section 18 requirement applied to Phase 05 structures | 09 | N/A (gap, not assumption) |
| 23 | Two candidate categories for shared-tier data partitioning (tenant-ID-column, schema-per-tenant) | Inferred — Extrapolated from ADR 0005 + `architecture-patterns` skill | ADR 0005 (Accepted) | 09 | Medium |
| 24 | Money and dual-timestamp Value Object patterns proposed for Invoice/DeviceImportRecord | Inferred — Extrapolated, standard localization-safe modeling pattern | Constitution Section 32 (Accepted) applied to Phase 05 gaps | 09 | Medium-High (well-established pattern; specific field shape unconfirmed) |
| 25 | 7 candidate AI use cases across 5 Bounded Contexts | Inferred — Industry Reference, derived from Phase 03/07 events/rules within Constitution Section 28's Permitted list | Constitution Section 28 (Accepted) applied to Phase 03/07 findings | 10 | Medium |
| 26 | AI Gateway contract shape (input/output/audit fields) | Inferred — Extrapolated from Constitution Section 23/28 requirements + `api-design-principles` skill | Constitution Section 23/28 (Accepted) | 10 | Medium |

*(Populated as Discovery proceeds — see phase reports for entries added
each phase; this table is the consolidated index, kept in sync at the end
of every phase.)*

## Gap Closure Wave 13 — Consolidated Entries (Waves 1–12)

Waves 1–12 each deliberately deferred logging their own new assumptions
individually here, to avoid the register becoming unusable (Wave 3 alone
would have added ~84 near-identical rows for its capability entries) —
each Wave report explicitly stated "consolidated at Wave 13." This section
fulfills that deferral with one consolidated row per Wave (or per distinct
assumption category within a Wave), rather than one row per individual
capability/event/rule/context. Full per-item detail remains in each Wave's
own artifact; nothing here overrides an individual item's status if that
item is more precisely typed in its source artifact.

| # | Assumption | Status | Source / Basis | Wave Introduced | Confidence |
|---|---|---|---|---|---|
| 27 | 3-cluster Organization Model grouping (Single-Facility / Multi-Facility-Chain / Ecosystem-External) — added structure beyond the user's literal customer-type list | Recommended | Wave 1 reasoning applied to the 9 Confirmed customer types | 1 | Medium |
| 28 | All 39 persona Goals/Pain Points/KPIs | Inferred — Industry Reference | Standard healthcare/lab/financial/workforce stakeholder-needs patterns | 2 | Low-Medium (per-category confirmation still needed, consistent with Baseline Assumption #4) |
| 29 | 84 of 100 Enterprise Capability Map entries (`Inferred` or `Confirmed-scope/Inferred-detail`) | Inferred — Industry Reference | Standard healthcare-operations capability patterns applied to the 32 Confirmed business domains | 3 | Medium (scope Confirmed by the user; internal detail Inferred) |
| 30 | 18 newly traced Value Streams (of 20 total) | Inferred — Industry Reference | Standard healthcare-operations workflow patterns | 4 | Medium |
| 31 | ~84 newly modeled Domain Events across 10 clusters | Inferred — Industry Reference | Event Storming method applied to Wave 3/4 findings | 5 | Medium |
| 32 | 26-rule Business Rules catalog + Configurable Result Verification Policy Model's illustrative axis values | Inferred — Industry Reference | Standard healthcare business-rule patterns + Constitution Section 21/23/25/26 applied to Wave 5 events | 6 | Medium (rule *shape* well-grounded in Constitution; specific thresholds explicitly Open per `open-questions.md` #23) |
| 33 | 6-alternative Core Domain Decision Matrix, including the "Patient-to-Result Orchestration" recommendation | Inferred — Extrapolated | Wave 3/4/5 findings reasoned against DDD Core Domain criteria | 7 | Medium — explicitly a Recommendation, not a decision; ADR-0011 disposition deferred to Wave 14 |
| 34 | 19 "Recognized" (as opposed to "Modeled") Bounded Context justifications in the 28-context remap | Inferred — Industry Reference | DDD Context Mapping patterns applied to Wave 3/5 findings; the 9 "Modeled" contexts inherit Evidenced status already established in the Baseline/Wave 5, not a new assumption | 9 | Low-Medium for Recognized tier (explicitly lower-confidence by design); Medium-High for Modeled tier |
| 35 | 7 industry-practice/product-recommendation Egypt market items (considerations #6, #7, #14, #16-partial, #18, #19, #20, #21) not covered by this round's live regulatory research | Inferred — Industry Reference / Recommended | Wave 11 explicit distinction from the 4 researched regulatory items (which are `Requires Legal Verification`, not assumptions) | 11 | Low-Medium |
| 36 | 7 newly surfaced Wave 12 security/privacy/clinical-safety risks (SEC-06, 07, 09, 10, 11, 12, 13) | Inferred | Industry-standard threat-modeling reasoning (STRIDE) applied to Waves 3–10's own findings, not independently researched | 12 | Medium |

*(Wave 8's Ubiquitous Language expansion and Wave 10's Candidate Modules
introduced no new assumption category — both explicitly inherit
Evidence/Assumption status from prior Waves, per their own reports.)*
