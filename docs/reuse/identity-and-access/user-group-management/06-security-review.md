# Security Review — User and Group Management

Directly relevant findings already logged in `../authentication/
06-security-review.md`: **CVE-2025-14777** (IDOR in realm client
creation/deletion) and **CVE-2026-3121** (privilege escalation via
manage-clients permission) are both administrative-surface
vulnerabilities of exactly this Feature's kind — cross-referenced, not
re-researched. Reinforces the same patch-cadence mitigation.
