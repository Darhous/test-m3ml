Kill Bill's usage-tracking primitives feed entitlement checks (e.g., is
this tenant's plan tier entitled to feature X, has this tenant exceeded
its metered specimen-volume allowance) — gated through OPA (Module 1)
for the actual access-control decision, with Kill Bill as the source of
truth for plan/usage state.
