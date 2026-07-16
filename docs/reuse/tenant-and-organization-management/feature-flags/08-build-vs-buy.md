# Build vs. Buy — Feature Flags

| Dimension (Weight) | Unleash | Flagsmith | Build In-House |
|---|---|---|---|
| Architecture (15%) | 5 | 4 | 2 |
| Security (15%) | 4 | 4 | 1 |
| License (10%) | 5 (OSS edition) | 5 | 5 |
| Testing/CI (10%) | 4 | 4 | 1 |
| Community Health (10%) | 5 | 4 | N/A |
| Enterprise Adoption (10%) | 5 — named regulated/public-sector adopters | 4 | 0 |
| Healthcare Suitability (10%) | 4 — governance/audit features suit a regulated platform | 3 | Unknown |
| Documentation (5%) | 4 | 4 | Unknown |
| Extensibility (5%) | 4 | 4 | 5 (at cost) |
| Upgradeability (5%) | 4 | 4 | Unknown |
| Vendor Independence (5%) | 4 — open-core, OpenFeature-compatible exit path | 4 — same | 5 |

**Weighted totals:** Unleash **4.5**, Flagsmith **4.0**, Build In-House
**~1.7**.

## Conclusion

**Unleash** — governance/audit-trail features are the deciding factor
for a platform where feature-gating decisions may need the same
traceability as other Sensitive-Operation-adjacent actions (Wave 6's
candidate Elevated Audit tier). Flagsmith remains a credible alternative,
particularly if the `tenant-configuration` Feature's remote-config need
ends up dominant (see that Feature's own files).
