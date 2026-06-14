# Non-CSO Weekly 30k Top 25 - 2026-05-29 After BRK.B Backfill

Generated from 200 non-CSO strategy/ticker candidates and ranked by actual TraderCore BackTester net PnL over the latest complete local trading week available in PostgreSQL after filling the missing BRK.B bars.

- Source data: PostgreSQL `historical_bars`, `10 secs` `TRADES` RTH bars.
- Scoring window: `2026-05-26T13:30:00+00:00` through `2026-05-29T19:59:50+00:00`.
- Candidate grid: `10 strategies * 20 tickers = 200` configs.
- Strategy budget and BackTester starting cash: `30000` USD per candidate. Single-symbol optimized order sizes are capped at `30000` USD and may use less when the selected share quantity is below the cap.
- Deployment exchange: `IBKR`.
- Deployment note: basket configs with optimized `maxGrossExposure` above `1.0` are clamped to `1.0` for the paper runtime so each strategy's target gross exposure stays within `30000` USD. BackTester metadata below reflects the original optimizer ranking.
- BackTester validation used temporary configs with exchange rewritten to `BACKTESTER`; exported configs remain deployment configs.
- Batch result: `5` benchmark-passing, `156` benchmark-failed with BackTester metrics, `39` skipped.
- Selected set: `5/25` passed positive/same-stock/SPX gates; `25/25` selected configs had positive BackTester PnL.
- Known skips: `19` MATREND-002 BackTester exit -6 failures and `20` PostgreSQL deadlocks during concurrent runs. BRK.B missing-bar skips after backfill: `0`.

| Rank | Config | Variant | Symbols | BackTester Return % | BackTester PnL | Status | Same-stock Excess % | SPX Excess % |
| --- | --- | --- | --- | ---: | ---: | --- | ---: | ---: |
| 1 | `01_ts004_mu_weekly_30k_ibkr.json` | `TS-004` | MU | 6.0256 | 1807.67 | `benchmark_failed` | -11.4983 | 5.1952 |
| 2 | `02_ts004_amd_weekly_30k_ibkr.json` | `TS-004` | AMD | 5.1925 | 1557.74 | `benchmark_failed` | -0.9353 | 4.3621 |
| 3 | `03_mw001_avgo_weekly_30k_ibkr.json` | `MW-001` | AVGO | 2.6757 | 802.70 | `benchmark_failed` | -4.2323 | 1.8453 |
| 4 | `04_qs002_meta_basket_weekly_30k_ibkr.json` | `QS-002` | META, TSLA, BRK.B, JPM, LLY, MU | 2.5555 | 766.64 | `benchmark_failed` | -0.6125 | 1.7251 |
| 5 | `05_ts004_avgo_weekly_30k_ibkr.json` | `TS-004` | AVGO | 2.5033 | 751.00 | `benchmark_failed` | -4.4046 | 1.6730 |
| 6 | `06_ts003_meta_weekly_30k_ibkr.json` | `TS-003` | META | 2.0049 | 601.48 | `benchmark_failed` | -1.5308 | 1.1746 |
| 7 | `07_qs002_nvda_basket_weekly_30k_ibkr.json` | `QS-002` | NVDA, AAPL, MSFT, AMZN, GOOGL, AVGO | 1.7547 | 526.41 | `benchmark_failed` | -0.4371 | 0.9244 |
| 8 | `08_qs002_amzn_basket_weekly_30k_ibkr.json` | `QS-002` | AMZN, GOOGL, AVGO, GOOG, META, TSLA | 1.5460 | 463.80 | `ok` | 0.0056 | 0.7157 |
| 9 | `09_qs002_lly_basket_weekly_30k_ibkr.json` | `QS-002` | LLY, MU, AMD, XOM, WMT, V | 1.5247 | 457.40 | `benchmark_failed` | -1.2582 | 0.6943 |
| 10 | `10_ts003_avgo_weekly_30k_ibkr.json` | `TS-003` | AVGO | 1.5091 | 452.74 | `benchmark_failed` | -5.3988 | 0.6788 |
| 11 | `11_pairs001_meta_basket_weekly_30k_ibkr.json` | `PAIRS-001` | META, TSLA, BRK.B, JPM, LLY, MU | 1.4818 | 444.53 | `benchmark_failed` | -1.6862 | 0.6514 |
| 12 | `12_mw001_lly_weekly_30k_ibkr.json` | `MW-001` | LLY | 1.3439 | 403.17 | `benchmark_failed` | -0.9422 | 0.5136 |
| 13 | `13_matrend001_tsla_weekly_30k_ibkr.json` | `MATREND-001` | TSLA | 1.3153 | 394.60 | `ok` | 0.4945 | 0.4850 |
| 14 | `14_mw001_tsla_weekly_30k_ibkr.json` | `MW-001` | TSLA | 1.2673 | 380.20 | `ok` | 0.4465 | 0.4370 |
| 15 | `15_ts003_intc_weekly_30k_ibkr.json` | `TS-003` | INTC | 1.2557 | 376.70 | `ok` | 7.2925 | 0.4253 |
| 16 | `16_ts003_msft_weekly_30k_ibkr.json` | `TS-003` | MSFT | 1.1097 | 332.92 | `benchmark_failed` | -7.0843 | 0.2794 |
| 17 | `17_pairs001_lly_basket_weekly_30k_ibkr.json` | `PAIRS-001` | LLY, MU, AMD, XOM, WMT, V | 1.0411 | 312.33 | `benchmark_failed` | -1.7418 | 0.2108 |
| 18 | `18_pairs001_tsla_basket_weekly_30k_ibkr.json` | `PAIRS-001` | TSLA, BRK.B, JPM, LLY, MU, AMD | 0.9550 | 286.49 | `benchmark_failed` | -2.6450 | 0.1246 |
| 19 | `19_pairs001_mu_basket_weekly_30k_ibkr.json` | `PAIRS-001` | MU, AMD, XOM, WMT, V, JNJ | 0.9545 | 286.34 | `benchmark_failed` | -0.8994 | 0.1241 |
| 20 | `20_ts002_meta_weekly_30k_ibkr.json` | `TS-002` | META | 0.8958 | 268.73 | `benchmark_failed` | -2.6400 | 0.0654 |
| 21 | `21_matrend001_amd_weekly_30k_ibkr.json` | `MATREND-001` | AMD | 0.8886 | 266.59 | `benchmark_failed` | -5.2391 | 0.0583 |
| 22 | `22_qs001_tsla_basket_weekly_30k_ibkr.json` | `QS-001` | TSLA, BRK.B, JPM, LLY, MU, AMD | 0.8348 | 250.45 | `benchmark_failed` | -2.7651 | 0.0045 |
| 23 | `23_pairs001_aapl_basket_weekly_30k_ibkr.json` | `PAIRS-001` | AAPL, MSFT, AMZN, GOOGL, AVGO, GOOG | 0.8329 | 249.88 | `benchmark_failed` | -1.4464 | 0.0026 |
| 24 | `24_ts003_nvda_weekly_30k_ibkr.json` | `TS-003` | NVDA | 0.8317 | 249.52 | `ok` | 2.8673 | 0.0014 |
| 25 | `25_mw001_mu_weekly_30k_ibkr.json` | `MW-001` | MU | 0.8175 | 245.26 | `benchmark_failed` | -16.7063 | -0.0128 |

Full optimizer metadata, source config paths, BackTester summaries, and benchmark details are in `index.json`.
