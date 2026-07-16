# Gap Closure Wave 10 — Candidate Modules and Platform Services

**Skills used:** `domain-driven-design` (modules strictly derived from
Wave 9's Bounded Context ownership, per Constitution Section 8),
`architecture-patterns` (Domain Core/Platform Kernel/Shared Infrastructure/
Cross-Cutting/Business Module layering).

## Executive Summary

Derived 28 candidate modules from Wave 9's 28 Bounded Contexts (1:1, no
module invented independently of a context). Classified into Core
Platform Services (3), Independent Gateways (3), Shared Technical Services
(2), Business Modules (19), and Commercial Modules (1). Explicitly flagged
Accounting as the most extraction-ready module by default, given Wave 3's
already-Recommended Integration-leaning posture for Financial depth.

## Findings

- Every module's Extraction Trigger is stated per Constitution Section 55
  (evidence-based, no invented thresholds) — Accounting is the one
  exception with a *qualitatively* different trigger type (regulatory/
  compliance-driven rather than scaling-driven for Payroll, product-
  decision-driven for Accounting) rather than a numeric one, consistent
  with the rest of this program's discipline against inventing numbers.
- Result Verification and Reporting is explicitly the module *least*
  likely to be extracted, not most — a direct, correct consequence of
  Core Domain status (deepest investment stays in the Monolith longest,
  per ADR 0001's own reasoning), worth stating explicitly since "Core"
  could otherwise be misread as "extract first."

## Decisions

None (module candidates, not Accepted architecture).

## Open Questions

Tenant-specific extension mechanism and Market-specific module need both
explicitly deferred (to the SAD and Wave 11 respectively) rather than
guessed.

## Risks

None new.

## Assumptions

All Business/Commercial Module Evidence Status inherits directly from
Wave 9's per-context Evidence status — no new assumption layer introduced.

## Files Updated

- `docs/discovery/artifacts/W10-candidate-modules-platform-services.md`
  (created)

## Review Checklist

- [x] Every module traces to exactly one Wave 9 Bounded Context.
- [x] Modules derived from Contexts, not the reverse (per explicit user
      instruction).
- [x] Domain Core / Platform Kernel / Shared Infrastructure / Cross-
      Cutting / Business Module distinction explicit, not blended.
- [x] Every module has a stated Extraction Trigger consistent with
      Constitution Section 55 (no invented numeric thresholds).
