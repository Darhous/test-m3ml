# reports/

**Status: populated.** *(Updated 2026-07-16, Gap Closure Wave 0 — was
"empty," now stale.)* Holds the narrative reports produced by each executed
Discovery playbook, plus the Gap Closure program's `GAP-CLOSURE-NN-*.md`
reports (see `../GAP-CLOSURE-CHANGELOG.md`).

This folder holds the narrative reports produced by each Discovery
playbook: findings, open items raised, conflicts raised and their
resolution, and (for Playbook 11) the full cross-phase Validation Report
and STRIDE + mitigation-mapping record, and (for Playbook 12) the Discovery
Completion Report. See each playbook under `../prompts/` for its exact
"Produced Artifacts" report filename.

Naming convention: `<phase-number>-<phase-name>-report.md` (e.g.,
`04-domain-discovery-report.md`). Playbook 11 produces two reports
(`11-validation-report.md`, `11-stride-mitigation-mapping.md`); Playbook 12
produces `12-discovery-completion-report.md` (and, per that playbook's own
note, the compiled Discovery Book itself may live here as
`12-discovery-book.md` or at `docs/discovery/DISCOVERY-BOOK.md` — decided
at execution time).
