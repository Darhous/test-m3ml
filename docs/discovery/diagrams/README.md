# diagrams/

**Status: populated.** *(Updated 2026-07-16, Gap Closure Wave 0 — was
"empty," now stale.)*

This folder holds the Mermaid/C4 diagrams produced by each Discovery
playbook: Business Capability Maps, Value Stream diagrams, Event Storming
timelines, Subdomain maps, Aggregate class diagrams, the Context Map, C4
System Context/Container diagrams, Workflow state machines, integration and
AI-Gateway flow diagrams, and the updated Tenant Isolation diagram. See each
playbook under `../prompts/` for its exact "Required Diagrams" list.

Every diagram here is produced by the phase that owns the content it
depicts (never batched or deferred), and every diagram is syntax-validated
by Playbook 11 (Validation) before the Discovery Book (Playbook 12)
references it — see `docs/discovery/DISCOVERY-FRAMEWORK.md` Section 7.

Naming convention: `<phase-number>-<diagram-name>.md` (or `.mmd`, decided
at execution time), matching the numbering of the playbook that produces
it.
