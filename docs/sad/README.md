# Software Architecture Document (SAD) — Index

**Document Status:** Review (this README) — see Section 12 of Wave 1 for
the full governance rule this status follows.

## What this is

This is the Software Architecture Document for the digital healthcare
platform (`darhous/test-m3ml`), authorized to begin authoring on
2026-07-18 (`docs/certification/26-FINAL-SEMANTIC-CONSISTENCY-CLOSURE.md`,
verdict: **CLEAN SEMANTIC BASELINE — READY FOR SOFTWARE ARCHITECTURE
DOCUMENT**).

Per `docs/constitution/PROJECT-CONSTITUTION.md` §1: the SAD is **not**
the Constitution and does not restate or reinterpret its governing
rules. The SAD describes *how* the platform is built to satisfy those
rules — it is authored strictly downstream of the Constitution, the 14
Accepted ADRs (`docs/adr/`), the frozen Technology Baseline
(`docs/architecture-review/02-TECHNOLOGY-BASELINE.md`), the Unified
Decision Register (`docs/certification/10-DECISION-REGISTER.md`), the
Unified Risk Register (`docs/certification/11-RISK-REGISTER.md`), and
the API Platform Strategy (`docs/api-platform/`).

## Approved Wave Structure

Adopted 2026-07-20, superseding the 11-wave scaffold originally proposed
during the pre-SAD workstation audit. This structure is now the official
plan for authoring the SAD and is not to be renegotiated unless a real
architectural conflict is discovered during execution.

| Wave | Title | Status |
|---|---|---|
| 1 | Introduction, Goals, Constraints & Stakeholders | **Review** — drafted and self-reviewed 2026-07-20 (verdict: PASS, see §15 of the Wave 1 document); awaiting project owner Accepted review |
| 2 | Context & Scope | Not started |
| 3 | Solution Strategy | Not started |
| 4 | Building Block View | Not started |
| 5 | Runtime View | Not started |
| 6 | Deployment View | Not started |
| 7 | Security, Privacy & Trust Boundaries | Not started |
| 8 | Multi-Tenancy, Identity & Access Governance | Not started |
| 9 | AI Governance, Device Integration & Other Cross-Cutting Concerns | Not started |
| 10 | Architecture Decisions & Traceability | Not started |
| 11 | Quality Requirements & Quality Scenarios | Not started |
| 12 | Risks, Technical Debt & Evolution | Not started |
| 13 | Glossary, Consistency Review & Final Close-out | Not started |

Each wave is authored, reviewed, and committed independently, in order.
No wave begins before the previous one is committed.

## Files

| File | Wave | Content |
|---|---|---|
| `01-introduction-goals-constraints-stakeholders.md` | 1 | Purpose, objectives, audience, goals, stakeholders, constraints, assumptions, out-of-scope, governance |

## Traceability

- Validated inputs this document set inherits as fixed:
  `docs/certification/15-SAD-INPUT-PACKAGE.md`
- Section-by-section input readiness: `docs/certification/23-SAD-READINESS-MATRIX.md`
- Full decision history: `docs/certification/10-DECISION-REGISTER.md`
- Full risk history: `docs/certification/11-RISK-REGISTER.md`
