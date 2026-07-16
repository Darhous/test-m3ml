# Gap Closure Wave 8 — Ubiquitous Language Expansion

**Skills used:** `domain-driven-design` (Ubiquitous Language discipline —
the core purpose of this Wave is preventing the exact same-word-different-
context failure the skill's own "Common Mistakes" table warns against).

## Executive Summary

Disambiguated all 37 conflict-prone terms the user named. Each term is
pinned to its owning Bounded Context(s), with explicit Forbidden Synonym
notes. 6 terms rejected as standalone canonical terms in favor of a
designated replacement (Booking→Appointment, Sample→Specimen,
Publication→Release, Facility→Organization/Branch,
Subscriber-for-a-person→Patient/Tenant, bare Customer→Patient/Tenant).

## Findings

- "Report" and "Collection" both genuinely need two meanings retained
  (not collapsed to one) — the discipline here is *mandatory qualification*
  ("Clinical Report" vs. "BI Report"), not elimination.
- One real domain gap surfaced: "Department" (a finer unit than Branch,
  relevant once Hospital customer types are modeled in depth) — not
  resolved, logged as a gap.
- One Discovery-level naming decision is flagged but not yet exercised by
  any real event: Batch (processing) vs. Lot (supply) — worth confirming
  before either term is used in a future SAD.

## Decisions

None (terminology discipline, not architectural decision).

## Open Questions

None new — the "Department" gap and "Batch vs. Lot" flag are logged
inline in the artifact table rather than duplicated as numbered Open
Questions, since neither blocks any other Wave.

## Risks

None new.

## Assumptions

None — this Wave is a naming-discipline exercise applied to already-
established (Evidenced or Inferred) concepts, not new factual content.

## Files Updated

- `docs/discovery/artifacts/W8-ubiquitous-language-expansion.md` (created)
- `.claude/context/glossary.md` (Wave 8 pointer appended, existing Draft
  terms preserved)

## Review Checklist

- [x] All 37 user-named terms addressed.
- [x] Every term pinned to an owning Bounded Context.
- [x] Forbidden synonyms explicitly listed, not just implied.
- [x] No term collapses two genuinely distinct meanings into one without
      a qualification rule (Report, Collection specifically checked).
