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

---

*(Subsequent Waves append their own dated sections below this line —
placeholder for Wave 1 onward.)*
