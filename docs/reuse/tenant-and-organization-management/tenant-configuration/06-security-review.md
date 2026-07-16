# Security Review — Tenant Configuration

Inherits `../feature-flags/06-security-review.md` for the Unleash-backed
portion. The platform-owned tenant-settings table inherits this Module's
RLS-based isolation (`multi-tenancy-isolation`) — no new security surface
beyond already-reviewed components.
