# Feature: Worklist Management

**Module:** Laboratory Execution (Business Module, Core-adjacent).
Assignment and sequencing of accessioned specimens to benches/analyzers
for processing (Wave 3/6 "Worklists, Benches"). Sits directly inside the
Core Domain chain: Order → Specimen → **Execution** → Result Verification
→ Report (ADR-0011 Amended, "Patient-to-Result Orchestration").

This Feature carries the program's twice-deferred decision (Modules 12
and 13): whether to adopt a mature open-source LIMS (SENAITE, OpenELIS
Global) as the Laboratory Execution engine, or continue the
REFERENCE + BUILD pattern already applied to every other Feature in this
Core Domain chain. That decision is made explicitly here, not deferred
further — see `10-final-decision.md`.
