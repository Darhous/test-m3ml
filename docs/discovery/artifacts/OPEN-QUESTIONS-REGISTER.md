# Discovery Open Questions Register

**Purpose:** a Discovery-scoped working register of open questions,
cross-referencing `.claude/context/open-questions.md` (the project's
canonical, longer-lived register) but tracking Discovery-specific status
(which phase raised it, whether it blocks a later phase) that the
Context Store file does not track. Every item here that survives to
Playbook 12 is reconciled into `.claude/context/open-questions.md` per
that file's own append-only update rule — nothing is answered here by
assumption; genuine answers only come from the user.

| # | Question | Raised By Phase | Blocks | Status | Cross-ref |
|---|---|---|---|---|---|
| 1 | Insurance/billing model (direct billing vs. reimbursement vs. capitation) | 02 | Detailed VS4 modeling in Phase 07 (Business Rules) | Open | `.claude/context/open-questions.md` #17 |
| 2 | Whether hospitals/clinics are in scope for the first real build | (pre-existing, reaffirmed) | Capability Map scope (Phase 02), Subdomain scope (Phase 04) | Open | `.claude/context/open-questions.md` #9 |
| 3 | Offline Mode requirement for field/home-visit collection | (pre-existing, reaffirmed by VS2) | Field-collector workflow detail (Phase 07) | Open | `.claude/context/open-questions.md` #6 |
| 4 | Who is authorized to perform `ResultVerified` (Pathologist vs. senior Lab Technician, likely varies by test type) | 03 (Hotspot H1) | Business Rules (Phase 07), Authorization design | Open | new — no prior cross-ref |
| 5 | Missing event: equipment/processing failure mid-run (H2) | 03 | Business Rules (Phase 07), Integrations (Phase 08) | Open | new |
| 6 | Missing event: failed home visit / no-show (H4) | 03 | Business Rules (Phase 07) | Open | new |
| 7 | Missing event: chain-of-custody handoff during transport (H5) | 03 | Business Rules (Phase 07), Device/Integration design (Phase 08) | Open | new |
| 8 | Escalation policy for repeated specimen rejections (H7) | 03 | Business Rules (Phase 07) | Open | new |
| 9 | Missing event: claim denial/rejection (H9) | 03 | Business Rules (Phase 07) | Open | new |
| 10 | Missing event: post-release result correction (`ResultCorrected`) | 05 | Business Rules (Phase 07) | Open | new — related to Constitution Section 12's own illustrative example |
| 11 | Chain-of-custody record detail (`ChainOfCustodyRecord` Value Object shape) still undesigned | 05 | Business Rules (Phase 07), Integrations (Phase 08) | Open — deferred to Phase 08 | relates to H5 |
| 12 | Order expiry window duration | 07 | Phase 12 finalization | Open | `.claude/context/open-questions.md` #18 |
| 13 | Result Verifier Role eligibility criteria (HIGH PRIORITY — clinical safety) | 07 | Phase 09/11/12 | Open | `.claude/context/open-questions.md` #19 |
| 14 | Repeated-rejection escalation threshold N | 07 | Phase 12 finalization | Open | `.claude/context/open-questions.md` #20 |
| 15 | Processing/equipment failure recovery policy | 07 | Phase 08 (Integrations, device failure handling) | Open | `.claude/context/open-questions.md` #21 |
| 16 | Home-visit failure retry policy | 07 | Phase 08 | Open | `.claude/context/open-questions.md` #22 |
| 17 | Core Domain identity — re-evaluated against 6 alternatives; Recommended (not decided) reframe to "Patient-to-Result Orchestration" | Gap Closure Wave 7 | ADR-0011 disposition (Wave 14) | Open | `.claude/context/open-questions.md` #14 |
| 18 | Shared-tier partitioning technical detail (tenant-identifier column vs. schema-per-tenant) | 09 (reaffirmed as SEC-04, Gap Closure Wave 12) | Wave 14 escalation note / future Software Architecture Document | Open | `.claude/context/open-questions.md` #15 |
| 19 | Tenant promotion-path trigger type (shared tier → dedicated tier) | 09 | Future Software Architecture Document | Open | `.claude/context/open-questions.md` #16 |
| 20 | Configurable Result Verification Policy Model's actual axis values (org type, analysis type, risk, specialty, approval level, branch/country policy) | Gap Closure Wave 6 | **Highest priority** — directly compounds item #13 above | Open | `.claude/context/open-questions.md` #23 |
| 21 | Whether a second, broader "Elevated Audit" tier is required (Refund, Expiry-block, Break-Glass, Tenant Configuration) | Gap Closure Wave 6 | Wave 14 governance disposition | Open | `.claude/context/open-questions.md` #24 |
| 22 | PDPL 151/2020 cross-border data transfer provisions — not deeply reviewed this round | Gap Closure Wave 11 | `Requires Legal Verification` — future dedicated legal research pass | Open | `.claude/context/open-questions.md` #25 |
| 23 | Egyptian Labor Law / Social Insurance requirements affecting Payroll — not researched this round (explicit research gap, not an assumption) | Gap Closure Wave 11 | `Requires Legal Verification` — future dedicated legal research pass | Open | `.claude/context/open-questions.md` #26 |
| 24 | Whether National ID should be a mandatory Patient Management field | Gap Closure Wave 11 | Requires research into Egyptian health-identity linkage practice | Open | `.claude/context/open-questions.md` #27 |

**Items #1–13 not otherwise reconciled above:** cross-checked against
`.claude/context/open-questions.md` items #1–13 (target markets beyond
Egypt-first scoping, legal requirements broadly, hosting model, usage
scale, device types, currencies/languages, legacy systems). None were
specifically raised or advanced by a Gap Closure Wave — Wave 1 scoped
Egypt as first market (Confirmed by the user, not answering the broader
context #1), and Wave 11 researched 4 specific regulatory topics (not the
whole of context #2). No row is fabricated here for them; they remain
Open exactly as the canonical Context Store file already states, and
hosting model (context #3) is explicitly out of this program's scope
(Strict Prohibitions — no Technology/Cloud Selection).

*(Populated as Discovery proceeds. Reconciled against
`.claude/context/open-questions.md` at Gap Closure Wave 13 — Discovery-
local register now covers 24 items; canonical Context Store file remains
the authoritative 27-item source, cross-referenced above rather than
duplicated in full.)*
