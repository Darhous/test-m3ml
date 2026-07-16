# artifacts/

**Status: populated.** *(Updated 2026-07-16, Gap Closure Wave 0 — this file
previously said "empty," which is stale.)* Holds the structured working
outputs of every executed Discovery playbook: the Playbook 01 execution
ledger, Business Capability Map, Event Storming board, Subdomain map,
candidate Aggregates, Bounded Contexts/Context Map, Business Rules catalog,
Integration inventory, tenancy/localization analysis, AI use-case catalog,
plus the 3 living registers (`ASSUMPTION-REGISTER.md`,
`OPEN-QUESTIONS-REGISTER.md`, `RISK-REGISTER.md`) and, from the Gap Closure
program, `DISCOVERY-CHANGE-MANIFEST.md` and expanded enterprise-wide
artifacts. See each playbook under `../prompts/` for its exact "Produced
Artifacts" list and expected filename.

Naming convention: `<phase-number>-<short-name>.md` (e.g.,
`02-business-capability-map.md`), matching the numbering of the playbook
that produces it. `00-master-execution-log.md` is the one artifact
maintained continuously across the whole run rather than produced once by a
single phase (Playbook 01).
