# Modeling and evaluation plan

## Target
Forecast a consistently defined Pokémon product price at **7 days** and **30 days** after a known forecast origin. Fix source, currency, condition, printing and price definition before training. Define how to handle missing future observations.

## Feasibility
Audit the number of products, historical sets, observations, cadence, stale gaps and source rights. Anniversary-only data may be too short for reliable 30-day evaluation; train on older sets and clearly mark transfer forecasts as experimental.

## Baselines
1. Last observed price (no-change).
2. Trailing median or average.
3. Seasonal naive only if justified by observed history.

## Primary model
A pooled/global XGBoost regressor trained across cards/sets using historical lags, rolling price means, returns, volatility, release age, verified rarity and observed volume if available. Consider log-price or log-return targets; document inverse transformation and bias.

## Statistical comparison
SARIMAX only for sufficiently long, regular time series. Do not assume seasonal structure from a newly released set.

## Validation
- Chronological training, validation and untouched test periods.
- Rolling-origin backtests for each horizon.
- Feature values and joins must respect data *available at forecast origin*, including ingestion delay.
- Tune on training/validation folds only.
- Optionally hold out whole sets to test generalization.
- Test future-label alignment and guard against lookahead leakage.

## Metrics
Report MAE and RMSE in dollars, WAPE where meaningful, error by set/rarity/price tier/coverage, and improvement versus the no-change baseline. Quantile or conformal intervals may be calibrated on validation data; report empirical coverage and interval width on test data.

## Model card
Include target, sources and usage rights, data ranges, counts, feature list, chronological splits, baseline comparisons, uncertainty, failure cases, leakage controls, limitations and intended use. No claimed accuracy before results exist.
