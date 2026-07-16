# Final Decision — ASTM Integration

## Decision: **ENGINE + ADAPTER (shared base engine) + BUILD (protocol-specific parsing)**

Follows `../hl7-integration-engine/10-final-decision.md`'s engine choice;
ASTM-specific parsing logic is platform-owned regardless, given the weak
native tooling on both candidates.
