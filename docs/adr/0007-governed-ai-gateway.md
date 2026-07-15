# 0007: Governed AI Gateway

## Status

Accepted

## Context

The platform's direction includes being "AI-Ready" (vision.md) and using AI
for summarization, pattern detection, search, operational assistance, and
clinical decision support. Because the platform handles highly sensitive
medical data (`constraints.md` #5) and AI must never issue a final,
unreviewed medical decision (`constraints.md` #6, CLAUDE.md Rule 15), AI
functionality cannot be embedded ad hoc inside arbitrary modules without a
consistent governance, audit, and human-review mechanism.

## Decision

AI is implemented as an **independent, governed AI Gateway** (one of the
Independent Components, Constitution Section 11). It may support
Summarization, patient-friendly explanations, pattern detection, anomaly
detection, search, operational assistance, and clinical decision *support*.
It may not independently approve medical results, modify verified medical
results, publish a final diagnosis, or send a final medical decision
without human review. Human-in-the-Loop is mandatory for sensitive clinical
actions. Every AI action (prompt, model/version, output, cost, evaluation,
provider) is logged and auditable. Sending sensitive information to an
external AI provider requires an approved policy and controls first.

## Alternatives Considered

- **AI embedded directly inside individual modules with no central
  gateway.** Rejected: makes consistent governance (audit logging,
  Human-in-the-Loop gating, external-provider data controls) impossible to
  enforce uniformly — each module would need to reinvent these controls,
  risking gaps.
- **Fully autonomous AI actions on medical data, with human review only on
  exception/appeal.** Rejected outright: directly violates the explicit
  constraint that AI must never issue a final, unreviewed medical decision.
- **Independent, governed AI Gateway with mandatory Human-in-the-Loop for
  sensitive actions and full action auditability.** **Chosen.** Matches the
  "AI-Ready" vision while enforcing the human-review constraint
  structurally, not just by policy document.

## Positive Consequences

- A single place to enforce AI governance controls (Human-in-the-Loop
  gating, audit logging, external-provider data policy) rather than
  N ad-hoc implementations.
- Clear, auditable boundary between "AI suggested" and "human approved,"
  which directly supports both patient safety and future compliance
  reviews (Constitution Section 31, without claiming compliance itself).
- New AI-assisted features can be added behind the same governance gate
  without re-deriving the safety controls each time.

## Negative Consequences

- Every sensitive AI-assisted feature requires building/using the
  Human-in-the-Loop review step, which is extra product/UX work compared
  to a naive "just show the AI output" approach.
- Centralizing AI access adds an operational dependency that AI-assisted
  features rely on.

## Risks

- **Human-in-the-Loop gate bypass**: a feature reaches a "final" state from
  an AI suggestion without genuine human review. Mitigated by dedicated
  gate tests (Constitution Section 28) attempting exactly this and
  asserting it is blocked.
- **Sensitive data sent to an external AI provider without an approved
  policy.** Mitigated by a policy-gate check required on any outbound call
  carrying sensitive data (Constitution Section 28).

## Verification

- Human-in-the-Loop gate tests (attempt to finalize a sensitive AI output
  without human approval; must be blocked).
- AI action audit-log completeness check.
- Policy-gate check on outbound calls to external AI providers with
  sensitive data.

## Revisit Triggers

- Specific AI-assisted functions prove to need a different governance
  shape (e.g., a fully non-sensitive, non-clinical use case that does not
  need Human-in-the-Loop) — handled as a scoped classification refinement
  within this Gateway, not a reversal of the mandatory gate for sensitive
  actions.
- Answers to `open-questions.md` #11 (AI usage limits) may refine, but not
  loosen, the "no autonomous final medical decision" constraint without a
  superseding ADR and explicit user approval.
