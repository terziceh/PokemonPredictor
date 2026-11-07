# Proposed data dictionary

This is a **target design**; fields are subject to actual source availability.

## dim_product
| Field | Type | Definition |
|---|---|---|
| product_id | text | Stable internal product key |
| source_product_id | text | Provider-specific product ID |
| set_id | text | Set key |
| product_name | text | Display name |
| product_type | text | Single, sealed or other |
| rarity | text nullable | Verified rarity |
| printing | text nullable | Variant |
| release_date | date nullable | Verified release date |

## fact_price_observation
| Field | Type | Definition |
|---|---|---|
| observation_id | text | Deterministic observation key |
| product_id | text | Product foreign key |
| source_name | text | Provider |
| observed_at_utc | timestamp | Price observation/event timestamp |
| ingested_at_utc | timestamp | Collection timestamp |
| price_type | text | Market, listing, sold, etc. |
| condition | text nullable | Product condition |
| currency | text | Price currency |
| price | decimal | Observed amount |
| sale_count | integer nullable | Actual observed sales, if available |
| source_record_id | text nullable | External event key |

## gold_card_day
One row per product, date, price type, condition and printing, with observed_price, observation_count, stale_days and days_since_release. Preserve missingness; do not blindly forward-fill.

## gold_model_features
One row per product, forecast origin, horizon, price type, condition and printing. Features must be available at forecast origin. Future labels are constructed separately and include label timestamp and matching tolerance.

## Minimum data tests
- Unique observation keys and valid product references
- Valid currency, prices and timestamps
- Correct price-type and condition separation
- Consistent daily aggregation rules
- Freshness, missingness and coverage reporting
- No unverified demand or sales-volume proxies
