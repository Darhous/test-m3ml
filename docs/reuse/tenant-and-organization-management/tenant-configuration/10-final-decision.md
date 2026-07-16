# Final Decision — Tenant Configuration

## Decision: **ENGINE + ADAPTER (Unleash, shared with `feature-flags`) + BUILD (for complex structured config)**

No new engine introduced. Flagsmith explicitly considered and rejected
for this Feature specifically to avoid operating two flag/config
platforms — a direct application of the program's Cross-Feature
Dependency / duplicate-elimination principle, even though Flagsmith's
own design fits this Feature's description slightly better in isolation.
