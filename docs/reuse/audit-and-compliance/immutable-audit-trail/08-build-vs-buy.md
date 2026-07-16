# Build vs. Buy — Immutable Audit Trail

| Dimension (Weight) | immudb | Trillian | PostgreSQL append-only (Build) |
|---|---|---|---|
| Architecture (15%) | 5 | 4 | 2 |
| Security (15%) | 5 — cryptographic tamper-evidence, holds even against a malicious DBA | 5 — same property | 2 — access-control only, no cryptographic guarantee |
| License (10%) | 5 | 5 | 5 |
| Testing/CI (10%) | 4 | 4 | 1 |
| Community Health (10%) | 4 | 4 | N/A |
| Enterprise Adoption (10%) | 4 — explicit 2026 healthcare framing | 3 — different use-case profile (CT-scale) | 0 |
| Healthcare Suitability (10%) | 5 — purpose-marketed for this exact scenario | 3 | 1 |
| Documentation (5%) | 4 | 4 | Unknown |
| Extensibility (5%) | 4 — SQL layer aids integration | 3 | 5 (at cost) |
| Upgradeability (5%) | 4 | 4 | Unknown |
| Vendor Independence (5%) | 3 — company-led, open-core | 5 — Google-originated but broadly community-operated | 5 |

**Weighted totals:** immudb **4.5**, Trillian **3.9**, Build (Postgres
append-only) **~2.2**.

## Conclusion

**immudb** — the only candidate offering cryptographic tamper-evidence
*and* a familiar SQL query surface *and* an explicit, current
healthcare-compliance framing from its own maintainers. Trillian remains
a credible fallback if immudb's open-core commercial trajectory ever
becomes a concern (flagged in `13-upgrade-strategy.md`).
