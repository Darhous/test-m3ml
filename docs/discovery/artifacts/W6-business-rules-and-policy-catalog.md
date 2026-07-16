# Business Rules and Policy Catalog (Wave 6)

**Status: Draft — Inferred unless noted.** Extends
`artifacts/07-business-rules-catalog.md` (retained unchanged) with the 24
rule categories the user named, plus a fully-specified **Result
Verification Policy Model** — the single most detailed requirement in the
user's authorization prompt, addressed as this Wave's centerpiece.

## Centerpiece: Configurable Result Verification Policy Model

**Confirmed requirement (user's explicit direction, not inferred):** no
single fixed rule for who approves a result. The policy must vary by
Organization Type, Analysis Type, Risk/Severity, Specialty, Approval
Level, User Role, Branch Policy, and Country Policy, with Emergency
Override support. Every verification must be Backend-Enforced, Audited,
Traceable, Versioned, and Configurable within safe limits.

### Relationship to the Baseline's Existing Rule (not a contradiction)

Baseline Phase 07 established: "a Result may only transition to `Verified`
by an actor holding a distinct **Result Verifier** Role." This Wave
**does not reverse that** — it refines it into the *default, safe-minimum*
policy that a configurable policy engine falls back to when no more
specific policy matches. The floor (a dedicated Role gate, never the
general Laboratory Staff Role) remains non-negotiable; what becomes
configurable is *which* Role(s) qualify and *how many* sign-offs are
required, per context.

### Policy Model Structure (Discovery-level design, not implementation)

A **Verification Policy** is evaluated against a **Verification Context**:

| Context Dimension | Example Values (Inferred, illustrative only) |
|---|---|
| Organization Type | Independent lab, Hospital, Corporate provider (Wave 1's 9 customer types) |
| Analysis Type | Routine chemistry, Critical/panic-value test, Genetic test *(illustrative — no real test catalog exists yet)* |
| Risk/Severity Level | Low, Moderate, Critical *(ties directly to the new `Critical Results` capability, Wave 3)* |
| Specialty | General, Pathology, Genetics *(illustrative)* |
| Branch Policy | Branch-specific override of an Organization-level default |
| Country Policy | Egypt-specific requirement layer (ties to Wave 11 — `Requires Legal Verification` where not independently confirmed) |

A matching policy resolves to:

| Policy Output | Description |
|---|---|
| Required Approval Level | Single sign-off (Baseline default) / Dual sign-off / Multi-specialty sign-off |
| Eligible Role(s) | Which Role(s) — never the general Laboratory Staff Role — may perform this specific verification |
| Emergency Override Allowed? | Whether a Break-Glass-style override (Constitution Section 21) may bypass the normal policy |
| Override Justification Required? | If override allowed, a captured justification is mandatory (Constitution Section 21, already Accepted) |

### The Four Non-Negotiable Properties (Confirmed, user's explicit words)

| Property | How This Model Satisfies It |
|---|---|
| Backend Enforced | Policy resolution and the resulting Role gate happen server-side only — never a client-side check (Constitution Section 21, already Accepted, reaffirmed here). |
| Audited | Every policy resolution (which policy matched, what it required, who performed the verification) is itself an Audit Event (Constitution Section 23). |
| Traceable | The specific policy version that governed a given `ResultVerified` event is recorded on that event, not just "current policy" — a policy change never retroactively changes what a past verification "should have" required. |
| Versioned | Policies are versioned artifacts, per Constitution Section 48's Versioning Policy (already Accepted) applied here specifically. |
| Configurable within safe limits | The *floor* (dedicated Role, never general Staff) is not configurable; everything above the floor is. This "safe limits" boundary is itself a Constitution-level concern for the future SAD, not fully specified by Discovery. |

### Open Question Raised

The exact axis values (which Organization Types require dual sign-off,
which Analysis Types count as "Critical," Egypt-specific verification
requirements) are **entirely Open** — this model specifies the *shape* of
the policy engine, not its content. Logged to `open-questions.md`.

## Broader Rule Catalog (24 categories, representative rules per category)

| Rule ID | Category | Domain Owner | Trigger → Outcome | Config Scope | Audit Req | Risk | Evidence |
|---|---|---|---|---|---|---|---|
| BR-E01 | Eligibility | Order Management | Patient/order meets test prerequisites → order accepted | Per test type | Standard | Low | Inferred |
| BR-V01 | Verification | Test Processing | See Result Verification Policy Model above | Per org/analysis/branch/country | **Elevated (Sensitive Op)** | High | Inferred (shape), Evidenced (floor) |
| BR-A01 | Approval | Procurement | PO above threshold → requires manager approval | Per org, threshold configurable | Standard | Medium | Inferred |
| BR-P01 | Pricing | Financial | Test priced per org's active price list/contract | Per org/contract | Standard | Medium | Inferred |
| BR-D01 | Discount | Financial | Discount applied within role-authorized limit | Per role, limit configurable | Standard | Medium | Inferred |
| BR-R01 | Refund | Financial | Refund requires distinct approval from original payment recorder | Per org | **Elevated** (financial-fraud-adjacent, Wave 12) | Medium-High | Inferred |
| BR-PAY01 | Payment | Financial | Payment recorded only against a valid open Invoice | Fixed | Standard | Low | Evidenced (Baseline) |
| BR-I01 | Insurance | Insurance and Corporate Contracts | Claim submitted only after eligibility confirmed | Per payer contract | Standard | Medium | Evidenced (Baseline, weak) |
| BR-PR01 | Procurement | Supply Chain | PO requires Supplier Evaluation on file | Per org | Standard | Low | Inferred |
| BR-PY01 | Payroll | Workforce | Payroll disbursement requires **dual-control approval** | Fixed floor, org-configurable additions | **Elevated (Sensitive Op)** | High | Inferred |
| BR-L01 | Leave | Workforce | Leave approved only within remaining balance, unless override | Per org policy | Standard | Low | Inferred |
| BR-INV01 | Inventory | Supply Chain | Stock adjustment requires reason code | Fixed | Standard | Medium | Inferred |
| BR-EX01 | Expiry | Supply Chain | Expired lot blocked from consumption automatically | Fixed (safety floor), non-configurable | **Elevated** (patient-safety-adjacent) | High | Inferred |
| BR-Q01 | Quality | Quality Management | Non-conformance auto-creates a candidate CAPA | Per org | Standard | Medium | Inferred |
| BR-CR01 | Critical Result | Test Processing | Critical result triggers immediate escalation notification | Fixed floor, timing configurable | **Elevated (Sensitive Op)** | **Highest** | Inferred |
| BR-ESC01 | Escalation | Cross-cutting | Unresolved Sensitive Operation escalates after configurable window | Per org/branch | Standard | Medium-High | Inferred |
| BR-N01 | Notification | Notification and Communication | Notification content filtered by Data Scope/Consent before send | Fixed (Constitution Section 26) | Standard | Medium | Evidenced (Baseline, Accepted rule) |
| BR-C01 | Consent | Governance | Access to consent-gated data requires an active, unrevoked grant | Fixed (Constitution Section 22) | **Elevated** | High | Evidenced (Accepted) |
| BR-DA01 | Data Access | Governance | Every read of Sensitive data is Data-Scope-checked server-side | Fixed (Constitution Section 21) | **Elevated** | High | Evidenced (Accepted) |
| BR-BG01 | Break-Glass | Governance | Emergency access is time-limited, justified, fully audited | Fixed (Constitution Section 21) | **Elevated** | **Highest** | Evidenced (Accepted) |
| BR-AI01 | AI Governance | AI Operations | AI request checked against Forbidden-list before execution | Fixed (Constitution Section 28) | **Elevated** | High | Evidenced (Baseline Phase 10) |
| BR-T01 | Tenant Configuration | Tenant and Organization Management | Tenant-level config changes to authorization-relevant settings are audited | Fixed (Constitution Section 48, Configuration Management) | **Elevated** | Medium-High | Evidenced (Accepted) |
| BR-S01 | Subscription | SaaS Commercial | Feature access blocked if subscription lapses, with configurable grace period | Per plan | Standard | Low | Inferred |
| BR-U01 | Usage | SaaS Commercial | Usage metering event recorded per billable platform action | Per plan | Standard | Low | Inferred |
| BR-FE01 | Feature Entitlement | SaaS Commercial | Feature availability resolved from tenant's active plan + flags | Fixed (Constitution Section 48) | Standard | Low | Evidenced (Accepted pattern) |

## Cross-Cutting Finding: A Second Tier of "Elevated" Rules Beyond Sensitive Operations

Constitution Section 21 defines Sensitive Operations narrowly (verified
medical results, consent, cross-tenant admin). This Wave's catalog surfaces
several rules (Refund, Expiry-block, Break-Glass, AI Forbidden-list check,
Tenant Configuration) that are not literally "Sensitive Operations" under
that definition but clearly warrant elevated audit treatment. **Recommended
(not Confirmed):** the future SAD/Constitution work should consider whether
a second, broader "Elevated Audit" tier is warranted alongside the
existing Sensitive Operation tier — flagged for Wave 12/13, not decided
here.

## Summary

**26 representative rules** across all 24 requested categories (2 categories
— Verification and Payroll — received deeper treatment given their
Sensitive-Operation weight). Combined with the Baseline's existing rule
catalog (`07-business-rules-catalog.md`), the platform now has a
documented rule shape for both its original Laboratory-Operations core and
its newly-scoped enterprise domains.
