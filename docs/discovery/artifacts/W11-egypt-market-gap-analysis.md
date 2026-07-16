# Egypt Market Gap Analysis (Wave 11)

**Status: Draft.** Every item below is explicitly typed per the Research
Rules: **Legal** (primary statute), **Regulatory** (agency decision/
guidance), **Industry Practice** (observed market norm, not law),
**Product Recommendation** (Recommended, not Confirmed), or
**Architectural Inference** (a Discovery-level design implication). No
item is a compliance claim (Constitution Section 31).

| # | Consideration | Type | Basis | Architectural Implication |
|---|---|---|---|---|
| 1 | Arabic-first usability | **Confirmed** (user's Wave 1 direction + ADR 0010, already Accepted) | User's authorization prompt | Already governed — Constitution Section 32. No new finding. |
| 2 | English support | **Confirmed** | Same as #1 | Already governed. |
| 3 | RTL | **Confirmed** | Same as #1 | Already governed (ADR 0010). |
| 4 | E-invoicing / e-receipt readiness | **Regulatory**, Requires Legal Verification | `EGYPT-REGULATORY-RESEARCH-REGISTER.md` #1 | Billing/Payments/Accounting modules (Wave 10) should be designed with a pluggable fiscal-integration point, not a hardcoded assumption of no e-invoicing — Architectural Inference, Recommended. |
| 5 | Tax readiness | **Regulatory**, Requires Legal Verification | Register #1 (simplified tax system, Law 6/2025) | Same as #4 — pricing/invoicing must support tax-inclusive calculation as a configurable concern, not fixed. |
| 6 | Payment channels | **Industry Practice** | General market observation, not independently sourced this Wave | Cash, card, and mobile-wallet payment methods are all plausible in the Egyptian market — Payments and Treasury (Wave 9/10) should not assume a single payment channel. Flagged Inferred, not researched in depth this pass. |
| 7 | Cash-heavy operations | **Industry Practice** | General market observation | Reinforces #6 — Cashbox/Treasury capability (Wave 5, Cluster A) is not optional even in a "digital-first" platform. |
| 8 | Insurance and corporate contracts | **Regulatory-adjacent**, Requires Legal Verification | Register #4 (Universal Health Insurance Law) | Insurance and Corporate Contracts (Wave 9) must accommodate both private corporate contracts (already modeled) and a future public UHIA/EHA-facing integration — flagged as a *possible* future integration, not designed here (no evidence of what that integration would look like). |
| 9 | Branch and franchise operations | **Confirmed** (Wave 1 — Multi-Branch, chain/multi-facility customer types) | User's direction | Already governed (Constitution Section 18, Tenant/Organization/Branch). |
| 10 | Home visit logistics | **Confirmed + Evidenced** (Baseline VS2, Wave 4) | Baseline Discovery | Already modeled; Egypt-specific traffic/address-format realities not researched this pass — flagged as a gap. |
| 11 | Connectivity limitations | **Industry Practice** (plausible in parts of Egypt, especially rural/Upper Egypt regions per the UHIA phased-rollout geography, Register #4) | Inferred from the UHIA rollout's own geographic phasing (Port Said, Luxor, Ismailia, South Sinai, Aswan, Suez, Minya — several are less urbanized regions) | Reinforces `open-questions.md` #6 (Offline Mode) — this Wave adds Egypt-specific plausibility, does not resolve the question. |
| 12 | Offline needs | Same as #11 | Same | Same — still Open (#6), now with a specific geographic rationale attached rather than a generic one. |
| 13 | Data residency considerations | **Legal-adjacent**, Requires Legal Verification | Register #2 (PDPL 151/2020) | The PDPL's cross-border transfer provisions (not independently confirmed in this research pass) may require Egypt-hosted or Egypt-approved-transfer data storage for Egyptian patient data — directly relevant to ADR 0009 (On-Premise/Hybrid readiness), reinforces rather than contradicts that existing decision. |
| 14 | Local support operations | **Product Recommendation** | Not independently researched | Recommended: local-language, local-timezone support operations — a product/operations decision, not an architectural one. |
| 15 | Local device/vendor realities | **Regulatory-adjacent**, Requires Legal Verification | Register #3 (EDA device/reagent registration) | Device Integration Gateway (ADR 0006) should track a device/reagent's EDA registration status as Supplier Management metadata (Wave 5) — Architectural Inference, Recommended. |
| 16 | Local accounting practices | **Product Recommendation**, Requires Legal Verification for specifics | Not independently researched (Egyptian Accounting Standards not looked up this pass) | Reinforces Wave 3's Accounting Native/Integration/Deferred finding — local GAAP-equivalent rules are a strong argument for Integration-capable rather than deep-native Accounting. |
| 17 | Local payroll considerations | **Legal**, Requires Legal Verification | Not independently researched this pass (Egyptian Labor Law / Social Insurance Law not looked up) | **Gap** — flagged for a dedicated future research pass; Payroll (Wave 9/10) already has a high-sensitivity, dual-control design (Wave 6) that is compatible with additional local-law constraints once researched. |
| 18 | Patient identity realities | **Product Recommendation** | Not independently researched (National ID integration not looked up) | Recommended: Patient Management (Wave 9) should accommodate a National ID-based identity field as a first-class concept, not a generic free-text field — flagged for SAD, not designed here. |
| 19 | Phone-number-centric communication | **Industry Practice** | General regional market observation | Reinforces Notification and Communication's channel candidates (Baseline Phase 08/Wave 5) — phone-number-keyed identity (for SMS/WhatsApp) is a plausible primary contact method, not email-first. |
| 20 | SMS and messaging preferences | Same as #19 | Same | Same — already a candidate channel (Baseline Phase 08); no new channel added, just reinforced. |
| 21 | Pricing and discount practices | **Product Recommendation** | Not independently researched | Recommended: Wave 6's Discount rule (role-authorized limit) should remain configurable per-branch, since Egyptian retail/service pricing practice commonly includes negotiated/promotional pricing — Inferred, not confirmed. |

## Summary

**21 considerations addressed.** 4 directly traced to real, dated
regulatory/legal sources via `WebSearch` (e-invoicing, PDPL, EDA device
registration, UHI Law — all logged in
`EGYPT-REGULATORY-RESEARCH-REGISTER.md`). 3 Confirmed (Arabic/English/RTL,
already Accepted ADR 0010). The remainder are Industry Practice or Product
Recommendation, explicitly not conflated with the researched legal items.
**Zero compliance claims made** — every regulatory/legal item carries
`Requires Legal Verification`, consistent with Constitution Section 31 and
this program's explicit instruction.
