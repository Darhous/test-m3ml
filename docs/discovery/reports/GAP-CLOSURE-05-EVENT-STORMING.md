# Gap Closure Wave 5 — Event Storming Gap Closure

**Skills used:** `domain-driven-design` (Domain Events framework, applied
to 10 new clusters; explicit Domain-vs-Integration-Event discipline
maintained per Constitution Section 12).

## Executive Summary

Storm-walked the 29 previously-missing/shallow domains into 10 clusters,
producing ~84 new Domain Events (plus 2 timer events), bringing the
platform's total Domain Event catalog to ~114 across 18 clusters/contexts.
Explicitly modeled Patient and Doctor as owned domains with their own
lifecycle events for the first time (Cluster G), directly addressing
Baseline Risk #7.

## Findings

- Cluster C (Workforce) surfaced the platform's second Sensitive-Operation-
  grade rule (Payroll dual-control approval), mirroring the Result Verifier
  Role pattern from Baseline Phase 07 — the same governance shape recurring
  in a completely different domain is a positive DDD-consistency signal,
  not a coincidence forced to fit.
- Cluster E (Complaints) and Cluster D (CAPA) have an undesigned
  relationship — flagged, not resolved, consistent with this program's own
  discipline against silent resolution.
- A diagram was deliberately **not** produced for this Wave — an
  84-event storming board diagram would be unreadable and decorative; the
  structured tables are the genuinely useful artifact here, same reasoning
  Wave 3 applied to its capability map.

## Decisions

None (raw event material, pre-decision, matching the Baseline's own Phase
03 "ADR Impact: None" precedent).

## Open Questions

6 new policy-shape gaps identified inline (reorder-point trigger, credential
-expiry lead time, CAPA closure window, complaint-to-CAPA relationship,
appointment no-show policy, corporate-rate pricing) — carried to Wave 6
for rule-shape treatment, consistent with how the Baseline's Phase 03 → 07
handoff worked.

## Risks

Payroll dual-control requirement not yet enforced anywhere (it's a Domain
Event pattern, not yet a Business Rule) — carried to Wave 6/12.

## Assumptions

All ~84 events are `Inferred — Industry Reference`, consolidated at Wave
13.

## Files Updated

- `docs/discovery/artifacts/W5-event-storming-gap-closure.md` (created)

## Review Checklist

- [x] All 29 domains from the user's list covered (grouped into 10
      clusters where naturally related, per the same clustering logic
      Wave 3 used for capabilities).
- [x] No Domain Event mixed with an Integration Event — explicit
      discipline check included.
- [x] Unified naming convention applied (past tense, no CRUD names) —
      spot-checked across all 84 new events, no violation found.
- [x] Every event traces to a specific cluster/domain — no orphan events.
