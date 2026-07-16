# Gap Closure Wave 2 — Stakeholders, Actors, and Personas Expansion

**Skills used:** `doc-coauthoring` (organizing 39 personas for readability
by category), `domain-driven-design` (Data Scope reasoning per persona,
feeding Wave 9's Bounded Context ownership work).

## Executive Summary

Expanded from 15 stakeholder categories / 4 detailed personas to 39 named
personas across 8 categories (Clinical/Care, Laboratory, Front-Office/
Support, Financial, Workforce, Supply Chain, Commercial/External,
Technical/Platform, Governance/Oversight, Commercial Operations). Every
persona has Goals, Pain Points, Data Scope, High-Risk Actions, and a
Primary KPI. Resolved 2 non-persona entries in the user's list ("Clinics,"
"Hospitals" are organization types) by representing their actual human
actors (Clinic Administrator, Hospital Administrator/Medical Director)
rather than dropping them.

## Findings

- The Platform Operator and Support Operations personas share a real,
  unresolved tension: cross-tenant visibility need vs. tenant isolation —
  flagged for Wave 12's security review, not resolved here (this is a
  genuine architectural question, not a Discovery-level judgment call).
- Payroll Staff's Data Scope note ("among the most sensitive non-clinical
  data in the platform") is a new, load-bearing finding — no prior
  Discovery content addressed payroll privacy at all.
- AI Operations is an entirely new persona category — the Baseline
  Discovery's AI use-case catalog (Phase 10) never asked "who operates and
  monitors the AI Gateway itself," only "who benefits from AI suggestions."

## Decisions

None (persona identification, not architectural decision).

## Open Questions

- Regulator persona's actual interaction model with the platform (if any)
  is undesigned — logged as a new gap, not resolved.

## Risks

- Platform Operator / Support Operations cross-tenant-visibility-vs-
  isolation tension — logged for `RISK-REGISTER.md` consolidation in
  Wave 12 (not duplicated here to avoid the exact kind of count drift Wave
  0 just fixed).

## Assumptions

All persona Goals/Pain Points/KPIs are `Inferred — Industry Reference`,
consistent with the Baseline Discovery's existing Assumption Register
discipline — logged for consolidation into `ASSUMPTION-REGISTER.md` at
Wave 13's validation pass rather than duplicated per-Wave.

## Files Updated

- `.claude/context/stakeholders.md` (Wave 2 summary section appended,
  original 15 categories preserved unchanged)
- `docs/discovery/artifacts/W2-persona-catalog.md` (created)

## Review Checklist

- [x] All ~39 named roles from the user's list represented (2 org-type
      entries correctly resolved to their human actors, not dropped).
- [x] Every persona has Goals/Pain Points/Data Scope/High-Risk
      Actions/KPI.
- [x] `stakeholders.md` history preserved.
- [x] No persona asserts a capability contradicting Backend-Enforced
      Authorization (Constitution Section 21) — spot-checked Platform
      Operator and Auditor specifically, given their elevated access.
