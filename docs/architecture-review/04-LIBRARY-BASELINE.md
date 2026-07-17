# Library Baseline — Detailed Validation

Every Library from `02-TECHNOLOGY-BASELINE.md` Section B, confirmed
Approved / Rejected / Replace.

| Library | Decision | Rationale (re-verified, not re-derived) | Replace? |
|---|---|---|---|
| pgvector | **APPROVED** | Reuses the platform's own already-adopted PostgreSQL; no dedicated vector-DB service justified absent a measured scale trigger (`ai-operations-gateway/semantic-search/08-build-vs-buy.md`). Clean PostgreSQL-License terms. | No — Qdrant/Weaviate remain logged as scale-triggered upgrade candidates, not replacements for a deficiency. |
| Prophet | **APPROVED** | MIT, mature, appropriate for moderate/messy time-series data; correctly logged as lower-priority given Wave 3/10's "speculative" classification of forecasting generally (`analytics/forecasting-engine/08-build-vs-buy.md`). | No. |
| FullCalendar | **APPROVED** | MIT core, decade-mature calendar-rendering component, correctly scoped as UI-rendering only (distinct from Cal.com's booking-logic Engine) (`scheduling-and-encounters/resource-calendar/05-architecture-review.md`). | No — flag: avoid premium plugins (separately licensed) without a fresh license check. |
| ZXing (or equivalent) | **APPROVED, conditionally** | The reuse program explicitly disclosed this was **not freshly re-searched** — a general-knowledge-based placeholder for "a mature, standard barcode-decode library," reused across 2 Modules (Specimen Operations, Inventory) without re-verification the 2nd time (`inventory/barcode-scanning/03-candidate-repositories.md`). This Board does not reject it — the category (mature OSS barcode libraries, Apache-2.0-class licensing) is not in genuine doubt — but formally requires the specific library and its license be **re-confirmed at implementation time**, not carried forward as if independently verified. | Conditional — re-verify before Module implementation, not a rejection. |

## Board Findings

- **4 of 4 Libraries ratified.** 3 with no reservation; 1 (ZXing)
  ratified with an explicit re-verification condition inherited
  directly from the reuse program's own honesty disclosure — this Board
  is not upgrading that disclosure's confidence level by omission.
- **No Library requires replacement.** No Library decision conflicts
  with an Engine decision (e.g., FullCalendar's UI-rendering scope does
  not overlap Cal.com's booking-Engine scope — re-confirmed against
  `MASTER_DEPENDENCY_MATRIX.md`, no duplicate flagged there).
- Libraries are, by design, the smallest category in this Baseline — the
  reuse program's own `MASTER_LIBRARY_CATALOG.md` closing note observed
  that most needs resolved to a full Engine rather than a linked-in
  Library. This Board finds that pattern architecturally sound, not a
  gap: a Library dependency carries less operational surface than an
  Engine, and the program's heavy Engine-reuse reflects genuine
  capability breadth in the candidates found, not under-investigation of
  the Library category.
