# Pokémon TCG Market Intelligence & Price Forecasting

An end-to-end Python, SQL Server, machine learning, and Power BI project exploring Pokémon TCG historical prices and forecasting 7- and 30-day future market prices, with an initial focus on the 30th-anniversary market.

**Status:** Planning / data feasibility. **No model accuracy or business impact is claimed yet.**

## Research questions
- Can price history outperform a last-observed-price baseline for 7- and 30-day forecasts?
- Which observable market features explain price changes and volatility?
- How well do models generalize to new cards and sets?
- How can reliable forecasts and uncertainty support retail pricing intelligence?

## Planned architecture
```text
Authorized source/API/export
  → Python ingestion & source snapshots
  → SQL Server (Bronze raw → Silver validated → Gold analytical)
  → Python EDA + leakage-safe feature engineering
  → Last-price baseline / XGBoost / optional SARIMAX
  → Walk-forward backtesting & prediction intervals
  → Power BI dashboard + portfolio case study
```
Databricks/Delta is an optional lakehouse extension once the SQL Server MVP is validated.

## Roadmap
| Phase | Deliverable |
|---|---|
| 01 — Scope & feasibility | Data source inventory, target definition, success criteria |
| 02 — Ingestion | Repeatable compliant Python collection, logs, raw snapshots |
| 03 — Warehouse | SQL Server Bronze/Silver/Gold and data quality tests |
| 04 — EDA | Price distributions, trends, missingness, volatility |
| 05 — Features | Point-in-time card-day features and 7/30-day labels |
| 06 — Modeling | Baselines, global XGBoost, optional SARIMAX |
| 07 — Validation | Walk-forward backtests, segment errors, uncertainty |
| 08 — BI & publication | Power BI dashboard, reproducible case study |

See [full roadmap](docs/ROADMAP.md), [architecture](docs/ARCHITECTURE.md), [data dictionary](docs/DATA_DICTIONARY.md), [modeling plan](docs/MODELING_PLAN.md), and [collaboration guide](docs/CONTRIBUTING.md). Track implementation in [GitHub Issues](https://github.com/terziceh/PokemonPredictor/issues).

## Proposed repository layout
```text
docs/       planning, architecture, data definitions, modeling methodology
ingestion/  source adapters and incremental collection
sql/        schemas, transformations and validation
notebooks/  EDA, feature engineering, modeling, evaluation
src/        reusable Python library
tests/      ingestion, SQL and leakage tests
dashboards/ Power BI assets and screenshots
reports/    findings, evaluation and final case study
```
The folders above are a *plan*, not a claim that the implementation exists.

## Responsible data use
Only use data sources and collection methods allowed by provider terms and access controls. Respect rate limits; do not bypass anti-bot restrictions. Do not commit credentials, browser profiles, private exports, or unlicensed datasets. Distinguish listing, market and executed-sale prices and preserve product condition/printing.

## Portfolio goal
Demonstrate data engineering, statistical reasoning, supervised learning, time-series evaluation, and retail-focused communication. Market prices are not the same as retail demand or optimal prices without sell-through, inventory and margin data.

*Independent educational project; not affiliated with The Pokémon Company, TCGplayer, or Meijer. Forecasts are not investment advice.*
