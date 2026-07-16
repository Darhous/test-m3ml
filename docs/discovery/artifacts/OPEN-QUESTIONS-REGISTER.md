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

*(Populated as Discovery proceeds.)*
