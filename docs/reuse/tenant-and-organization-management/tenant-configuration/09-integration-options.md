# Integration Options — Tenant Configuration

Simple config values: Unleash variant payloads, evaluated via the same
OpenFeature adapter as `../feature-flags/`. Complex structured config
(White-Label theming, future-market localization bundles): a
platform-owned, RLS-isolated `tenant_settings` table, read through the
Tenant and Organization Management Module's own API — not exposed
directly to other Modules (Constitution Section 8).
