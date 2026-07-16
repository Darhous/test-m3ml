# Risk Analysis — Consent Management

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Consent status check bypassed by a Module that doesn't call the shared OPA evaluation | Medium | High (privacy/legal) | Constitution Section 8 (One Owning Module) + Backend-Enforced (Section 21) discipline — every data-sharing action must route through the check, an implementation-time enforcement requirement flagged here |
| Egypt PDPL 151/2020's actual consent requirements (Wave 11, `open-questions.md` #25, `Requires Legal Verification`) differ materially from the FHIR-generic model | Medium | Medium | The FHIR shape is a starting Reference, not a legal-compliance guarantee — must be reviewed against real PDPL text before being treated as sufficient |
