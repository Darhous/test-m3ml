# Playbook 04 — Domain Discovery

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 3 of 11 domain-content phases
**Depends On:** Playbook 03 (Event Storming board, Pivotal Event candidates)
**Produces For:** Playbook 05 (Domain Modeling drafts candidate Aggregates
per identified Subdomain), Playbook 06 (Bounded Contexts formalizes
boundaries around these Subdomains)

---

## Purpose

Cluster the raw Events/Commands/Actors from Playbook 03 into candidate
Subdomains, and classify each as Core, Supporting, or Generic (DDD Strategic
Design/Distillation, Constitution Section 6). This is the phase that
finally answers — or makes a well-evidenced attempt to answer — Open
Question item 14 (Constitution Section 46 / `open-questions.md` item 14):
"which Bounded Context is the platform's Core Domain?"

## Scope

**In scope:** clustering events/commands into candidate Subdomains,
Core/Supporting/Generic classification with explicit justification, a first
draft Ubiquitous Language glossary per Subdomain, identifying which
Business Capabilities (Playbook 02) each Subdomain serves.

**Out of scope:** formal Bounded Context boundary-drawing and Context
Mapping patterns (Playbook 06 — a Subdomain is a business-classification
concept; a Bounded Context is the resulting model/language boundary, and
the two do not always map 1:1); tactical modeling (Aggregates/Entities —
Playbook 05).

## Inputs

- `docs/discovery/artifacts/03-event-storming-board.md`
- `docs/discovery/artifacts/02-business-capability-map.md`
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 6 (Strategic
  Design/Distillation guidance, Core Domain definition, Section 47's
  Glossary entry)
- `.claude/context/open-questions.md` item 14

## Preconditions

- Playbook 03 marked complete; Event Storming board and Hotspot list exist.

## Required Skills

- `domain-driven-design` — Strategic Design and Distillation section
  specifically (Core/Supporting/Generic classification method, Domain
  Vision Statement technique).
- `doc-coauthoring` — for reader-testing the resulting Subdomain map against
  a domain-expert reader.

## Required Context Files

`glossary.md`, `module-catalog.md` (the existing 16 category-only
placeholders are an *input hint*, not a constraint — Subdomains discovered
here may or may not align with those categories; note where they diverge
and why).

## Project Bindings (this project)

- This phase is the designated place to propose an answer to
  `open-questions.md` item 14 (Core Domain). A proposed answer is recorded
  as `Proposed`, not `Accepted`, until it survives Playbook 11 (Validation)
  and is ratified in Playbook 12.

## Execution Steps

1. Group the events/commands from the Event Storming board by the business
   capability and actor cluster they belong to — an initial, mechanical
   clustering pass.
2. Refine clusters using Pivotal Events (Playbook 03) as candidate seams:
   where a Pivotal Event marks a handoff between stakeholder groups, treat
   that as a signal (not a rule) that a Subdomain boundary may belong
   there.
3. Name each candidate Subdomain in Ubiquitous Language, cross-checked
   against `module-catalog.md`'s 16 existing categories — note explicitly
   for each Subdomain whether it aligns with an existing category, splits
   one, or spans more than one.
4. For each Subdomain, apply the Core/Supporting/Generic test from the
   `domain-driven-design` skill: does competitive/differentiating value
   live here (Core), is it necessary but not differentiating (Supporting),
   or is it commodity (Generic, candidate for buy/reuse rather than deep
   custom modeling)?
5. Write a one-paragraph Domain Vision Statement for each candidate Core
   Subdomain, justifying the classification with evidence from Playbook 02
   (Business Capability Map) and Playbook 03 (event richness/complexity),
   not assertion.
6. Cross-check every classification against Constitution Section 6's
   explicit warning: a Bounded Context (or, at this stage, a Subdomain) is
   not automatically a microservice, and Core Domain status does not imply
   extraction — extraction remains governed solely by ADR 0001 (Selective
   Service Extraction).

## Deliverables

- A candidate Subdomain map with Core/Supporting/Generic classification and
  justification.
- A proposed answer to Open Question item 14 (Core Domain), status
  `Proposed`.
- A first-draft, per-Subdomain Ubiquitous Language glossary extension.

## Produced Artifacts

- `docs/discovery/artifacts/04-subdomain-map.md`
- `docs/discovery/reports/04-domain-discovery-report.md` (classification
  justifications, divergences from `module-catalog.md`'s existing
  categories, proposed Core Domain answer)

## Required Diagrams

- Subdomain map (Mermaid `flowchart` or `mindmap`), color/shape-coded by
  Core/Supporting/Generic, stored under `docs/discovery/diagrams/`.

## Review Checklist

- [ ] Every Subdomain traces to specific events/capabilities from Playbooks
      02–03 — none invented without evidentiary trail.
- [ ] Every Core classification has a written justification (Domain Vision
      Statement), not just a label.
- [ ] Divergence from `module-catalog.md`'s existing 16 categories is
      explicitly noted, not silently overwritten.
- [ ] No classification asserts or implies a microservice-extraction
      decision (that remains ADR 0001's exclusive gate).

## Quality Gates

- **DDD Consistency Review** (`domain-driven-design` skill's Quick
  Diagnostic, Constitution Section 6/49): applied to the Subdomain map as a
  whole before Exit.
- **Evidence Gate:** a Core classification without a Domain Vision
  Statement citing specific evidence fails this gate and must be revised or
  downgraded to Supporting/Generic pending more evidence.

## Exit Criteria

- Candidate Subdomain map complete, classified, and justified.
- A Proposed (not Accepted) answer to Open Question item 14 exists, with
  its evidentiary basis documented.

## Files To Update

- `.claude/context/open-questions.md` — item 14 annotated with "Proposed
  answer: see `docs/discovery/artifacts/04-subdomain-map.md`" — the item
  stays `Open` until Playbook 12 ratifies it (if it survives Validation).
- `.claude/context/glossary.md` — append Subdomain names as `Draft` terms.

## ADR Impact

Potentially significant: if the Core Domain answer survives Playbook 11
(Validation) unchanged, Playbook 12 authors an ADR recording it (extends
Constitution Section 46/47's "Core Domain: Open" entry to "Accepted", per
Constitution Section 39's ADR-before-Accepted rule). This playbook itself
does not author that ADR — it only proposes the answer.

## Common Mistakes

- Forcing every event cluster into exactly one of the 16 existing
  `module-catalog.md` categories instead of letting the evidence produce a
  different shape (categories are a hint, not a constraint, per this
  playbook's own Inputs section).
- Classifying a Subdomain as Core because it is *complex* rather than
  because it is *differentiating* — complexity and Core status are
  correlated but not identical (a Generic Subdomain, like notifications
  delivery mechanics, can be complex without being differentiating).
- Treating "Core Domain identified" as equivalent to "this becomes a
  microservice" — explicitly forbidden conflation (Constitution Section 6).
- Skipping the Domain Vision Statement step because the classification
  "feels obvious" — obviousness is not evidence.

## Self Review

For each Subdomain marked Core, re-read its Domain Vision Statement and ask:
"if a competitor built this exact capability, would that matter to the
business?" If the honest answer is no, downgrade the classification.

## Stop Conditions

- The Event Storming board (Playbook 03) does not contain enough material
  to justify any classification for a given cluster — return to Playbook
  03 rather than classifying on thin evidence.
- Two candidate Subdomains claim the same Pivotal Event as their boundary
  seam with no way to resolve which — log as a Hotspot for Playbook 06
  (Bounded Contexts) to resolve via Context Mapping, rather than guessing
  here.
