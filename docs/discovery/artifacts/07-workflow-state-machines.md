# Workflow State Machines (Discovery, Phase 07)

**Status: Draft — Assumption-Driven Autonomous Run.** Formalizes the state
transitions implied by Phase 05/06 Aggregates and this phase's invariants.
See `docs/discovery/diagrams/07-state-machines.md` for the visual diagrams.

## TestOrder

States: `Requested → Collected → Completed`; `Requested → Cancelled`;
`Requested → Expired`.
**Authorization per transition:** `Requested`: Doctor or Patient (per
Order Management). `Cancelled`: Patient or ordering Doctor before
collection (exact authority split Open). `Expired`: System (automatic,
per proposed expiry rule, window Open).

## Specimen

States: `Collected → [Transported] → Accessioned → QualityChecked →
{Accepted | Rejected}`.
**Authorization per transition:** `Collected`/`Transported`: Sample
Collector or Laboratory Staff. `Accessioned`/`QualityChecked`: Laboratory
Staff. `Rejected`: Laboratory Staff (reason code required, per invariant).

## TestResult — highest-scrutiny state machine

States: `Processing → Captured → Verified → Released`; `Processing →
Failed` (proposed, resolves H2); `Released → Corrected` (new fact, does
not mutate `Released`).
**Authorization per transition:** `Processing`/`Captured`: Laboratory
Staff / Device (via Device Integration Gateway). `Verified`: **Result
Verifier Role only** (Sensitive Operation — elevated authorization +
Audit Event, Constitution Section 21/23). `Released`: System, gated on
`Verified` (Sensitive Operation). `Corrected`: Result Verifier Role only
(Sensitive Operation).

## Claim

States: `Submitted → Adjudicated → {Approved | Denied} → Settled`
(`Denied` is a proposed addition, resolves H9).
**Authorization per transition:** `Submitted`: Finance Staff.
`Adjudicated`/`Approved`/`Denied`: external Payer system (not an internal
actor — the platform receives, does not decide, this transition).
`Settled`: Finance Staff or automated reconciliation (Open).

## Cross-Cutting Rule Applied to All Four State Machines

No state machine here permits a transition with no named authorizing
actor — every transition above states who (or what system/external party)
may perform it, consistent with Constitution Section 25 (Workflow and
State Transition Rules: "the rule/actor that authorizes each transition").
Where the *exact* eligibility detail is unknown (e.g., Result Verifier Role
criteria), the *rule shape* (a gate exists) is still fixed, and only the
detail is Open — no transition is left ungated by default-allow, consistent
with Constitution Section 21's Deny by Default principle.
