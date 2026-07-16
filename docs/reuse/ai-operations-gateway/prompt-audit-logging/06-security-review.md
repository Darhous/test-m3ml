# Security Review — Prompt Audit Logging

Inherits both parent reviews. Additional concern: prompt/response logs
may themselves contain sensitive data if a use case's input included
patient context — logs must inherit the same RLS tenant isolation
(Module 2) as clinical data, not be treated as generic ops logs.
