# Architecture Review — LLM Gateway / Orchestration

Portkey's native guardrails (PII redaction, jailbreak/prompt-injection
detection) sit directly on the request path — a strong match for
Constitution Section 28's requirement that AI never independently
approve/modify results or expose sensitive data without approved policy.
LiteLLM's virtual-key/budget model is a better fit if per-Module usage
metering (cost attribution) is the dominant concern; Portkey's guardrails
are the better fit if governance/safety is dominant — this platform's
Constitution Section 28 weighting favors governance.
