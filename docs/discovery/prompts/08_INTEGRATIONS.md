# Playbook 08 — Integrations Discovery

**Playbook Type:** Reusable Enterprise Discovery Methodology
**Phase:** 7 of 11 domain-content phases
**Depends On:** Playbook 06 (Bounded Contexts and their external-facing
boundaries), Playbook 07 (Business Rules, for which rules apply at each
boundary)
**Produces For:** Playbook 09 (SaaS Platform Discovery, for tenant-facing
integration implications), Playbook 10 (AI Discovery, which is a
specialized case of this playbook for the AI Gateway boundary specifically),
Playbook 11 (Validation runs STRIDE over every integration surfaced here)

---

## Purpose

Discover and document every external integration surface the platform
needs: medical devices, external API partners, legacy systems, notification
channels, and any other boundary crossing outside the platform's own
Bounded Contexts — applying Constitution Section 24 (Medical Device
Integration Rules) and the Anti-Corruption Layer requirement from Section 6.

## Scope

**In scope:** device integration surfaces (protocols, vendors, failure
modes per Constitution Section 24), external API partner integrations,
legacy system integration needs (`open-questions.md` #13), notification
channel candidates (`open-questions.md` #10), file-based integration needs
(Constitution Section 27), and the Anti-Corruption Layer design for each.

**Out of scope:** the AI Gateway boundary specifically (Playbook 10 owns
that, as a specialized integration with its own governance depth); internal
Bounded Context relationships (already covered by Playbook 06's Context
Map); notification *content*/Data Scope rules in detail (Constitution
Section 26 governs that at implementation time — this phase identifies the
channel candidates only).

## Inputs

- `docs/discovery/artifacts/06-context-map.md`
- `docs/discovery/artifacts/07-business-rules-catalog.md`
- `docs/constitution/PROJECT-CONSTITUTION.md` Section 24 (Medical Device
  Integration Rules), Section 27 (File and Document Rules), ADR 0006
  (Independent Device Gateway)
- `.claude/context/open-questions.md` items 5 (device types), 10
  (notification channels), 13 (legacy migration)

## Preconditions

- Playbook 06 and 07 marked complete.

## Required Skills

- `domain-driven-design` — Anti-Corruption Layer and Context Mapping
  (Conformist, Open Host Service + Published Language patterns, applied to
  genuinely external systems this time, not internal contexts).
- `stride-analysis-patterns` — early threat surface identification for
  every new external boundary (full STRIDE review is Playbook 11's job;
  this phase does a first pass to make sure integration design accounts for
  obvious threats from the start).
- `c4-architecture` — Container/Component-level diagrams showing each
  integration's place in the platform.

## Required Context Files

`open-questions.md`, `constraints.md`, `stakeholders.md` (External API
Partners, Device Integration Teams categories).

## Project Bindings (this project)

- Every device integration surfaced here is owned by the Device Integration
  Gateway (Independent Component, Constitution Section 11, ADR 0006) — this
  phase identifies *what* needs integrating, not a redesign of the Gateway
  itself.
- Every finding here must respect Constitution Section 24's requirement
  that a device/adapter failure never corrupts core business data.

## Execution Steps

1. From the Context Map (Playbook 06), list every Bounded Context boundary
   that touches something outside the platform's own contexts.
2. For each device integration candidate, document: protocol/technology
   category (HL7/HL7v2/FHIR/ASTM/TCP-IP/Serial/File-Based/Vendor API — per
   Constitution Section 24's readiness list), vendor category (not a
   specific product), data imported, and required provenance fields.
3. For each device integration, do a first-pass failure-mode analysis: what
   happens if this device sends malformed data, stops responding, or sends
   duplicate data — cross-checked against Constitution Section 24's
   "failures isolated, logged, surfaced for review" rule.
4. For each external API partner integration, document: direction
   (inbound/outbound), data exchanged, and which Context Mapping pattern
   applies (usually Anti-Corruption Layer or Open Host Service + Published
   Language, per Playbook 06's established patterns).
5. For legacy system integration needs (`open-questions.md` #13), document
   what is known; if nothing concrete is known yet, explicitly state so
   rather than inventing a legacy system profile.
6. For notification channels (`open-questions.md` #10), list candidate
   channels the business actually needs (from Playbook 02's stakeholder
   needs and Playbook 03's events implying a notification), not a generic
   "all channels" list.
7. Run a first-pass STRIDE sweep (`stride-analysis-patterns`) across every
   integration surfaced — full mitigation mapping is Playbook 11's job;
   this phase flags obvious threats (e.g., Spoofing risk on an unauthenticated
   device protocol) so the integration's design doesn't ignore them from day
   one.

## Deliverables

- Integration inventory: devices, external API partners, legacy systems,
  notification channels, each with a first-pass failure-mode/threat note.
- Anti-Corruption Layer design note per integration.

## Produced Artifacts

- `docs/discovery/artifacts/08-integration-inventory.md`
- `docs/discovery/reports/08-integrations-report.md` (first-pass STRIDE
  findings, open items for `open-questions.md` #5/#10/#13)

## Required Diagrams

- C4 Container diagram showing the Device Integration Gateway and its
  adapters relative to business Bounded Contexts (`c4-architecture`).
- Mermaid `flowchart` per integration showing the Anti-Corruption Layer
  boundary explicitly (matching the style of Constitution Section 24's
  existing diagram).

## Review Checklist

- [ ] Every integration has an assigned Context Mapping pattern.
- [ ] Every device integration has a documented failure-mode note.
- [ ] No integration was designed to write directly into a Bounded
      Context's owned schema, bypassing the Gateway/ACL.
- [ ] Notification channel candidates are evidence-based (traced to a
      stakeholder need or event), not a generic exhaustive list.

## Quality Gates

- **Anti-Corruption Layer Gate:** every external-system boundary has an
  explicit ACL note before Exit — no boundary left "to be designed later"
  without at least a placeholder ACL responsibility statement.
- **First-Pass STRIDE Gate:** every integration has at least one STRIDE
  category considered (even if the finding is "no significant threat
  identified at this stage, re-verify in Playbook 11").

## Exit Criteria

- Integration inventory complete for every boundary identified in Playbook
  06's Context Map.
- First-pass STRIDE notes exist for every integration, ready for Playbook
  11's full mitigation-mapping pass.

## Files To Update

- `.claude/context/open-questions.md` — update items 5, 10, 13 with
  Discovery findings (status remains `Open` unless the user gives a
  definitive answer during this phase, in which case follow that item's own
  "move to Answered" procedure).

## ADR Impact

A newly identified integration category not already covered by Constitution
Section 24's protocol-readiness list, or a notification channel decision
that becomes Accepted, may warrant an ADR at Playbook 12. Routine
integrations already anticipated by ADR 0006 do not need a new ADR — they
are implementations of an existing Accepted decision.

## Common Mistakes

- Designing a device adapter to also contain business/domain logic
  (explicitly forbidden by Constitution Section 24).
- Treating "we don't have device details yet" as a reason to invent
  plausible-sounding device types instead of leaving the item `Open`.
- Skipping the first-pass STRIDE sweep because "full security review comes
  later" — the point of the first pass is to avoid designing an integration
  that later fails Playbook 11 outright.
- Listing every conceivable notification channel instead of the ones
  actual stakeholder needs from Playbook 02 imply.

## Self Review

For each integration, re-read its failure-mode note and ask: "if this
external system is malicious or simply broken, can it corrupt core
business data?" If the answer is unclear, the Anti-Corruption Layer design
is incomplete.

## Stop Conditions

- An integration cannot be given any Context Mapping pattern because its
  data flow direction/ownership is unclear — return to Playbook 06 to
  clarify the relevant Context boundary rather than guessing a pattern.
- A proposed integration would require a device adapter or external
  partner to write directly into a Bounded Context's schema — stop, this
  violates Constitution Section 16/24 and must be redesigned, not accepted
  as an exception without going through Section 44.
