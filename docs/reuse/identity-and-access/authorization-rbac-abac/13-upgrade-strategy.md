# Upgrade Strategy — Authorization (RBAC/ABAC)

OPA ships policy bundles independently of the OPA engine binary itself —
this means the platform's own Result Verification Policy Model rules can
be versioned and deployed on a different cadence than OPA engine upgrades
(directly serving Constitution Section 48's Versioning Policy and Wave
6's requirement that verification policy be "Versioned"). Recommended
posture: track OPA's own release cadence for engine security patches
separately from the platform's own policy-bundle release cadence, using
OPA's native bundle-signing feature to guarantee only an approved policy
version is ever evaluated in production. Exact SLA/cadence numbers are an
SAD-level decision, not invented here.
