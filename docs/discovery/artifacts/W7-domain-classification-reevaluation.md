# Domain Discovery and Classification Re-evaluation (Wave 7)

**Status: Draft.** Re-applies Strategic Design/Distillation across the now
much larger evidence base (Wave 3's 100 capabilities, Wave 5's ~114
events) and explicitly does **not** assume Test Processing and Result
Verification (ADR 0011, Proposed) is the final Core Domain, per the user's
direct instruction.

## Re-Classification of All Discovered Domains

| Domain Cluster | Wave 4 Baseline Classification | Wave 7 Re-evaluation |
|---|---|---|
| Test Processing and Result Verification | Core (Proposed, ADR 0011) | **Retained as a strong Core candidate, but no longer assumed the only one — see Decision Matrix** |
| Specimen Management | Supporting (debated) | Unchanged — still debated, same reasoning as Baseline |
| Order Management | Supporting | Unchanged |
| Billing and Claims | Supporting | Unchanged |
| Workforce (HR/Attendance/Payroll/Training) | *(did not exist)* | **Generic** — necessary, industry-commodity, buy/adapt-candidate (Constitution Section 4/6 Generic test: "buy or use open-source") |
| Supply Chain (Inventory/Procurement/Suppliers) | *(did not exist)* | **Supporting** — necessary for lab operation specifically (reagent consumption ties to Core), but not itself differentiating |
| Finance/Accounting/Treasury | *(did not exist)* | **Generic**, per Wave 3's own Native/Integration/Deferred finding — accounting depth is commodity, not differentiating |
| CRM/Support/Complaints | *(did not exist)* | **Generic** |
| Quality/CAPA | *(did not exist)* | **Supporting** — regulatory-necessary, not itself the differentiator, but closely tied to Core (a quality failure directly damages the Core's trust value) |
| SaaS/Platform/Tenant Operations | *(did not exist)* | **Platform** (a distinct classification from Core/Supporting/Generic — see "Platform Tenant Operations" analysis below) |
| AI Operations | Governed layer (Constitution Section 28) | **Supporting** — AI assists every domain; it is not itself where competitive value lives (the *judgment* it assists remains human and domain-specific) |
| Patient/Doctor/Clinic Operations (Wave 5, Cluster G) | *(Actors only, no owned domain)* | **Core-adjacent** — see Decision Matrix, this is the strongest link to the "Orchestration" alternatives below |

## Core Domain Decision Matrix — 6 Alternatives Compared

| Alternative | Description | Evidence Strength | Differentiation Potential | Buy-vs-Build Fit | Scope Coherence with Confirmed Vision (Wave 1) | Risk if Wrong |
|---|---|---|---|---|---|---|
| **Laboratory Execution** *(= original ADR 0011, renamed for this comparison)* | The analytical processing + verification step alone | **Strong** (directly Evidenced, Baseline Phases 03–07) | High *(clinical accuracy is genuinely hard to replicate)* | Must Build | **Weak** — doesn't explain why a Healthcare Operations Platform needs Finance/HR/Supply Chain at all if this alone is Core | Moderate — narrows investment away from orchestration value if wrong |
| **Diagnostic Operations** | Laboratory Execution broadened to the full diagnostic value chain (Order→Specimen→Result) | Strong (Evidenced, same base as above + Order/Specimen contexts) | High | Must Build | Weak-Moderate — still lab-centric, doesn't address non-diagnostic domains | Moderate |
| **Patient-to-Result Orchestration** | The end-to-end *coordination* across Order→Specimen→Process→Verify→Release→Bill→Notify is the differentiator, not any single stage | **Strong** (directly builds on Baseline's already-identified "Order Fulfillment Policy" cross-context Process Manager, Phase 07) | **High** — seamless multi-step orchestration without manual handoffs is genuinely hard to replicate and directly serves the "not a plain CRUD system" vision (Constitution, original) | Must Build | **Strong** — explains why the platform needs many domains coordinated, not just one deep | Lower — even if the specific "which flow" emphasis shifts, the orchestration-is-the-value thesis is robust |
| **Healthcare Operations Orchestration** | Generalizes the above across *all* 32 domains — the platform's cross-domain orchestration itself, not just the clinical flow | Moderate (evidence exists for the clinical case; Finance/Workforce/Supply Chain orchestration is entirely Inferred, per Wave 3's evidence-distribution finding) | **Highest, if achievable** — matches Wave 1's Confirmed Vision almost verbatim | Must Build | **Strongest** — direct match to Confirmed Vision | **Higher** — premature to commit deep investment platform-wide before any single non-clinical domain has real evidence |
| **Clinical Diagnostic Network** | Network-effects framing (multi-facility/practitioner referral network, marketplace dynamics) | **Weak** — no evidence anywhere in this project of a network/marketplace business model; Wave 1's Partner/Marketplace capability is explicitly flagged "speculative" | Unknown — depends entirely on an unconfirmed business-model bet | Unknown | Weak — not stated in Wave 1's Confirmed direction | **High** — would commit to a business model the user never confirmed |
| **Platform Tenant Operations** | The multi-tenant SaaS platform capability itself is the differentiator | Moderate (Evidenced at Constitution level — Section 10/18, Hybrid Tenant Isolation) | **Low, by DDD's own definition** — see reasoning below | Partially (some SaaS infrastructure is commodity-buyable) | Moderate — Confirmed as a requirement, not stated as *the* differentiator | Low if rejected (doesn't foreclose treating it as Platform/Generic, which is likely correct anyway) |

