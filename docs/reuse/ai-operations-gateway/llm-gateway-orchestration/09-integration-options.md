# Integration Options — LLM Gateway / Orchestration

Deployed as the sole ADR-0007 Independent Component chokepoint — every
Module's AI-assisted use case (Wave 10's 7 accepted use cases) calls
Portkey, never a model provider directly. Guardrail policies configured
per use case, cross-referencing OPA (Module 1) for any use case needing
deeper contextual policy beyond Portkey's built-in filters.
