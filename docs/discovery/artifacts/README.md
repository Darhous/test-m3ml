# artifacts/

**Status: empty.** Discovery has not been executed yet.

This folder will hold the structured working outputs of each Discovery
playbook once `EXECUTE-DISCOVERY.md` is run: the Playbook 01 execution
ledger, Business Capability Map, Event Storming board, Subdomain map,
candidate Aggregates, Bounded Contexts/Context Map, Business Rules catalog,
Integration inventory, tenancy/localization analysis, and the AI use-case
catalog. See each playbook under `../prompts/` for its exact "Produced
Artifacts" list and expected filename.

Naming convention: `<phase-number>-<short-name>.md` (e.g.,
`02-business-capability-map.md`), matching the numbering of the playbook
that produces it. `00-master-execution-log.md` is the one artifact
maintained continuously across the whole run rather than produced once by a
single phase (Playbook 01).
