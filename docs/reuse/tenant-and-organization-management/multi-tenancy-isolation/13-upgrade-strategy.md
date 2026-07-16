# Upgrade Strategy — Multi-Tenancy Isolation

Not an "upgrade" in the product-version sense (no third-party product
adopted). The relevant forward-looking consideration is **migration
between tiers**: if a Shared-tier tenant is promoted to Dedicated tier
(`open-questions.md` #16, trigger type still Open), the RLS-based data
must be extracted and migrated into that tenant's dedicated database —
a bounded, well-understood migration pattern (export rows matching
`tenant_id`, import into the new dedicated instance), not a rearchitecture.
This bounded-migration property is a further point in RLS's favor as the
Shared-tier Reference pattern.
