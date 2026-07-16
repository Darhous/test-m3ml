# Build vs. Buy — Tenant Provisioning

Not a product-adoption decision — the provisioning Saga itself is
necessarily platform-owned orchestration logic (it encodes this
platform's own specific business steps), calling into already-selected
Engines (Keycloak, PostgreSQL). No third-party "tenant provisioning
product" would fit a platform-specific onboarding sequence without being
effectively rebuilt anyway — correctly classified as BUILD for the
orchestration layer itself, while the underlying primitives are Reuse.
