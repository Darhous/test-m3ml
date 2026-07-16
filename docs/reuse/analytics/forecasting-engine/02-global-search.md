# Global Search Log — Forecasting Engine

**Query:** `open source time series forecasting library Prophet vs
statsmodels vs NeuralProphet 2026`

**Finding:** Prophet (Meta) remains "the better starting point" for most
applications per 2026 sources — faster to train, less prone to
overfitting on small/moderate datasets (this platform's evidenced
scale), principled Bayesian uncertainty quantification, built-in holiday/
seasonality handling relevant to Egypt-specific demand patterns.
NeuralProphet only wins on very small datasets in some benchmarks; ETS/
statsmodels wins when data is clean and regular (a stronger assumption
than this platform can currently make). No credible "buy" product beyond
libraries — this is a Library-scale decision, not an Engine/service.
