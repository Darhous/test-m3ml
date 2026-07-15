# Playbook 06 — Bounded Contexts

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 5 of 11 domain-content phases
**Depends On:** Playbook 05 (candidate Aggregates and cross-Subdomain
overlap list)
**Produces For:** Playbook 07 (Business Rules works within now-fixed
Context boundaries), Playbook 08 (Integrations Discovery needs Context
boundaries to know what counts as "external"), Playbook 09 (SaaS Platform
Discovery applies tenancy rules per Context), Playbook 12 (Final Discovery
Book's Context Map is this phase's primary deliverable, formalized)

---

## Purpose

Formally draw Bounded Context boundaries, resolve the cross-Subdomain
overlaps flagged by Playbook 05, assign every candidate Aggregate to
exactly one Bounded Context, and produce the Context Map with named
Context Mapping patterns for every inter-context relationship — directly
implementing Constitution Section 7 (Bounded Context Rules).

## Scope

**In scope:** Bounded Context naming and documentation (purpose, Ubiquitous
Language, owning module candidate), Context Map construction, Context
Mapping pattern assignment (Customer/Supplier, Conformist, Anti-Corruption
Layer, Open Host Service + Published Language, Shared Kernel), resolving
Playbook 05's overlap list, first-draft Module Ownership mapping
(Constitution Section 8).

**Out of scope:** detailed business rules within a context (Playbook 07);
external-system-specific integration design (Playbook 08 — this phase only
notes *that* a boundary touches an external system, not *how*); the final
Module Catalog (this phase produces strong *candidates* feeding it, per the
same caution already established in `module-catalog.md` and Constitution
Section 2).

## Inputs

- `docs/discovery/artifacts/05-candidate-aggregates.md`
- `docs/discovery/artifacts/04-subdomain-map.md`
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 7 (Bounded Context
  Rules), Section 8 (Module Ownership Rules), Section 9 (Module Dependency
  Rules)

## Preconditions

- Playbook 05 marked complete; candidate Aggregate catalog and overlap list
  exist.

## Required Skills

- `domain-driven-design` — Bounded Contexts and Context Mapping section
  (the nine mapping patterns, Anti-Corruption Layer, Shared Kernel
  cautions).
- `c4-architecture` — for the System Context-level diagram of the resulting
  Context Map.
- `mermaid-diagrams` — general diagram support.

## Required Context Files

`glossary.md`, `module-catalog.md` (compare final candidate contexts
against the 16 existing categories; this phase is the first place a real
divergence gets formally recorded, still without declaring
`module-catalog.md` final per Constitution Section 2/46).

## Project Bindings (this project)

- Every Bounded Context touching device data must plan for the Anti-
  Corruption Layer required by Constitution Section 6/24 (ADR 0006).
- Every Bounded Context touching AI must plan for the Anti-Corruption Layer
  required by Constitution Section 28 (ADR 0007).
- No Bounded Context boundary decision may imply a microservice
  extraction — that remains exclusively ADR 0001's gate (Constitution
  Section 5/9).

## Execution Steps

1. Resolve every cross-Subdomain overlap from Playbook 05: for each
   overlapping Aggregate, decide which Bounded Context owns it, using the
   Subdomain classification (Playbook 04) and consistency rationale
   (Playbook 05) as the deciding evidence — document the reasoning, don't
   just pick one.
2. Name each resulting Bounded Context in Ubiquitous Language; write its
   purpose statement and list its owned Aggregates.
3. For every pair of Bounded Contexts with a relationship (one context's
   Aggregate references another's by ID, or one context reacts to another's
   events), assign an explicit Context Mapping pattern — no unlabeled
   relationship is allowed (Constitution Section 7).
4. Apply the Anti-Corruption Layer pattern at every boundary touching an
   external system (device, AI provider, external API partner, legacy
   system) — even if the external system's detailed integration is not
   designed until Playbook 08, the *boundary* and its ACL requirement is
   fixed here.
5. Flag any proposed Shared Kernel explicitly — per Constitution Section 7,
   this requires its own ADR later (Playbook 12) because it is an exception
   to Module Ownership.
6. Draft a first-pass Module Ownership mapping: which Bounded Context(s)
   each candidate Module owns, cross-checked against Constitution Section 8
   ("one owning Module per Bounded Context concept").
