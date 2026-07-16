# Risk Analysis — Patient Registry / MPI

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Duplicate patient records accumulate across branches without MPI-grade matching | Medium (real risk, deliberately deferred) | Medium-High (clinical safety, billing accuracy) | OpenCR/HAPI MDM identified as the evidence-based upgrade path once duplication is actually measured — not resolved preemptively |
| Egypt National ID linkage (`open-questions.md` #27, Recommended not Confirmed) not yet incorporated into the FHIR-based identifier model | Medium | Medium | Flagged for the eventual SAD/Patient Aggregate design, not resolved here |
