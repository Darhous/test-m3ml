# Technology Baseline — Decision Freeze

**Effective:** Upon commit of this document to `main`.
**Authority:** Enterprise Architecture Review Board (EARB), acting on
the completed Global Enterprise Build-vs-Buy & Reuse Intelligence
Program (`docs/reuse/`).
**Frozen Artifact:** `02-TECHNOLOGY-BASELINE.md` (30 entries: 21
Engines, 4 Libraries, 5 Reference Standards), together with
`03-ENGINE-BASELINE.md`, `04-LIBRARY-BASELINE.md`, `05-SDK-BASELINE.md`,
`06-FORK-BASELINE.md` as its detailed supporting record.

## What "Frozen" Means

1. **Every entry in `02-TECHNOLOGY-BASELINE.md` is the mandatory
   default** for API Platform Strategy, the Software Architecture
   Document, Core Platform, SDK, and Module development. A team building
   against a Module this Baseline covers uses the listed technology, not
   an independently-chosen alternative, without going through the
   Amendment process below.
2. **"Frozen" does not mean "immutable forever."** It means: the next
   consumer of this Baseline (API Strategy, SAD) inherits it as settled
   input, not as an open question to re-litigate. Change happens through
   the Amendment Process, not through silent drift.
3. **Two entries are frozen in a CONDITIONAL state, not a full-confidence
   state** — Eramba Community (`compliance-tracking`) and Mirth Connect
   4.5.2 (`hl7-integration-engine`/`astm-integration`). Freezing them
   conditionally is itself the frozen decision: downstream consumers must
   carry the flagged risk forward (`11-RISKS.md` R-01, R-02), not treat
   silence as resolution.
4. **One Feature is explicitly NOT frozen**: `home-collection-logistics`
   (Specimen Operations) remains genuinely undecided, blocked on Open
   Question #6. There is no Baseline entry for it to freeze.

## Amendment Process

A Technology Baseline entry may be changed only by one of:

1. **A new ADR**, following Constitution Section 39's existing ADR
   discipline — required for any change to a Platform Kernel or
   Core-Domain-adjacent Engine (Keycloak, OPA, immudb, or any Engine
   whose Feature carries a `REFERENCE (FHIR...) + BUILD` decision).
2. **A subsequent EARB review cycle**, per each entry's own `Review
   Cycle` field (Annual or Semi-Annual) in `02-TECHNOLOGY-BASELINE.md`,
   or triggered early by a Revisit Trigger event (a security incident, a
   license change by the upstream vendor, a maintenance-abandonment
   signal).
3. **Formal legal counsel findings** from the AGPL/unconfirmed-license
   review (`08-AGPL-LEGAL-CHECKLIST.md`) — if legal review blocks an
   Engine, its Baseline entry moves to REJECTED and the documented
   fallback candidate (already named in `02-TECHNOLOGY-BASELINE.md`'s
   "Replacement Candidate" column) becomes the subject of a fresh,
   focused Build-vs-Buy micro-assessment — not a full program re-run.

**No Baseline entry may be changed by an individual Module team's
unilateral choice, however well-justified it seems in the moment** — the
entire point of a frozen baseline is that the same license/maintenance/
security due diligence is not re-litigated Module-by-Module.

**Update (2026-07-18, Pre-SAD Baseline Correction):** this Amendment
Process's path 2 (a subsequent EARB review cycle) was formally invoked
to *extend* — not change — the Baseline: 3 new Engines (Kong Gateway,
OpenBao, PostgreSQL) were added, closing the previously-Open API
Gateway, Secrets/Vault, and relational-database decisions. This
document's own 30-entry/21-Engine count is preserved as the accurate
record of the original EARB freeze; the current count (33 entries, 24
Engines) is in `docs/architecture-review/02-TECHNOLOGY-BASELINE.md` and
`docs/certification/22-ARCHITECTURE-BASELINE-FREEZE.md`.

## Freeze Contents Cross-Reference

| Document | Role in the Freeze |
|---|---|
| `02-TECHNOLOGY-BASELINE.md` | The frozen table itself |
| `03-ENGINE-BASELINE.md` | Per-Engine 10-point validation backing the freeze |
| `04-LIBRARY-BASELINE.md` | Per-Library validation |
| `05-SDK-BASELINE.md` | Confirms zero SDKs frozen (not an omission) |
| `06-FORK-BASELINE.md` | Confirms zero Controlled Forks frozen (not an omission) |
| `07-LICENSE-REVIEW.md` | License-family legal grounding for the freeze |
| `08-AGPL-LEGAL-CHECKLIST.md` | The 7 items whose freeze is conditional on future legal review |
| `09-OPEN-QUESTIONS.md` | What is explicitly NOT frozen, and why |
| `10-ADR-REVIEW.md` | Governance dependency: the freeze's Core-Domain-preservation logic depends on ADR-0011 remaining in its current or a materially similar form |
| `11-RISKS.md` | 8 risks carried forward with the freeze, not resolved by it |

## Board Attestation

This Board attests that:

- Every ratified technology was independently checked against the
  10-point validation checklist (architectural fit, domain boundaries,
  license compatibility, maintainability, upgrade path, security,
  maturity, community health, ecosystem stability, long-term ownership).
- No decision was reversed without documented cause.
- No new repository research was performed to reach this freeze — it is
  a ratification of `docs/reuse/`'s existing evidence, not a new
  assessment.
- All AGPL and unconfirmed-license findings are carried forward with
  their full urgency, not softened.
- ADR-0011's Proposed (not Accepted) status is preserved accurately.

**The Technology Baseline is FROZEN as of this commit.**
