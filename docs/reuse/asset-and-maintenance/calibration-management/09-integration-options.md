Separate data domain from Module 14's `calibration-tracking` (analyzer/
QC-tied); both may reference the same physical Analyzer entity but
through different Aggregates — flagged for explicit disambiguation at
SAD time to avoid confusion, not treated as a duplicate to consolidate.
