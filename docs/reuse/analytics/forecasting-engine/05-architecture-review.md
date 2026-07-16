# Architecture Review — Forecasting Engine

Prophet is a Python library, not a service — runs as a batch/scheduled
job (e.g., nightly demand-forecast recompute) reading from PostgreSQL
and writing forecast results back for Superset to visualize. No new
deployed component beyond the platform's existing stack. This is
consistent with Wave 3's own "speculative" flag on Forecasting/
Predictive Maintenance — a low-infrastructure-cost way to keep the
option open without committing to a heavy ML platform prematurely.
