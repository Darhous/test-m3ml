# Integration Options — AI Use Case Governance

Every AI request passes: Portkey guardrails → OPA use-case policy check
→ model call (if allowed) → response through Portkey guardrails again →
`prompt-audit-logging` pipeline.
