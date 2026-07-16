# Final Decision — Feature Flags

## Decision: **ENGINE + ADAPTER**

**Engine:** Unleash (Apache-2.0 OSS edition).
**Adapter:** platform code evaluates flags via the OpenFeature (CNCF)
vendor-neutral SDK, with Unleash configured as the backing provider —
avoiding direct vendor lock-in to Unleash's own SDK surface.

## Why Not Flagsmith

Close second (weighted 4.0 vs. 4.5). Unleash's built-in change-approval
governance and audit logging are a better match for this platform's
Sensitive-Operation-adjacent gating needs; Flagsmith remains the stronger
choice specifically for the `tenant-configuration` Feature's remote-
config need (see that Feature) — noted as a real possibility that the
platform ends up using Flagsmith there instead, which would not
contradict this decision since both implement OpenFeature.
