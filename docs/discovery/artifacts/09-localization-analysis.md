# Localization Analysis (Discovery, Phase 09)

**Status: Draft — Assumption-Driven Autonomous Run.** Standalone summary;
full gap detail is in `09-tenancy-analysis.md`'s Localization Gaps table
(kept together with tenancy findings there since both surfaced from the
same per-Aggregate review pass).

## Summary

Reviewed every Phase 05 candidate Aggregate for hardcoded language/
currency/timezone assumptions, per Constitution Section 32 (Arabic/English,
RTL/LTR, Multi-Currency, Multi-Timezone, locale-aware formatting — already
Accepted, ADR 0010). Found 2 concrete gaps (Invoice's `Amount` field lacking
currency; `DeviceImportRecord`'s `timestamp` lacking timezone context) and
1 general pattern gap (timestamps platform-wide not yet explicitly modeled
with timezone awareness).

## What Was NOT Found

No Aggregate hardcoded a specific language, currency, or timezone value —
the gaps found are *omissions* (fields that need locale-awareness added),
not *violations* (a field that actively assumes a single locale). This is
a meaningfully better finding than the alternative — it means Phase 05's
candidate modeling was locale-neutral by omission rather than locale-biased
by design, which is easier to complete correctly later.

## Recommendation

Carry the `Money` Value Object pattern (`{amount, currencyCode}`) and the
dual-timestamp pattern (`{localTimestamp, timezoneRef,
platformTimestamp}`) forward as standing modeling conventions for any
future Aggregate design, not just the two instances found here — apply
proactively in Phase 12's consolidation pass and flag for the future SAD.
