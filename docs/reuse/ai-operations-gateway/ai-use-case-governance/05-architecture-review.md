# Architecture Review — AI Use Case Governance

Two-layer: Portkey's built-in guardrails handle generic PII/jailbreak
filtering at the request level; OPA (already integrated for Result
Verification and Governance policy, Modules 1/3) evaluates the specific
"is this use case Permitted for this context" decision against
Constitution Section 28's list — a third confirmed OPA consumer.
