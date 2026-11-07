# Project roadmap and acceptance criteria

**Workflow:** Backlog → Ready → In Progress → Review → Done. Use GitHub Issues for deliverables and PRs for implementation. Each phase is complete only when its acceptance criteria can be reproduced.

## 01 — Project scope and data feasibility
- [ ] Confirm exact anniversary products and whether analysis includes singles, sealed products, or both.
- [ ] Identify authorized data sources, coverage, usage rights, price definitions and available sale counts.
- [ ] Fix target currency, condition, printing, 7/30-day horizons and future-label matching rules.
- [ ] Assess whether older sets provide enough training history.
**Done when:** source inventory, sample dataset, target definition, and risks are documented.

## 02 — Ingestion
- [ ] Implement approved Python source adapter with bounded retries, logging, timestamps and checkpoints.
- [ ] Preserve raw snapshots, source provenance and deterministic deduplication keys.
- [ ] Run incremental loads without duplicate observations.
**Done when:** repeated ingestion is reproducible and source permissions are documented.

## 03 — SQL Server warehouse
- [ ] Bronze immutable raw observations.
- [ ] Silver canonical product/set dimensions and validated price observations.
- [ ] Gold card-day analytical panel and reproducible transforms.
- [ ] Test uniqueness, referential integrity, types, freshness, and reconciliation counts.
**Done when:** validated SQL scripts and data dictionary match loaded tables.

## 04 — Exploratory analysis
- [ ] Profile missingness and time coverage by product, condition, rarity and price type.
- [ ] Analyze price distributions, volatility, release age, outliers and stale observations.
- [ ] Document whether observed volume is actually available.
**Done when:** notebook has reproducible figures, conclusions and limitations.

## 05 — Point-in-time features
- [ ] Create price lags, returns, rolling means, volatility, release-age and metadata features.
- [ ] Construct 7/30-day labels without leaking future observations into features.
- [ ] Test chronology and reproducibility.
**Done when:** training panel and leakage tests are documented.

## 06 — Forecast models
- [ ] Last-observed-price and trailing-median baselines.
- [ ] Global XGBoost regression trained across historical cards/sets.
- [ ] SARIMAX only where regularly sampled history justifies it.
- [ ] Track experiment configuration and artifacts.
**Done when:** reproducible out-of-time comparisons exist.

## 07 — Backtesting and uncertainty
- [ ] Rolling-origin evaluation for both horizons.
- [ ] Report MAE, RMSE, WAPE where defined, and errors by rarity/price tier/set.
- [ ] Evaluate prediction interval coverage and identify failure cases.
**Done when:** evaluation report and model card include leakage audit and limitations.

## 08 — Power BI and portfolio
- [ ] Market overview, card explorer, actual vs forecast, model performance, methodology.
- [ ] Publish dashboard screenshots/demo and reproducible setup.
- [ ] Explain retail relevance without claiming access to inventory, margins or actual demand.
**Done when:** final case study includes measured results and source limitations.

## Suggested roles
**Engineering owner:** ingestion, warehouse, orchestration, data tests. **Science owner:** EDA, features, modeling, evaluation. **Shared:** design, code review, dashboard, documentation. Assign actual GitHub usernames only after agreement.
