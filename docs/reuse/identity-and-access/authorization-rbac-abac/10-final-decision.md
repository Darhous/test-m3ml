# Final Decision — Authorization (RBAC/ABAC)

## Decision: **ENGINE + ADAPTER (dual-engine, two-layer)**

- **Coarse RBAC:** Keycloak Roles/Groups (already adopted — no separate
  decision needed, see `../authentication/10-final-decision.md`).
- **Fine-grained ABAC/Policy:** **Open Policy Agent (OPA)**, CNCF
  Graduated, Apache-2.0, integrated as a sidecar/library called only by
  the Result Verification and Reporting Module (and any future
  "Elevated Audit" tier consumer, pending `open-questions.md` #24).

## Why Not Casbin

Close second (weighted score 4.1 vs. OPA's 4.7). Casbin's simpler model
and lower learning curve are genuine advantages, but OPA's CNCF Graduated
governance status and native decision-audit logging are a stronger match
for a Sensitive-Operation-grade, Audit-mandatory Feature specifically —
Casbin remains a credible fallback if OPA's Rego learning curve proves a
real adoption obstacle at SAD time (flagged, not decided, here).

## Why Not Extending Keycloak Authorization Services

Would avoid adding a second engine, but scored lowest of the 3 real
candidates on Architecture fit — UMA's model was not designed for this
level of multi-dimensional business-rule expressiveness, and forcing the
Policy Model into it risks turning into a de facto Build decision wearing
an Engine's clothing (custom policy-provider code eroding the reuse
benefit this program exists to capture).
