# Playbook 02 — Business Discovery

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 1 of 11 domain-content phases
**Depends On:** Playbook 01 (Master preconditions satisfied)
**Produces For:** Playbook 03 (Event Storming needs real business processes
to storm), Playbook 04 (Domain Discovery needs business capabilities to
classify into subdomains), Playbook 09 (SaaS Platform Discovery needs
business-level market/scale context)

---

## Purpose

Establish *why* the platform exists and *what* business value it delivers,
in business language, before any technical or domain-modeling activity
starts. Produces the Business Capability Map, Value Stream inventory, and a
refined Stakeholder needs picture that every later phase is grounded in.

## Scope

**In scope:** business goals, business capabilities (named in business
language, not system language), value streams (end-to-end flows that
deliver value to a stakeholder), stakeholder needs refinement, business-level
constraints (market, regulatory posture at a business-description level —
not legal certification), and business-level success measures.

**Out of scope:** domain events (Playbook 03), Bounded Contexts or Aggregates
(Playbooks 04–06), technical integration detail (Playbook 08), any
architecture or technology decision.

## Inputs

- `.claude/context/vision.md` (Draft vision statement)
- `.claude/context/stakeholders.md` (Draft stakeholder categories)
- `.claude/context/open-questions.md` (items 1, 2, 4, 9, 12 are
  business-shaped questions this phase should attempt to narrow, not
  necessarily fully close)
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 3 (Vision) and
  Section 4 (Core Values)

## Preconditions

- Playbook 01's ledger shows Phase 02 as the next eligible phase.
- `.claude/context/vision.md` and `stakeholders.md` exist and are readable
  (they do — both are Draft-status Context Store files).

## Required Skills

- `doc-coauthoring` — for structuring stakeholder-input elicitation and
  reader-testing the resulting Business Capability Map.
- `domain-driven-design` — specifically its Strategic Design / Distillation
  guidance (Core/Supporting/Generic subdomain classification lens), applied
  here at the business-capability level as a *first pass*, refined further
  in Playbook 04.

## Required Context Files

`vision.md`, `stakeholders.md`, `open-questions.md`, `constraints.md`
(for the already-Confirmed constraints this phase must not contradict, e.g.,
"medical data is highly sensitive").

## Project Bindings (this project)

- Starting point: Laboratory Management (Confirmed, `vision.md`).
- Long-term goal: broad healthcare platform (Confirmed, `vision.md`).
- Known stakeholder categories to validate/refine, not replace:
  `stakeholders.md`'s 15 categories.

## Execution Steps

1. Restate the Confirmed vision items from `vision.md` verbatim — do not
   re-derive or re-word them (No-Guessing Rule).
2. For each stakeholder category in `stakeholders.md`, elicit (from the
   user — never invent) its primary business needs and the value stream(s)
   it participates in. Leave a category's needs unfilled and flagged `Open`
   rather than guessing.
3. Build a Business Capability Map: a flat or lightly-nested list of
   *what the business does* (e.g., "Order a Lab Test," "Verify a Result,"
   "Bill a Payer") — business language, not system/module language. Do not
   let this map silently become the Module Catalog; it is an input to
   Playbook 04, not a substitute for it.
4. For each Business Capability, do a first-pass Core/Supporting/Generic
   classification (DDD Strategic Design), explicitly marked `Candidate` —
   final classification happens in Playbook 04 once Event Storming
   (Playbook 03) has surfaced the actual event flow.
