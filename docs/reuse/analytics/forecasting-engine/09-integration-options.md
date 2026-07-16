# Integration Options — Forecasting Engine

Scheduled batch job (frequency TBD at SAD time) reads historical
Inventory/Workforce data from PostgreSQL, runs Prophet, writes forecast
results to a dedicated table for Superset (`bi-dashboards`) to visualize
— no real-time inference path needed for this use case.
