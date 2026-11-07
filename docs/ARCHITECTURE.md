# Proposed technical architecture

```text
Permitted API/export
   ↓
Python adapter (provenance, timestamps, retries, checkpoint)
   ↓
Bronze: raw source snapshots
   ↓
Silver: normalized products, sets and price observations
   ↓
Gold: card-day prices, coverage and point-in-time feature tables
   ↓
Python: EDA → naive baseline → XGBoost → optional SARIMAX
   ↓
Chronological backtesting + uncertainty calibration
   ↓
Power BI + technical case study
```

## Storage decision
**MVP:** SQL Server as the authoritative warehouse; pandas, scikit-learn, XGBoost and statsmodels for analysis. **Extension:** Databricks Delta Bronze/Silver/Gold, Jobs and MLflow after the MVP works. Avoid maintaining two inconsistent authoritative stores.

## Data contracts
A price observation must preserve provider, product ID, product variant/condition, price type (market/listing/sold), currency, observation timestamp and ingestion timestamp. Do not combine asking prices and executed transactions without explicit transformation.

## Orchestration and compliance
Use incremental watermarks, idempotent upserts, structured logs, retry limits and quality checks. Set cadence and request volume only after confirming provider permissions; do not bypass rate limits, CAPTCHAs or access restrictions.

## Quality and security
Validate uniqueness, positive prices, currency, timestamps, freshness, referential integrity, missingness and anomalies. Store secrets outside the repository. Keep immutable raw snapshots where licensed, so transformations can be replayed.

## Dependencies and risks
Data rights and historical depth are not yet established. A new anniversary release may require training on older sets. Market prices do not prove retail demand, inventory needs or margin optimization.
