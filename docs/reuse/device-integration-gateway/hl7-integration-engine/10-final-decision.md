# Final Decision — HL7 Integration Engine

## Decision: **ENGINE + ADAPTER, with an explicit caveat**

**Recommended (not high-confidence):** Mirth Connect 4.5.2 (last OSS
release, MPL 2.0), specifically **because** of its healthcare-purpose
fit — but flagged with the same "reconsider at SAD time" caveat given to
`compliance-tracking` (Module 3), since its frozen-security status is a
real, ongoing risk, not a one-time cost. **Apache Camel is a credible,
actively-maintained fallback** if the frozen-engine risk is judged
unacceptable at SAD time — costs more integration engineering but removes
the patch-freeze risk entirely.
