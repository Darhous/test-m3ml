# Playbook 10 — AI Discovery

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 9 of 11 domain-content phases
**Depends On:** Playbook 06 (Bounded Contexts), Playbook 07 (Business
Rules, for which decisions are sensitive/clinical), Playbook 08
(Integrations Discovery's general external-boundary method, specialized
here for the AI Gateway)
**Produces For:** Playbook 11 (Validation runs STRIDE + Human-in-the-Loop
gate checks over every AI use case found here), Playbook 12 (Final
Discovery Book's AI Gateway use-case catalog)

---

## Purpose

Discover candidate AI-assisted use cases across the platform's Bounded
Contexts, classify each by sensitivity and required Human-in-the-Loop
depth, and confirm every candidate fits within the governed AI Gateway
boundary already Accepted in ADR 0007 — without choosing an AI provider,
model, or vendor.

## Scope

**In scope:** candidate AI-assisted functions per Bounded Context
(summarization, pattern detection, anomaly detection, search, operational
assistance, clinical decision support — the permitted list from
Constitution Section 28), sensitivity classification per use case,
Human-in-the-Loop touchpoint design per use case, data-minimization
requirements per use case if data would leave the platform's control.

**Out of scope:** selecting an AI provider/model (forbidden platform-wide);
general (non-AI) integration discovery (Playbook 08); prompt engineering or
model evaluation design (SAD/implementation-level, later).

## Inputs

- `docs/discovery/artifacts/06-bounded-contexts.md`
- `docs/discovery/artifacts/07-business-rules-catalog.md`
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 28 (AI Governance
  Rules), ADR 0007 (Governed AI Gateway)
- `.claude/context/open-questions.md` item 11 (AI usage limits detail)

## Preconditions

- Playbook 06 and 07 marked complete.

## Required Skills

- `domain-driven-design` — Anti-Corruption Layer pattern, applied to the AI
  Gateway boundary specifically (Constitution Section 6/28).
- `stride-analysis-patterns` — first-pass threat identification for each AI
  use case's data flow.
- `threat-mitigation-mapping` — mapping identified AI-related threats
  (especially data exfiltration to an external provider) to candidate
  mitigations.
- `api-design-principles` — for sketching the AI Gateway's contract shape
  per use case (still technology-agnostic).

## Required Context Files

`constraints.md` (constraint #6: no autonomous final AI medical decision),
`open-questions.md` item 11.

## Project Bindings (this project)

- Every candidate AI use case must be checked against Constitution Section
  28's explicit Forbidden list (approving a medical result, modifying a
  verified medical result, publishing a final diagnosis, sending a final
  medical decision without human review) — any candidate resembling these
  is rejected outright at this phase, not softened.

## Execution Steps

1. Scan every Bounded Context's business rules (Playbook 07) and events
   (Playbook 03) for candidate AI-assisted opportunities, restricted to the
   Constitution Section 28 permitted list (Summarization, patient-friendly
   explanations, pattern detection, anomaly detection, search, operational
   assistance, clinical decision *support*).
2. For each candidate use case, classify its data sensitivity (does it
   touch medical/personal data? does it need to leave the platform's
   control to an external provider?).
3. For each candidate use case, design the Human-in-the-Loop touchpoint:
   at what point does a human review the AI output before it becomes a
   "final" action, per Constitution Section 28's mandatory gate.
4. Reject outright (do not soften or reword) any candidate that matches
   Constitution Section 28's Forbidden list — log the rejection with
   reasoning so it is not silently reconsidered later.
5. For any use case that would send sensitive data to an external AI
   provider, apply the `threat-mitigation-mapping` skill to identify what
   data-minimization/contractual/technical safeguard category would be
   required (categories, not vendor-specific controls) before the policy
   gate (Constitution Section 28) could be satisfied.
6. Sketch the AI Gateway's contract shape per use case (input, expected
   output type, required audit fields per Constitution Section 23/28) —
   technology-agnostic, no model/provider named.
