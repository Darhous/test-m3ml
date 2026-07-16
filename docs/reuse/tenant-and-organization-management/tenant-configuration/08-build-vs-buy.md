# Build vs. Buy — Tenant Configuration

**Hybrid, evidence-based, not a default:** reusing Unleash for simple
config avoids a second engine (this program's own duplicate-elimination
objective); BUILD for complex structured config avoids forcing an
ill-fitting tool onto a use case it wasn't designed for. Introducing
Flagsmith solely for this Feature was rejected — its marginal advantage
(native combined flags+config model) does not outweigh the cost of
operating two flag platforms for one platform's needs.
