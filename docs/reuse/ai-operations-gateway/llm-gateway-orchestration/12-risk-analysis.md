# Risk Analysis — LLM Gateway / Orchestration

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Portkey's shorter full-OSS history hides an immature edge case | Low-Medium | Medium | LiteLLM fallback identified; monitor Portkey's post-March-2026 stability track record before final commitment |
| A Module bypasses the Gateway and calls a model provider directly | Low (architectural discipline) | High (Constitution Section 28 violation) | Network-level egress restriction to only the Gateway — an SAD/infra decision, flagged here |
| Guardrails alone do not resolve Risk #18/SEC-05 (AI notification summarization) | Certain (guardrails are a partial mitigation, not full closure) | Medium-High | Still requires the human-review-step product decision flagged since Baseline Phase 10 |