7. Narrow `open-questions.md` item 11 (AI usage limits) with the concrete
   use-case boundaries found in this phase, without inventing limits beyond
   what Constitution Section 28 already fixes.

## Deliverables

- AI use-case catalog: per Bounded Context, per use case, sensitivity
  classification, Human-in-the-Loop touchpoint, data-minimization needs.
- Rejected-candidate log (use cases that violate Section 28's Forbidden
  list).

## Produced Artifacts

- `docs/discovery/artifacts/10-ai-use-case-catalog.md`
- `docs/discovery/reports/10-ai-discovery-report.md` (rejected candidates
  with reasoning, data-minimization findings, narrowed open-questions #11)

## Required Diagrams

- Mermaid `flowchart` per use case, in the same style as the Constitution's
  Section 28 AI Gateway diagram, showing Input → AI Gateway → Suggestion →
  Human-in-the-Loop → Final Action, with the audit log branch included.

## Review Checklist

- [ ] Every use case is drawn from the Constitution Section 28 permitted
      list — none invented outside it.
- [ ] Every use case has an explicit Human-in-the-Loop touchpoint design.
- [ ] Every rejected candidate is logged with its specific Forbidden-list
      match, not silently dropped.
- [ ] No AI provider, model name, or vendor is named anywhere in this
      phase's output.

## Quality Gates

- **Forbidden-List Gate:** every candidate use case explicitly checked
  against Constitution Section 28's Forbidden list before acceptance — this
  is a hard gate, not a judgment call.
- **Human-in-the-Loop Design Gate:** a use case without a concrete
  Human-in-the-Loop touchpoint design fails this gate and cannot proceed to
  the catalog as "ready" — it is logged as incomplete instead.

## Exit Criteria

- AI use-case catalog complete for every Bounded Context that surfaced a
  candidate; every accepted use case has a Human-in-the-Loop design; every
  rejected candidate is logged with reasoning.

## Files To Update

- `.claude/context/open-questions.md` — item 11 narrowed with concrete
  use-case boundaries found.

## ADR Impact

Generally none — individual AI use cases are implementations of the
already-Accepted ADR 0007, not new architectural decisions. If this phase
reveals a genuinely new *category* of AI governance need not covered by
Constitution Section 28 (e.g., a use case type the Forbidden/Permitted list
does not clearly address), flag it for a Constitution Amendment
(Section 45) rather than silently classifying it either way.

## Common Mistakes

- Softening a Forbidden-list violation into a "supported" use case by
  rewording it (e.g., calling autonomous diagnosis-publishing
  "AI-assisted fast-track review" without an actual human gate) — this is
  exactly the kind of reframing Constitution Section 28 is designed to
  prevent.
- Designing a Human-in-the-Loop touchpoint that is technically present but
  trivially bypassable (e.g., an "auto-approve after 1 hour" timeout) —
  this does not satisfy the mandatory gate's intent.
- Naming a specific AI provider/model "just as an example" — even
  illustrative vendor names are out of scope for this Constitution-governed
  Discovery.
- Treating every AI use case as equally sensitive instead of doing the
  per-case classification Step 2 requires.

## Self Review

For every accepted use case, re-read its Human-in-the-Loop design and ask:
"could this specific design allow a sensitive action to reach 'final'
status without a real human decision?" If the honest answer is "possibly,"
the design is not done.

## Stop Conditions

- A stakeholder or business requirement insists on a use case that matches
  the Forbidden list, and pushes back on the rejection — stop, do not
  reinterpret Section 28 to accommodate it; escalate to the user as a
  direct Constitution conflict requiring their explicit decision (Section
  44), not a Discovery-level resolution.
- A use case's data-minimization requirement cannot be met by any known
  category of safeguard — log as a blocking gap for that specific use case
  and mark it `Not Ready`, rather than proceeding with an ungoverned data
  flow.
