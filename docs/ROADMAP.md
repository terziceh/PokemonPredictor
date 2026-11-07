# PokemonPredictor — GitHub Project Plan (v2)

**Status:** Planning; implementation not yet verified.  
**Goal:** Deliver an end-to-end Pokémon TCG market-price forecasting portfolio project that demonstrates data science, data engineering, and retail-oriented business communication.

## 1. Project definition

**Question:** Can we predict the observed market price of a Pokémon TCG product 7 and 30 days ahead better than a no-change baseline?

**Initial scope:** A carefully selected cohort of products (for example 20–50, subject to data availability), plus historical sets to support model training. The 30th-anniversary market is the intended showcase, but its history may be insufficient for a stand-alone forecasting model.

**Primary stack:** Python, SQL Server, pandas, scikit-learn, XGBoost, Power BI, GitHub.  
**Optional extension:** Databricks, Delta Lake, Jobs, MLflow.

**Non-goals for MVP:** Live trading recommendations, speculative guaranteed returns, real retailer inventory optimization, two parallel warehouses, or unrestricted web scraping.

## 2. Milestone strategy

| Sprint | GitHub issue | Outcome | Exit gate |
|---|---|---|---|
| 1 — Feasibility | [#1](../issues/1) | Approved source, stable product IDs, sample historical data | Documented coverage and forecast target |
| 2 — Ingestion & SQL | [#2](../issues/2), [#3](../issues/3) | Python ingestion + SQL Server Bronze/Silver/Gold MVP | Repeatable, validated incremental load |
| 3 — EDA & baseline | [#4](../issues/4), [#6](../issues/6) | Statistical findings and no-change forecast | Out-of-time baseline MAE/RMSE |
| 4 — ML features & XGBoost | [#5](../issues/5), [#6](../issues/6) | Leakage-safe feature table and pooled ML model | Model runs on unseen dates |
| 5 — Validation | [#7](../issues/7) | Walk-forward backtests and interval assessment | Model card and baseline comparison |
| 6 — Dashboard & case study | [#8](../issues/8) | Power BI, README, screenshots and technical story | Reproducible portfolio demonstration |
| 7 — Optional platform extension | New issues after MVP | Databricks Jobs/Delta, MLflow, automated monitoring | Same validated results on managed pipeline |

Sprints are **sequenced work packages**, not promises of one-week duration. Do not begin advanced modeling until data feasibility is established.

## 3. Board configuration

Create a GitHub Projects board named **Pokémon TCG Market Intelligence — Delivery Board** and add issues #1–#8.

**Status columns:** Backlog → Ready → In Progress → Review → Done.  
**Suggested custom fields:** Phase (01–08), Priority (P0/P1/P2), Workstream (Engineering/Science/BI/Documentation), Owner, Target sprint, Blocked (Yes/No).

**Starting priorities:**
- P0: #1 data access and target definition; #2 ingestion; #3 SQL warehouse.
- P1: #4 EDA; #5 features; #6 modeling; #7 evaluation.
- P2: #8 dashboard polish (dashboard skeleton can begin earlier).

**Dependency chain:** #1 → #2 → #3 → #4 → #5 → #6 → #7 → #8. Baseline work in #6 can start immediately after #3/#4, before XGBoost.

## 4. Sprint-level implementation checklist

### Sprint 1 — Feasibility and scope
- [ ] List target products, source IDs, sets, rarity, condition and printing.
- [ ] Identify authorized historical pricing API/export and provider terms.
- [ ] Obtain sample rows across multiple dates and products.
- [ ] Decide exactly what a price observation means: market, listing or executed sale.
- [ ] Check whether 7- and 30-day future labels can be constructed with acceptable gaps.
- [ ] Write a short feasibility decision: **Go**, **Narrow scope**, or **Change data source**.

**Deliverable:** `docs/DATA_SOURCES.md` and small schema-only example; no unlicensed raw dataset committed.

### Sprint 2 — Data pipeline and warehouse
- [ ] Python source adapter, timestamp handling, provenance and checkpoint.
- [ ] Bronze raw snapshots; Silver standardized product and price tables.
- [ ] Gold card-day prices and coverage view.
- [ ] Uniqueness, type, referential integrity and freshness tests.
- [ ] Two consecutive runs without duplicate records.

**Deliverables:** `ingestion/`, `sql/`, `tests/` and updated data dictionary.

### Sprint 3 — EDA and baseline
- [ ] Plot product coverage, missingness, price distributions and volatility.
- [ ] Analyze trends by set, rarity and time since release where verified.
- [ ] Establish naive last-observed-price and rolling-median baselines.
- [ ] Report MAE/RMSE separately for 7- and 30-day horizons.

**Deliverables:** `notebooks/01_data_profiling.ipynb`, `02_price_eda.ipynb`, `03_baselines.ipynb`.

### Sprint 4 — Machine learning
- [ ] Construct as-of-date price lags, returns, rolling averages and volatility.
- [ ] Add verified rarity, release age and other point-in-time metadata.
- [ ] Build forecast labels separately and test for leakage.
- [ ] Train a global XGBoost model with chronological validation.
- [ ] Compare against the naive baseline; preserve test holdout.

**Deliverables:** `notebooks/04_feature_engineering.ipynb`, `05_xgboost.ipynb`, reusable `src/` code.

### Sprint 5 — Evaluation and uncertainty
- [ ] Walk-forward backtesting over multiple forecast origins.
- [ ] Compare MAE, RMSE and WAPE where meaningful.
- [ ] Break down errors by price tier, rarity, set and data coverage.
- [ ] Add prediction intervals only with empirical coverage checks.
- [ ] Document weak cases, data constraints and model selection.

**Deliverables:** `notebooks/06_backtesting.ipynb`, `reports/model_card.md`, `reports/evaluation.md`.

### Sprint 6 — Power BI and portfolio
- [ ] Market overview and card explorer.
- [ ] Forecast versus actual with uncertainty visualization.
- [ ] Baseline-versus-XGBoost evaluation page.
- [ ] Publish screenshots, demo instructions and business-facing takeaways.
- [ ] Verify README setup instructions from a clean environment.

**Deliverables:** `dashboards/`, `reports/case_study.md`, completed README.

### Sprint 7 — Stretch goals
- [ ] Reimplement Bronze/Silver/Gold with Delta on Databricks.
- [ ] Schedule permitted ingestion and transformation jobs.
- [ ] Track model runs with MLflow.
- [ ] Add automated data quality and drift reporting.
- [ ] Optionally evaluate SARIMAX for sufficiently long regular histories.

**Gate:** Only after the SQL Server + Python + Power BI MVP works.

## 5. Collaboration

**Engineering lead (suggested):** source adapter, ingestion, SQL Server, data quality, optional Databricks.  
**Data science lead (suggested):** EDA, feature engineering, baselines, XGBoost, evaluation.  
**Both:** data contracts, code review, Power BI, storytelling, documentation.

Each issue should have a single accountable owner and acceptance criteria. Use small feature branches and pull requests. Do not assign usernames without agreement.

## 6. Definition of done

An issue is **Done** only when its artifact exists, can be reproduced, has appropriate tests/checks, and its assumptions and limitations are documented. An entire sprint is done only when its exit gate is met.

## 7. Meijer-oriented portfolio narrative

Present the project as a retail-analytics case study: define a pricing-intelligence question, build a reliable historical dataset, evaluate predictive methods against baselines, and communicate uncertainty to a nontechnical stakeholder. Do not claim retail demand, inventory optimization or measurable business lift without real sell-through and cost data.

## 8. Risks and decision points

| Risk | Mitigation |
|---|---|
| Source does not permit automated collection | Use an authorized API/export or licensed historical dataset |
| Anniversary set has limited history | Train on historical sets; label anniversary forecasts experimental |
| Sparse/stale price observations | Report coverage; avoid fabricated daily prices |
| Price definition differs across providers | Separate market/listing/sold and product condition |
| Forecast leakage | Point-in-time features, chronological splits and label tests |
| Model fails to beat no-change baseline | Report that result; emphasize analysis and limitations |
| Scope becomes too large | Finish SQL Server MVP before Databricks extension |

**Immediate next action:** Complete [Issue #1](../issues/1), then approve the exact data contract before implementing more of the pipeline.
