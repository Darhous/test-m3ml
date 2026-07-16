# Architecture Review — Tenant Configuration

Running both Unleash and Flagsmith simultaneously would duplicate a
Platform Kernel component — directly against this program's own
duplicate-elimination objective. Recommended resolution: use Unleash
(already selected in `../feature-flags/`) for simple per-tenant config
values expressible as strategy-variant payloads; reserve a platform-owned
tenant-settings table (BUILD) for complex structured config (e.g.,
White-Label theme objects with many nested fields) that would strain a
flag engine's payload model. This avoids introducing Flagsmith as a
second engine while still not forcing an ill-fitting use of Unleash.
