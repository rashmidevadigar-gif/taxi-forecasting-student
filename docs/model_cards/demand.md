# Model Card — taxi-demand-forecaster

_Generated: 2026-10-24 10:47 UTC_

## Model details

- **Problem:** demand
- **Algorithm:** XGBRegressor
- **Target:** `pickup_count`
- **Registry version:** n/a

## Intended use

Operational forecasting of pickup_count to support fleet positioning and rider fare estimates. Not intended for individual pricing decisions or any use with legal/financial consequences for individuals.

## Evaluation — overall (test split)

| Metric | Value |
|--------|-------|
| rmse | 8.8504 |
| mae | 2.5514 |
| mape | 40.1314 |
| r2 | 0.9697 |

## Evaluation — subgroup fairness

### By borough

Disparity ratio (worst/best RMSE): **203.84** (threshold 1.5) — ⚠️ **flagged**. Worst: `Manhattan`, best: `Staten Island`.

| Group | n | RMSE | MAE | MAPE |
|-------|---|------|-----|------|
| Manhattan | 3862 | 16.040 | 7.795 | 29.72 |
| Queens | 3971 | 6.026 | 1.163 | 52.26 |
| Unknown | 116 | 3.277 | 1.986 | 46.96 |
| Brooklyn | 3457 | 0.742 | 0.444 | 53.72 |
| Bronx | 2476 | 0.443 | 0.266 | 65.04 |
| EWR | 58 | 0.272 | 0.102 | 97.94 |
| Staten Island | 633 | 0.079 | 0.048 | 92.73 |

### By time_of_day

Disparity ratio (worst/best RMSE): **2.64** (threshold 1.5) — ⚠️ **flagged**. Worst: `evening`, best: `overnight`.

| Group | n | RMSE | MAE | MAPE |
|-------|---|------|-----|------|
| evening | 4554 | 12.187 | 3.398 | 36.91 |
| afternoon | 3947 | 8.477 | 2.959 | 36.23 |
| morning | 3036 | 6.206 | 2.362 | 39.67 |
| overnight | 3036 | 4.609 | 0.941 | 56.72 |

### By day_type

Disparity ratio (worst/best RMSE): **1.00** (threshold 1.5) — ok. Worst: `weekday`, best: `weekday`.

| Group | n | RMSE | MAE | MAPE |
|-------|---|------|-----|------|
| weekday | 14573 | 8.850 | 2.551 | 40.13 |

### By holiday

Disparity ratio (worst/best RMSE): **1.00** (threshold 1.5) — ok. Worst: `non-holiday`, best: `non-holiday`.

| Group | n | RMSE | MAE | MAPE |
|-------|---|------|-----|------|
| non-holiday | 14573 | 8.850 | 2.551 | 40.13 |

### By airport

Disparity ratio (worst/best RMSE): **4.17** (threshold 1.5) — ⚠️ **flagged**. Worst: `airport`, best: `non-airport`.

| Group | n | RMSE | MAE | MAPE |
|-------|---|------|-----|------|
| airport | 116 | 34.740 | 25.218 | 33.44 |
| non-airport | 14457 | 8.323 | 2.370 | 40.27 |

## Top features (SHAP)

| Feature | Mean |SHAP| |
|---------|-----------|
| lag_1 | 10.9303 |
| lag_168 | 8.0260 |
| lag_24 | 4.6653 |
| rolling_mean_3 | 1.3479 |
| hour_cos | 0.7771 |
| lag_2 | 0.6418 |
| rolling_mean_168 | 0.3754 |
| rolling_std_3 | 0.3452 |
| lag_3 | 0.3336 |
| hour | 0.3118 |

## Limitations

- Trained on a single month of NYC Yellow Taxi data; may not generalise to other periods, boroughs served sparsely, or green/for-hire vehicles.
- Predictions degrade under distribution shift (see drift monitoring).

## Ethical considerations

- No demographic or protected attributes are used or available; fairness is assessed as geographic/temporal service equity, not demographic parity.
- Large borough-level disparities could translate into unequal service quality across neighbourhoods and should be monitored.