7. Compare the resulting Context list against `module-catalog.md`'s 16
   categories; record alignment, splits, merges, or net-new categories
   explicitly.
8. Validate the resulting Module Dependency graph is acyclic (Constitution
   Section 9) before Exit — a cycle here is a Stop Condition, not a note.

## Deliverables

- Formal Bounded Context list: name, purpose, owned Aggregates, Ubiquitous
  Language glossary per context.
- Context Map: every inter-context relationship labeled with a named
  pattern.
- First-draft Module Ownership mapping.

## Produced Artifacts

- `docs/discovery/artifacts/06-bounded-contexts.md`
- `docs/discovery/artifacts/06-context-map.md`
- `docs/discovery/reports/06-bounded-contexts-report.md` (overlap
  resolutions with rationale, `module-catalog.md` divergence notes, flagged
  Shared Kernels, acyclic-graph confirmation)

## Required Diagrams

- C4 System Context diagram (via `c4-architecture`) showing the platform's
  external boundary.
- Context Map diagram (Mermaid `flowchart`), every edge labeled with its
  Context Mapping pattern, stored under `docs/discovery/diagrams/`.
- Module Dependency graph (Mermaid `flowchart`), matching the style of the
  existing diagram in Constitution Section 9.

## Review Checklist

- [ ] Every candidate Aggregate from Playbook 05 is assigned to exactly one
      Bounded Context.
- [ ] Every inter-context relationship has a named Context Mapping pattern
      — none unlabeled.
- [ ] Every boundary touching an external system has an Anti-Corruption
      Layer noted.
- [ ] The Module Dependency graph is acyclic.
- [ ] Every proposed Shared Kernel is explicitly flagged for an ADR.

## Quality Gates

- **Context Map Completeness Gate:** no relationship between two contexts
  may go unlabeled — this is a hard gate per Constitution Section 7,
  Constitution Section 49 (Fitness Function: DDD Boundaries), not a
  recommendation.
- **Acyclic Graph Gate:** Constitution Section 49's Dependency Direction
  Fitness Function, applied here for the first time to real candidate
  contexts instead of the illustrative example in Section 9's diagram.
- **DDD Consistency Review** (`domain-driven-design` Quick Diagnostic).

## Exit Criteria

- Context Map is complete, every relationship labeled, acyclic dependency
  graph confirmed, `module-catalog.md` divergence documented.

## Files To Update

- `.claude/context/module-catalog.md` — append a "Candidate Contexts from
  Discovery" section cross-referencing the 16 existing categories (append
  only; the file's own rule against filling in a final Module list still
  holds — these are Discovery candidates, explicitly not final, per that
  file's own update rule and Constitution Section 2/46).
- `.claude/context/glossary.md` — append per-context Ubiquitous Language
  terms.

## ADR Impact

Likely significant: any proposed Shared Kernel requires an ADR (Constitution
Section 7). A Context Map that reveals a materially different Module
grouping than the Section 11 Independent Components list may also warrant
an ADR at Playbook 12 if it changes the Constitution's Section 11 list —
flagged here, authored there.

## Common Mistakes

- Resolving an Aggregate overlap by splitting the Aggregate itself instead
  of deciding which context owns it whole — Aggregates are not meant to be
  cut across a Context boundary.
- Treating "no relationship needed" as the default for two contexts that
  are obviously related (missing edges in the Context Map are as much a
  defect as unlabeled ones).
- Silently making a Shared Kernel decision without flagging it for an ADR.
- Confusing a Bounded Context boundary with a deployment/service boundary —
  re-triggers the exact mistake Constitution Section 6 explicitly warns
  against.

## Self Review

Walk the Context Map edge by edge and confirm each labeled pattern actually
matches the relationship's real shape (e.g., don't label something
Anti-Corruption Layer if it's really a Shared Kernel — the label must
describe reality, not aspiration).

## Stop Conditions

- The Module Dependency graph contains a cycle after Step 8 — stop, do not
  proceed to Playbook 07 with a cyclic graph; return to Step 1 and
  re-resolve the offending overlap.
- A Context boundary decision would require violating Schema per Module
  (ADR 0003) or No Direct Cross-Module Database Access (Constitution
  Section 16) to be workable — stop and escalate; do not draw a boundary
  that cannot be implemented under Accepted rules.