### Why "Platform Tenant Operations" Is Reasoned Out, Not Just Dismissed

DDD's Core/Generic distinction is specifically about where *competitive,
differentiating* value lives versus *necessary infrastructure*. Being a
well-built multi-tenant SaaS platform is close to table-stakes for any
modern B2B healthcare software vendor — it's necessary (and the user's
Wave 1 direction confirms it's Required), but competitors can and do build
equivalent multi-tenancy. This is a textbook **Platform** classification
(a fourth category alongside Core/Supporting/Generic, already implicitly
used in Wave 3), not a Core Domain candidate. Rejected as Core, but
retained as a first-class Platform concern.

## Recommendation (Recommended, not Confirmed — requires user decision)

**Recommended: revise ADR 0011 from "Laboratory Execution" (as originally
scoped) to "Patient-to-Result Orchestration."** This is the strongest
alternative on the matrix: it retains nearly all of the original evidence
base (the same Aggregates, events, and Sensitive Operations still apply —
this is a *reframing* of what makes them valuable, not new discovery), it
directly resolves the Wave 1 scope-coherence gap the original proposal
had, and it is meaningfully less risky than jumping straight to the
platform-wide "Healthcare Operations Orchestration" framing before any
non-clinical domain has real evidence.

**"Healthcare Operations Orchestration" is flagged as a plausible future
evolution**, not adopted now — Wave 13's evidence-distribution numbers
(still heavily clinical-weighted) don't yet support committing to a
platform-wide orchestration thesis with confidence.

**"Clinical Diagnostic Network" is not recommended** — no evidence
supports it and adopting it would require a business-model confirmation
the user has not given.

This recommendation feeds Wave 9 (which re-evaluates ADR 0012, the
Bounded Context Map, using whichever Core Domain framing is adopted) and
is formally decided (Retain/Amend/Supersede/Reject) in Wave 14's ADR
disposition — not unilaterally changed here.

## Buy vs. Build vs. Commodity Summary (per the user's explicit questions)

| Question | Answer |
|---|---|
| What can be bought/integrated rather than built? | Accounting/General Ledger depth (Wave 3), generic HR/Payroll processing (industry-commodity), generic CRM ticketing |
| What must the platform own? | Patient-to-Result orchestration logic, Result Verification Policy Model (Wave 6), Device Integration ACL, Tenant/Data-Scope enforcement |
| What achieves competitive advantage? | Seamless cross-domain orchestration (per the recommendation above), configurable verification policy depth, Egypt-market fit (Wave 11) |
| What is commodity? | Generic notification delivery mechanics, generic expense tracking, generic attendance tracking |
