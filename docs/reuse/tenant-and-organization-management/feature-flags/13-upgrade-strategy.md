# Upgrade Strategy — Feature Flags

Because the platform's own code targets the OpenFeature SDK rather than
Unleash's proprietary SDK, an Unleash version upgrade — or a future
provider swap — is contained to the provider-configuration layer.
Recommended posture: track Unleash's own release notes for the OSS
edition; monitor for any feature migrating from OSS to Enterprise-only
tier over time (open-core products occasionally do this), re-evaluating
license compatibility if it happens.
