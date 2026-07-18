# API Catalog

## Purpose

`03-API-DOMAIN-INVENTORY.md` is this Board's own point-in-time,
document-form inventory of every Module's API classification. The API
Catalog is the **living, queryable system** that inventory implies is
needed once the platform has dozens of Published contracts across 28
Modules — it does not replace `03`, it operationalizes it. This
document does not duplicate `03`'s content; it specifies the Catalog's
structure and behavior.

## Catalog

Every Published contract (OpenAPI or AsyncAPI, `16`–`18`) is registered
in the Catalog with, at minimum: owning Module (`04-API-GOVERNANCE.md`'s
Ownership model), API type (`03`'s seven-type classification),
lifecycle stage (`04`'s Draft/Published/Deprecated/Retired), current
version (`07-VERSIONING.md`), and a link to its Interactive Docs entry
(`22-DEVELOPER-PORTAL.md`). The Catalog is generated from the
Published contracts themselves (the same source-of-truth discipline as
`20`'s SDKs and `22`'s Interactive Docs) — never hand-maintained
separately, which would let it drift from what is actually deployed.

## Discovery

A developer (internal or, once certified, Partner) can search the
Catalog by Module, resource name (Ubiquitous-Language-consistent per
`06-NAMING-CONVENTIONS.md`), API type, or lifecycle stage. This is the
mechanism that closes OWASP API9 (Improper Inventory Management,
`11-API-SECURITY.md`) at the *operational* level — `03` closes it at
the *document* level, the Catalog closes it at the *runtime* level, so
"what APIs exist and who owns them" never depends on this document set
staying manually current.

## Ownership

Reuses `04-API-GOVERNANCE.md`'s Ownership model exactly — the Catalog
displays, never redefines, the owning Module for each entry. A Catalog
entry with no resolvable owning Module is treated as a governance
defect (an API that reached Published without going through
`04`'s Approval Workflow) and is flagged, not silently listed.

## Lifecycle

The Catalog is the canonical, queryable record of every contract's
current lifecycle stage (`04-API-GOVERNANCE.md`). A contract entering
Deprecated status automatically surfaces its retirement date and
replacement-version pointer (`07-VERSIONING.md`) in the Catalog — this
is how a consuming team actually discovers an upcoming breaking change,
rather than relying on being personally notified. Retired contracts
remain in the Catalog (archived, not deleted, per
`17-OPENAPI-GOVERNANCE.md`'s Version Governance) for historical
traceability.

## Classification

Every Catalog entry carries the same seven-type classification as
`03-API-DOMAIN-INVENTORY.md` (Internal/External/Partner/Public/Admin/
Integration/Future), plus one additional Catalog-specific facet not
needed in a static document but necessary in a live system: **exposure
surface** — which Catalog entries are reachable through the Edge
Gateway (External/Partner/Public/Admin) versus Internal-only
(`02-API-FIRST-ARCHITECTURE.md`'s Boundary Rules). This lets the
Catalog itself be used as an automated check that no Internal API has
been accidentally Gateway-exposed — a structural verification of a
rule `02` states as policy.

## Relationship to the Developer Portal and Marketplace

The Catalog is the **data source**; `22-DEVELOPER-PORTAL.md` is the
**internal/Partner-facing presentation** of Published, non-Future
entries; `24-MARKETPLACE.md` is a **further-filtered, commercially-
packaged presentation** of specifically the API Products a Tenant/
Partner has chosen to publish. One source of truth, three audiences —
this document does not introduce a second inventory mechanism at any
of those layers.
