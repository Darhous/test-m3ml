# Gap Closure Wave 3 — Enterprise Capability Map

**Skills used:** `domain-driven-design` (Strategic classification per
capability — Core/Supporting/Generic/Platform/Commercial/Operational/
Compliance test applied to all 100), `doc-coauthoring` (structuring 100
capabilities across 10 categories for usability).

## Executive Summary

Rebuilt the Capability Map from the Baseline's 20 (Laboratory-only) to 100
across 10 categories spanning the full Confirmed Business Scope (Wave 1).
Every capability has a Strategic Classification, a Candidate Bounded
Context, and an Evidence Level (Evidenced / Confirmed-scope-Inferred-detail
/ Inferred). Explicitly drew the Native/Integration/Deferred boundary for
Financial capabilities per the user's explicit "don't assume a full
financial ERP" instruction, rather than silently defaulting either way.

## Findings

- Evidence distribution is itself a finding: Governance (8/8 mostly
  Evidenced, inherited from the already-Accepted Constitution) is the
  strongest-evidenced category; Supply Chain and Customer Operations (0/10
  and 0/9 Evidenced respectively) are the weakest — a precise map of where
  future real-stakeholder input matters most.
- Payroll's separation from general Workforce Management (proposed, not
  decided) is the single most consequential judgment call in this Wave —
  driven by Wave 2's data-sensitivity finding, not arbitrary.
- "Calibration" and "Reporting" each appear meaningfully twice
  (Laboratory-instrument Calibration vs. general Asset Calibration;
  Clinical Reporting vs. enterprise BI Reporting) — flagged explicitly to
  prevent Wave 8 (Ubiquitous Language) from silently conflating them.

## Decisions

None (capability classification, not architectural decision — Candidate
Bounded Contexts here are inputs to Wave 9, not commitments).

## Open Questions

- Whether Payroll should be its own Bounded Context or a slice of
  Workforce Management — carried to Wave 9's Decision Matrix.
- Whether "Reporting" (BI) needs disambiguation from "Reporting" (clinical)
  at the Ubiquitous Language level — carried to Wave 8.

## Risks

None new this Wave (capability mapping is lower-risk than rule/security
work) — existing Risk Register entries remain the operative set.

## Assumptions

Every `Inferred` and `Confirmed-scope/Inferred-detail` capability entry
(84 of 100) is a logged assumption by construction — consolidated into
`ASSUMPTION-REGISTER.md` at Wave 13 rather than duplicated per-row here
(100 individual register rows would make the register unusable).

## Files Updated

- `docs/discovery/artifacts/W3-enterprise-capability-map.md` (created)
- `docs/discovery/diagrams/W3-capability-map-categories.md` (created)
- `.claude/context/module-catalog.md` (Wave 3 pointer appended, existing
  8-context table preserved)

## Review Checklist

- [x] All 10 required categories covered, minimum capability lists per
      category met or exceeded.
- [x] Every capability has Strategic Classification, Candidate Context,
      Evidence Level.
- [x] Financial Native/Integration/Deferred boundary explicitly drawn,
      labeled Recommended not Confirmed.
- [x] No capability silently assumes a full financial ERP.
- [x] Terminology collisions (Calibration, Reporting) flagged for Wave 8,
      not silently resolved here.
