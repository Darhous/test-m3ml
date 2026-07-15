# Playbook 12 — Final Discovery Book

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 11 of 11 domain-content phases (final)
**Depends On:** Playbook 11 (Validation passed, zero unresolved
contradictions, zero unmitigated threats)
**Produces For:** the future Software Architecture Document task (not part
of this framework — the Discovery Book is its primary input)

---

## Purpose

Compile every Validation-passed artifact from Playbooks 02–11 into a single
coherent Discovery Book, formally update all affected `.claude/context/`
files, author any ADR that Playbook 11's consolidated list identified as
warranted, and produce the Discovery Completion Report — the final,
citable record that a future Software Architecture Document task consumes
instead of re-deriving Discovery from scratch.

## Scope

**In scope:** compiling the Discovery Book document, promoting Proposed
findings to their correct Context Store status (never silently to
`Accepted` — only through the same ADR-first discipline the Constitution
already requires), authoring new ADRs where warranted, producing the
Discovery Completion Report, final `module-catalog.md` candidate-content
update (still explicitly not a "final Module Catalog" per Constitution
Section 2/46 — Discovery produces strong candidates, not a closed list).

**Out of scope:** starting the Software Architecture Document itself;
writing production code; making any decision Playbook 11 flagged as
unresolved/escalated (those remain with the user, not this playbook).

## Inputs

Every artifact under `docs/discovery/artifacts/` and `docs/discovery/
reports/` from Playbooks 02–11.

## Preconditions

- Playbook 11 marked complete with zero unresolved contradictions and zero
  unmitigated/unowned threats.

## Required Skills

- `doc-coauthoring` — for compiling and reader-testing the final Discovery
  Book as a single, coherent document.
- `architecture-decision-records` — for authoring any new ADR identified by
  Playbook 11's consolidated ADR-impact list.
- `c4-architecture` and `mermaid-diagrams` — for assembling the final
  diagram set (Context Map, C4 diagrams, per-context class diagrams, state
  machines, integration diagrams) into one consistent, cross-referenced
  collection.

## Required Context Files

All of `.claude/context/*.md` — this is the phase where Discovery's
findings are formally written back.

## Project Bindings (this project)

- Any promotion of `open-questions.md` item 14 (Core Domain) from Proposed
  to Accepted happens here, and only here, gated by Playbook 11 having
  found no contradiction in that finding — per Constitution Section 39
  (ADR-before-Accepted).

## Execution Steps

1. Assemble the Discovery Book's structure: Executive Summary, Business
   Context (Playbook 02), Event Model (Playbook 03), Subdomain Map
   (Playbook 04), Domain Model (Playbook 05), Bounded Contexts and Context
   Map (Playbook 06), Business Rules (Playbook 07), Integrations (Playbook
   08), SaaS Platform Findings (Playbook 09), AI Use Cases (Playbook 10),
   Validation Summary (Playbook 11).
2. For every finding Playbook 11 flagged as "ready to promote" (no
   contradiction, no unmitigated threat, evidence-based per the
   No-Guessing Rule), determine whether it rises to "significant
   architectural decision" per Constitution Section 39. If yes, author a
   new ADR (`docs/adr/00NN-*.md`, following the existing 10 ADRs' format
   exactly, continuing the sequential numbering) with Status `Accepted`.
   If the finding is a narrower, implementation-level detail, record it
   directly in the relevant Context Store file without a new ADR, exactly
   as v1/v2 of the Constitution already distinguished "significant
   decision" from "process/detail" content.
3. Update `.claude/context/decisions.md`'s ADR Index and Proposed Decisions
   table to reflect any newly authored ADR, following that file's own
   established update procedure (append, preserve history, no silent
   status changes).
4. Update `.claude/context/module-catalog.md` with the candidate Bounded
   Context list from Playbook 06, explicitly labeled "Discovery Candidates
   — not a final Module Catalog," preserving the existing 16 categories and
   noting alignment/divergence (already partially done in Playbook 06;
   this step finalizes it against Validation-passed content only).
