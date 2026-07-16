# Risk Analysis — Authentication

| Risk | Likelihood | Impact | Mitigation | Cross-Reference |
|---|---|---|---|---|
| Un-patched Keycloak CVE reaches production (real, recurring pattern per `06-security-review.md`) | Medium (frequent point releases mean frequent patch obligations) | High — Identity and Access is a universal dependency; a breach here compromises every Module | Formal patch-cadence commitment (subscribe to Keycloak security advisories, patch within a defined SLA — SLA number itself is an SAD-level decision, not invented here) | Discovery Risk Register #14/SEC-01 (DoS), #17/SEC-04 (tenant isolation) |
| Keycloak's Organizations feature does not, by itself, resolve `open-questions.md` #15 (shared-tier partitioning mechanism) | Certain (it is a tooling option, not a decision) | High — Risk Register #17, Highest severity, remains open regardless of this Feature's decision | This Feature's adoption must not be read as silently resolving #15 — flagged explicitly here so a future SAD reader does not assume it was | Risk Register #17 |
| AGPL-adjacent confusion if a future contributor mistakenly evaluates a Zitadel-derived customization | Low | Medium (legal) | This document's explicit rejection rationale (`10-final-decision.md`) should be cited if Zitadel is ever reconsidered | `04-license-review.md` |
| Vendor/community drift (Red Hat/IBM deprioritizing Keycloak) | Low — CNCF governance is a specific mitigation already in place | High if it occurred | CNCF incubation means the project does not depend solely on one company; monitor CNCF graduation status as a positive signal | `07-community-review.md` |
| Full custom White-Label theming (Wave 1 requirement) may exceed Keycloak's theming engine's easy customization ceiling | Medium | Low-Medium (cosmetic, not functional) | Flagged for SAD-level UI evaluation, not resolved here | `11-reusable-assets.md` |

## Overall Risk Rating for This Decision

**Medium** — the decision itself is low-risk (mature, evidenced choice),
but it inherits and does not resolve one Highest-severity Discovery risk
(#17) and introduces one recurring operational obligation (patch
cadence) that must be explicitly budgeted, not assumed away.