5. Trace 2–5 end-to-end Value Streams (e.g., "Patient receives a verified
   lab result") from trigger to value delivered, naming which stakeholders
   and capabilities participate at each step.
6. Cross-check every business-level claim against `constraints.md` and
   `docs/constitution/PROJECT-CONSTITUTION.md` — a business goal that would
   require violating an Accepted constraint (e.g., a goal that assumes AI
   can auto-approve a diagnosis) is flagged as a Conflict, not silently
   accepted (see `EXECUTION-GUIDE.md`, "How to Handle Conflicts").
7. Log every business-level question that cannot be answered from existing
   context or the current conversation as a new item in the phase report,
   cross-referenced to `open-questions.md` numbering (extend, do not
   renumber existing items).

## Deliverables

- Business Capability Map (business-language, with Candidate
  Core/Supporting/Generic tags).
- Value Stream inventory (2–5 end-to-end flows).
- Refined stakeholder needs (extends `stakeholders.md`'s existing
  categories; does not delete or renumber them).

## Produced Artifacts

- `docs/discovery/artifacts/02-business-capability-map.md`
- `docs/discovery/artifacts/02-value-streams.md`
- `docs/discovery/reports/02-business-discovery-report.md` (summary,
  open items raised, conflicts raised)

## Required Diagrams

- Business Capability Map (Mermaid `flowchart` or `mindmap`, grouped by
  Core/Supporting/Generic candidate tag).
- Value Stream diagram(s) (Mermaid `journey` or `flowchart`, one per traced
  value stream), stored under `docs/discovery/diagrams/`.

## Review Checklist

- [ ] Every Business Capability is named in business language (a domain
      expert would recognize the name; not a technical term).
- [ ] Every stakeholder category from `stakeholders.md` was either refined
      or explicitly left `Open` with a reason — none silently skipped.
- [ ] Every Core/Supporting/Generic tag is marked `Candidate` (not
      finalized at this phase).
- [ ] No business goal contradicts an existing Accepted constraint without
      being flagged as a Conflict.

## Quality Gates

- **Reader Test** (`doc-coauthoring`): could a business stakeholder (not an
  engineer) read the Business Capability Map and confirm "yes, that's what
  we do"? If not, the map is too technical and must be revised before
  Exit.
- **No-Guessing Gate:** every capability/value stream traces to either an
  explicit user statement in this phase or an existing Confirmed item in
  `vision.md`/`stakeholders.md` — nothing is asserted from assumption.

## Exit Criteria

- Business Capability Map and Value Stream inventory both exist, pass the
  Reader Test, and every open item is logged (not silently dropped).
- No unresolved Conflict from Step 6 remains unescalated.

## Files To Update

- `.claude/context/stakeholders.md` — append refined needs per category
  (status-tagged, history preserved, per that file's own update rule).
- `.claude/context/open-questions.md` — append any new business-level
  question surfaced (do not renumber existing items).

## ADR Impact

None expected at this phase — business capabilities are pre-architectural.
If a business goal *forces* an architectural implication (e.g., "we must
support real-time cross-branch inventory visibility"), log it as an input
to Playbook 04/06, not as an ADR here — ADRs are authored at Playbook 12 (or
earlier phases explicitly named for it) once the architectural shape is
actually decided.

## Common Mistakes

- Naming capabilities after system modules or technical components instead
  of business outcomes (a classic Business Discovery failure that
  pre-biases the later Domain Discovery phase).
- Treating the Candidate Core/Supporting/Generic tags as final — they are
  not; Playbook 04 owns the final classification.
- Skipping stakeholder categories with no obvious "business need" (e.g.,
  Security and Compliance Teams) instead of eliciting their needs too.
- Silently resolving a Conflict with an Accepted constraint instead of
  flagging it.

## Self Review

Re-read the Business Capability Map and ask: "does every item describe
value delivered, not a system function?" Re-read the Value Streams and
confirm each one names a real trigger and a real delivered value, not a
technical process.

## Stop Conditions

- A business goal is stated that directly and unavoidably contradicts an
  Accepted Constitution rule or ADR (e.g., a stated goal requiring AI to
  autonomously finalize a diagnosis, contradicting ADR 0007) — stop and
  escalate to the user per Constitution Section 44, do not proceed by
  reinterpreting the goal or the rule.
- A stakeholder category cannot be reached/elicited at all — mark it
  explicitly `Open` in the phase report and continue; do not block the
  whole phase on one category, but do not silently invent its needs either.
