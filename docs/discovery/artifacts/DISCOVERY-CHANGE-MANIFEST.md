# Discovery Change Manifest

**Purpose:** the single running ledger of every file created, expanded,
rewritten, superseded, or deleted across the Discovery Gap Closure &
Healthcare Operations Platform Expansion program. Updated after every
Wave, append-only (never overwritten — a later Wave's changes are new
rows, not edits to earlier rows).

**Column meanings:**
- **Disposition:** Created / Expanded / Rewritten / Superseded / Deleted.
- **Replacement:** for Superseded/Deleted entries, where the knowledge now
  lives.
- **Commit:** the git commit hash that made the change (filled after each
  Wave's commit).

## Wave 0 — Baseline Audit and Repair

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/reports/12-discovery-completion-report.md` | Expanded (inline correction) | Risk count miscounted (14 → 13) | N/A — same file, corrected | *(this Wave's commit)* |
| `docs/discovery/DISCOVERY-BOOK.md` | Expanded (inline correction) | STRIDE threat count miscounted (32 → 29) | N/A — same file, corrected | *(this Wave's commit)* |
| `docs/discovery/README.md` | Expanded (inline correction) | Stale "not executed" status | N/A — same file, corrected | *(this Wave's commit)* |
| `docs/discovery/artifacts/README.md` | Expanded (inline correction) | Stale "empty" status | N/A — same file, corrected | *(this Wave's commit)* |
| `docs/discovery/reports/README.md` | Expanded (inline correction) | Stale "empty" status | N/A — same file, corrected | *(this Wave's commit)* |
| `docs/discovery/diagrams/README.md` | Expanded (inline correction) | Stale "empty" status | N/A — same file, corrected | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-00-BASELINE-AUDIT.md` | Created | Required Wave 0 deliverable | N/A | *(this Wave's commit)* |
| `docs/discovery/artifacts/DISCOVERY-CHANGE-MANIFEST.md` | Created | Required Wave 0 deliverable (this file) | N/A | *(this Wave's commit)* |

**No file deleted in Wave 0.** No file marked Superseded in Wave 0 (that
begins at Wave 14 for `DISCOVERY-BOOK.md`).

## Wave 1 — Vision, Scope, Operating Model Expansion

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W1-vision-scope-operating-model.md` | Created | Required Wave 1 deliverable | N/A | *(this Wave's commit)* |
| `.claude/context/vision.md` | Expanded (append-only) | Confirmed vision expansion, per user's explicit direction | N/A — history preserved | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-01-VISION-SCOPE.md` | Created | Required Wave 1 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 1.

## Wave 2 — Stakeholders, Actors, Personas Expansion

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W2-persona-catalog.md` | Created | 39-persona expansion, required Wave 2 deliverable | N/A | *(this Wave's commit)* |
| `.claude/context/stakeholders.md` | Expanded (append-only) | Wave 2 summary pointer added | N/A — history preserved | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-02-STAKEHOLDERS.md` | Created | Required Wave 2 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 2.

## Wave 3 — Enterprise Capability Map

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W3-enterprise-capability-map.md` | Created | 100-capability enterprise map, required Wave 3 deliverable | N/A | *(this Wave's commit)* |
| `docs/discovery/diagrams/W3-capability-map-categories.md` | Created | Category-level diagram (100-node diagram would be decorative, not useful) | N/A | *(this Wave's commit)* |
| `.claude/context/module-catalog.md` | Expanded (append-only) | Wave 3 pointer added | N/A — 8-context table preserved | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-03-CAPABILITIES.md` | Created | Required Wave 3 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 3.

## Wave 4 — Value Streams and Customer Journeys Expansion

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W4-value-streams-expanded.md` | Created | 20-stream expansion, required Wave 4 deliverable | N/A | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-04-VALUE-STREAMS.md` | Created | Required Wave 4 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 4.

## Wave 5 — Event Storming Gap Closure

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W5-event-storming-gap-closure.md` | Created | ~84 new Domain Events across 10 clusters, required Wave 5 deliverable | N/A | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-05-EVENT-STORMING.md` | Created | Required Wave 5 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 5. No diagram produced this Wave
(deliberate — see report, "Findings").

## Wave 6 — Business Rules and Policy Discovery

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W6-business-rules-and-policy-catalog.md` | Created | Configurable Result Verification Policy Model + 26-rule catalog, required Wave 6 deliverable | N/A | *(this Wave's commit)* |
| `.claude/context/open-questions.md` | Expanded (append-only) | Items 23–24 added | N/A — history preserved | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-06-BUSINESS-RULES.md` | Created | Required Wave 6 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 6.

## Wave 7 — Domain Discovery and Classification Re-evaluation

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W7-domain-classification-reevaluation.md` | Created | 6-alternative Core Domain Decision Matrix, required Wave 7 deliverable | N/A | *(this Wave's commit)* |
| `.claude/context/open-questions.md` | Expanded (append-only) | Item 14 annotated with re-evaluation | N/A — history preserved | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-07-DOMAIN-CLASSIFICATION.md` | Created | Required Wave 7 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 7. ADR 0011 itself not yet modified
— disposition decided at Wave 14.

## Wave 8 — Ubiquitous Language Expansion

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W8-ubiquitous-language-expansion.md` | Created | 37-term disambiguation, required Wave 8 deliverable | N/A | *(this Wave's commit)* |
| `.claude/context/glossary.md` | Expanded (append-only) | Wave 8 pointer added | N/A — existing terms preserved | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-08-UBIQUITOUS-LANGUAGE.md` | Created | Required Wave 8 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 8.

## Wave 9 — Bounded Context Remapping

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W9-bounded-context-remapping.md` | Created | 28-context remap + ADR-0012 Decision Matrix, required Wave 9 deliverable | N/A | *(this Wave's commit)* |
| `docs/discovery/diagrams/W9-context-map-enterprise.md` | Created | Tiered Context Map diagram | N/A | *(this Wave's commit)* |
| `.claude/context/module-catalog.md` | Expanded (append-only) | Wave 9 pointer added | N/A — history preserved | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-09-BOUNDED-CONTEXTS.md` | Created | Required Wave 9 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 9. ADR 0012 itself not yet modified
— disposition decided at Wave 14.

## Wave 10 — Candidate Modules and Platform Services

| Path | Disposition | Reason | Replacement | Commit |
|---|---|---|---|---|
| `docs/discovery/artifacts/W10-candidate-modules-platform-services.md` | Created | 28-module catalog derived from Wave 9 contexts, required Wave 10 deliverable | N/A | *(this Wave's commit)* |
| `docs/discovery/reports/GAP-CLOSURE-10-MODULE-CANDIDATES.md` | Created | Required Wave 10 report | N/A | *(this Wave's commit)* |

No file deleted or superseded in Wave 10.

---

*(Subsequent Waves append their own dated sections below this line.)*
