# Master Cross-Feature Dependency Map

Detects repositories that solve **multiple** Features at once, so research
is never duplicated. When a candidate reappears in a later Feature's
research, this file is checked first and the entry is cross-referenced,
not re-derived. Example (from the program's own instructions): Keycloak
solves Authentication, Authorization, SSO, MFA, Session Management, and
Audit-adjacent identity events — one adoption decision, five Feature
entries pointing back to it.

| Repository | Features It Solves | Modules | Single Adoption Point (which Feature owns the decision) |
|---|---|---|---|
