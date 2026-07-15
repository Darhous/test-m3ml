# Playbook 11 — Validation

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 10 of 11 domain-content phases
**Depends On:** Playbooks 02–10 (all Discovery content produced)
**Produces For:** Playbook 12 (Final Discovery Book assembles only
Validation-passed content)

---

## Purpose

Run the full cross-phase quality review over everything Playbooks 02–10
produced before it is compiled into the Final Discovery Book: DDD
consistency, contradiction detection against the Constitution/ADRs/Context,
full STRIDE and mitigation mapping over every integration and AI use case,
completeness checking against Open Questions, terminology consistency, and
diagram syntax validation. This is the Discovery-phase analog of the
Constitution's own Self-Validation pattern (Constitution Section 62).

## Scope

**In scope:** reviewing every artifact produced by Playbooks 02–10 as a
whole (not phase-by-phase re-review — each phase already ran its own Review
Checklist/Quality Gates; this phase checks *cross-phase* consistency that
no single phase could see), full STRIDE + threat-mitigation-mapping pass,
Reader Testing the discovery narrative end-to-end, diagram syntax
validation across all produced diagrams.

**Out of scope:** producing new domain content (if Validation finds a gap,
it is logged for the user/a return to the relevant phase, not filled in
here); writing the Final Discovery Book itself (Playbook 12).

## Inputs

All artifacts under `docs/discovery/artifacts/` and `docs/discovery/reports/`
from Playbooks 02–10; `docs/constitution/PROJECT-CONSTITUTION.md`;
`docs/adr/*.md`; `.claude/context/*.md`.

## Preconditions

- Playbooks 02–10 all marked complete in the execution ledger.

## Required Skills

- `domain-driven-design` — full Quick Diagnostic re-applied across the
  entire discovered model, not just per-phase.
- `stride-analysis-patterns` — full threat review over every integration
  (Playbook 08) and AI use case (Playbook 10).
- `threat-mitigation-mapping` — mitigation mapping for every threat STRIDE
  identifies, per Constitution Section 37 (no unmitigated threat without a
  named owner/accepted-risk decision).
- `doc-coauthoring` — Reader Testing pass on the full Discovery narrative.
- `mermaid-diagrams` — syntax validation pass across every diagram produced
  by Playbooks 02–10.
- `api-design-principles` — review of any AI Gateway/API contract sketches
  from Playbooks 08/10 for consistency with Constitution Section 14.

## Required Context Files

All of `.claude/context/*.md` (this phase is where Discovery's proposed
changes are checked against the full current state before Playbook 12
commits them).

## Project Bindings (this project)

- Cross-check every Discovery finding against `docs/constitution/
  PROJECT-CONSTITUTION.md`'s Sections 5–37 (the rule sections) — a finding
  that contradicts an Accepted rule is a defect in Discovery output, not a
  reason to question the Constitution (Constitution Amendment is a separate,
  explicit process, Section 45).

## Execution Steps

1. **Contradiction Review:** compare every Discovery finding (Playbooks
   02–10) against Constitution Sections 5–37, all 10 ADRs, and every
   `Accepted`/`Confirmed` item in `.claude/context/*.md`. Log every
   contradiction found.
2. **Duplication Review:** check whether any two phases produced
   conflicting or duplicate definitions for the same concept (e.g., two
   different Bounded Contexts both claiming ownership of a term in
   `glossary.md`) — resolve by returning to the earlier phase, not by
   picking one arbitrarily here.