5. Update `.claude/context/glossary.md`, `constraints.md`, and
   `open-questions.md` with the final, Validation-passed versions of
   everything appended incrementally during Playbooks 02–10 (history
   preserved, no deletions, per each file's own established rule).
6. Produce the Discovery Completion Report: what was discovered, what was
   promoted to Accepted (with ADR references), what remains Open, what
   Conflicts were escalated to the user and how they were resolved, and a
   full artifact/diagram index.
7. Confirm the Discovery Book and Completion Report both pass a final
   Reader Test (`doc-coauthoring`) before declaring this playbook, and the
   framework's phase sequence, complete.

## Deliverables

- The Final Discovery Book (single compiled document).
- Any newly authored ADR(s).
- Updated Context Store files.
- Discovery Completion Report.

## Produced Artifacts

- `docs/discovery/reports/12-discovery-book.md` (or
  `docs/discovery/DISCOVERY-BOOK.md` at the framework root — decided at
  execution time based on how the team wants to surface it; both locations
  are acceptable, this playbook does not mandate one over the other)
- `docs/discovery/reports/12-discovery-completion-report.md`
- Any new file(s) under `docs/adr/`

## Required Diagrams

A consolidated diagram index referencing every diagram produced across
Playbooks 02–11 (no new diagram types required beyond what those phases
already produced and Playbook 11 validated).

## Review Checklist

- [ ] Every section of the Discovery Book traces to a specific,
      Validation-passed Playbook 02–11 artifact — nothing added fresh at
      this phase.
- [ ] Every new ADR follows the existing 10 ADRs' exact format (Status,
      Context, Decision, Alternatives Considered, Positive Consequences,
      Negative Consequences, Risks, Verification, Revisit Triggers).
- [ ] Every Context Store update preserves history (no deletions, no
      silent status changes) per each file's own established rule.
- [ ] `module-catalog.md`'s update is explicitly labeled as Discovery
      Candidates, not a final Module Catalog.

## Quality Gates

- **Traceability Gate:** every claim in the Discovery Book must be traceable
  to a specific artifact from Playbooks 02–11 — no new claims introduced at
  compilation time.
- **ADR Format Gate:** every new ADR checked against the existing 10 ADRs'
  structure before being added to `docs/adr/`.
- **Final Reader Test:** the Discovery Book and Completion Report must both
  pass `doc-coauthoring`'s reader test before Exit.

## Exit Criteria

- Discovery Book compiled and passes the Reader Test.
- All warranted ADRs authored with Status `Accepted`.
- All affected Context Store files updated, history preserved.
- Discovery Completion Report produced and accurate against the execution
  ledger (Playbook 01).

## Files To Update

- `.claude/context/decisions.md`, `glossary.md`, `constraints.md`,
  `open-questions.md`, `module-catalog.md` (as detailed in Execution Steps
  3–5).

## ADR Impact

This is the phase where ADRs are actually authored (see Execution Step 2).
Every new ADR must be cross-referenced from `decisions.md`'s ADR Index,
exactly as ADR 0001–0010 already are.

## Common Mistakes

- Compiling the Discovery Book from memory/impression of the phases instead
  of strictly from their Validation-passed artifacts.
- Promoting a finding straight to `Accepted` in a Context Store file
  without authoring the required ADR first (violates Constitution Section
  39, which this framework must not bypass even at the very end of
  Discovery).
- Treating the `module-catalog.md` update as license to declare a final
  Module Catalog — explicitly still forbidden per Constitution Section
  2/46, even after a full Discovery pass.
- Ending the framework without producing the Discovery Completion Report,
  leaving no clear record of what is now Accepted vs. still Open for the
  next task (the future SAD) to consume.

## Self Review

Read the Discovery Completion Report as if you are the person about to
start the Software Architecture Document task with zero other context:
could you correctly tell, from this report alone, what is Accepted, what is
still Open, and where every ADR and Context Store update lives? If not, the
report is incomplete.

## Stop Conditions

- Playbook 11 is not actually complete (a contradiction or unmitigated
  threat remains) — do not proceed to compilation; return to Playbook 11.
- A finding that Execution Step 2 determines needs a new ADR cannot be
  written without inventing a detail not actually established by Playbooks
  02–11 — stop, do not fill the gap with an assumption; leave the finding
  at its current (non-Accepted) status and note the gap in the Completion
  Report instead.
