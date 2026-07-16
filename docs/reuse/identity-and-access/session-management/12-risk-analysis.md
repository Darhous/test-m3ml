# Risk Analysis — Session Management

Inherits `../authentication/12-risk-analysis.md`. Feature-specific: an
overly long session/refresh-token expiry configuration would widen the
window of exposure for a stolen token — an SAD/configuration-level
decision, not resolved here, but flagged so it is not silently defaulted.
Likelihood: Medium. Impact: Medium.