3. **DDD Consistency Review:** re-run the Quick Diagnostic (7-row
   checklist) across the full discovered model as a whole (Playbooks
   04–07's combined output), not per-Subdomain — checks for a
   platform-level "God model" pattern that no single phase could see.
4. **Full STRIDE Pass:** for every integration (Playbook 08) and AI use
   case (Playbook 10), complete the STRIDE analysis the first-pass in those
   phases started — Spoofing, Tampering, Repudiation, Information
   Disclosure, Denial of Service, Elevation of Privilege.
5. **Mitigation Mapping:** for every threat found in Step 4, map it to a
   mitigation category or log it as an explicitly accepted risk with a
   named owner (Constitution Section 37) — no unmitigated, unowned threat
   may pass this phase.
6. **Completeness Check:** for every item in `.claude/context/
   open-questions.md` that a Playbook 02–10 phase touched, confirm the
   phase report correctly reflects whether it is now Answered, Narrowed
   (still Open with evidence), or unchanged.
7. **Terminology Consistency Check:** every term appended to `glossary.md`
   across Playbooks 02–10 is checked for contradictory definitions between
   phases.
8. **Diagram Syntax Validation:** every Mermaid diagram produced across
   Playbooks 02–10 is checked for valid syntax (balanced brackets/quotes,
   correct diagram-type keyword, valid arrow syntax) before being
   considered ready for the Final Discovery Book.
9. **Reader Testing:** read the full Discovery narrative (Playbooks
   02→10's artifacts in order) as a single story and confirm it is
   coherent to a reader who was not present for any individual phase.

## Deliverables

- A single Validation Report covering all nine review dimensions above.
- A Contradiction/Duplication resolution list (each item: found, resolved
  how, or escalated).
- A complete STRIDE + mitigation-mapping record for every integration and
  AI use case.

## Produced Artifacts

- `docs/discovery/reports/11-validation-report.md`
- `docs/discovery/reports/11-stride-mitigation-mapping.md`

## Required Diagrams

None new — this phase validates diagrams already produced by Playbooks
02–10; a diagram found invalid is sent back to its originating phase for
correction, not redrawn here.

## Review Checklist

- [ ] Every contradiction found is either resolved (with the resolution
      documented) or escalated to the user — none silently dropped.
- [ ] Every STRIDE threat has a mapped mitigation or a named
      accepted-risk owner.
- [ ] Every diagram passes syntax validation.
- [ ] Every touched Open Question's status accurately reflects Playbook
      02–10 findings.
- [ ] The end-to-end Discovery narrative reads coherently (Reader Test
      passed).

## Quality Gates

- **Zero-Unmitigated-Threat Gate:** Constitution Section 37, applied at
  Discovery scale — no threat may reach Playbook 12 unmitigated and
  unowned.
- **Zero-Unresolved-Contradiction Gate:** no contradiction against an
  Accepted Constitution rule or ADR may reach Playbook 12 unresolved or
  unescalated.
- **Diagram Validity Gate:** 100% of produced diagrams pass syntax
  validation before Playbook 12 compiles them.

## Exit Criteria

- All nine review dimensions completed with their findings documented.
- No unresolved, unescalated contradiction remains.
- No unmitigated, unowned threat remains.

## Files To Update

- `.claude/context/open-questions.md` — final-pass accuracy correction if
  any Playbook 02–10 update was found inconsistent during this phase.

## ADR Impact

None directly authored here — this phase identifies which findings *should*
become ADRs (cross-referencing each phase's own "ADR Impact" section) and
hands a consolidated list to Playbook 12, which is where ADR authoring
actually happens.

## Common Mistakes

- Treating Validation as a formality/rubber stamp instead of genuinely
  re-running the checks — the entire point of this phase is to catch what
  no single earlier phase could see in isolation.
- Resolving a contradiction by quietly editing the Constitution or an ADR
  instead of escalating (Constitution Amendment is Section 45's exclusive
  process, never a side effect of a Discovery Validation pass).
- Marking a STRIDE threat as mitigated without a concrete mitigation
  category, just to close the checklist item.
- Skipping the Reader Test because "the content is technically correct" —
  technically correct and coherent-to-a-reader are different bars, and both
  are required for the Final Discovery Book to be usable.

## Self Review

Before declaring this phase complete, re-read the Validation Report's
Contradiction and STRIDE sections specifically and confirm every single row
has an explicit resolution or escalation status — an empty "resolution"
cell anywhere is itself a defect.

## Stop Conditions

- A contradiction against an Accepted Constitution rule or ADR cannot be
  resolved within this phase (it requires a genuine architectural or
  business decision) — stop, escalate to the user with the specific
  contradiction stated plainly, per Constitution Section 44.
- A STRIDE threat is identified with no available mitigation category and
  no willing risk owner — stop, do not let it pass silently; this blocks
  the affected integration/use case from being marked ready in Playbook 12.
