# Non-CSO Weekly 30k Top 25 - 2026-05-29

Generated from 200 non-CSO strategy/ticker candidates and ranked by actual TraderCore BackTester net PnL over the latest complete local trading week available in PostgreSQL.

- Source data: PostgreSQL `historical_bars`, `10 secs` `TRADES` RTH bars.
- Scoring window: `2026-05-26T13:30:00+00:00` through `2026-05-29T19:59:50+00:00`.
- Candidate grid: `10 strategies * 20 tickers = 200` configs.
- Strategy budget and BackTester starting cash: `30000` USD per candidate. Single-symbol optimized order sizes are capped at `30000` USD and may use less when the selected share quantity is below the cap.
- Deployment exchange: `IBKR`.
- BackTester validation used temporary configs with exchange rewritten to `BACKTESTER`; exported configs remain deployment configs.
- Batch result: `4` benchmark-passing, `128` benchmark-failed with BackTester metrics, `68` skipped.
- Selected set: `4/25` passed positive/same-stock/SPX gates; all `25/25` selected configs had positive BackTester PnL.
- Known skips: BRK.B 10-second bars were unavailable for the scoring window; three candidates also hit PostgreSQL deadlocks during concurrent runs.

| Rank | Config | Variant | Symbols | BackTester Return % | BackTester PnL | Status | Same-stock Excess % | SPX Excess % |
| --- | --- | --- | --- | ---: | ---: | --- | ---: | ---: |
| 1 | `01_ts004_amd_weekly_30k_ibkr.json` | `TS-004` | AMD | 5.1070 | 1532.10 | `benchmark_failed` | -1.0207 | 4.2767 |
| 2 | `02_matrend001_mu_weekly_30k_ibkr.json` | `MATREND-001` | MU | 4.0634 | 1219.02 | `benchmark_failed` | -13.4604 | 3.2331 |
| 3 | `03_ts004_avgo_weekly_30k_ibkr.json` | `TS-004` | AVGO | 3.8833 | 1165.00 | `benchmark_failed` | -3.0246 | 3.0530 |
| 4 | `04_ts003_amd_weekly_30k_ibkr.json` | `TS-003` | AMD | 2.1134 | 634.01 | `benchmark_failed` | -4.0143 | 1.2830 |
| 5 | `05_mw001_intc_weekly_30k_ibkr.json` | `MW-001` | INTC | 2.0485 | 614.55 | `ok` | 8.0854 | 1.2182 |
| 6 | `06_qs002_aapl_basket_weekly_30k_ibkr.json` | `QS-002` | AAPL, MSFT, AMZN, GOOGL, AVGO, GOOG | 1.8814 | 564.41 | `benchmark_failed` | -0.3979 | 1.0510 |
| 7 | `07_qs002_nvda_basket_weekly_30k_ibkr.json` | `QS-002` | NVDA, AAPL, MSFT, AMZN, GOOGL, AVGO | 1.8019 | 540.57 | `benchmark_failed` | -0.3899 | 0.9716 |
| 8 | `08_qs002_jnj_basket_weekly_30k_ibkr.json` | `QS-002` | JNJ, INTC, COST, NVDA, AAPL, MSFT | 1.7230 | 516.90 | `ok` | 3.3128 | 0.8927 |
| 9 | `09_qs002_msft_basket_weekly_30k_ibkr.json` | `QS-002` | MSFT, AMZN, GOOGL, AVGO, GOOG, META | 1.4892 | 446.76 | `benchmark_failed` | -1.2800 | 0.6589 |
| 10 | `10_ts003_avgo_weekly_30k_ibkr.json` | `TS-003` | AVGO | 1.2950 | 388.50 | `benchmark_failed` | -5.6130 | 0.4647 |
| 11 | `11_ts004_intc_weekly_30k_ibkr.json` | `TS-004` | INTC | 1.1990 | 359.70 | `ok` | 7.2359 | 0.3687 |
| 12 | `12_pairs001_msft_basket_weekly_30k_ibkr.json` | `PAIRS-001` | MSFT, AMZN, GOOGL, AVGO, GOOG, META | 1.1486 | 344.59 | `benchmark_failed` | -1.6206 | 0.3183 |
| 13 | `13_pairs001_nvda_basket_weekly_30k_ibkr.json` | `PAIRS-001` | NVDA, AAPL, MSFT, AMZN, GOOGL, AVGO | 1.1117 | 333.50 | `benchmark_failed` | -1.0802 | 0.2813 |
| 14 | `14_mw001_avgo_weekly_30k_ibkr.json` | `MW-001` | AVGO | 0.9793 | 293.79 | `benchmark_failed` | -5.9287 | 0.1490 |
| 15 | `15_qs002_jpm_basket_weekly_30k_ibkr.json` | `QS-002` | JPM, LLY, MU, AMD, XOM, WMT | 0.9762 | 292.87 | `benchmark_failed` | -1.3308 | 0.1459 |
| 16 | `16_matrend001_tsla_weekly_30k_ibkr.json` | `MATREND-001` | TSLA | 0.9134 | 274.01 | `ok` | 0.0926 | 0.0830 |
| 17 | `17_matrend001_avgo_weekly_30k_ibkr.json` | `MATREND-001` | AVGO | 0.7832 | 234.95 | `benchmark_failed` | -6.1248 | -0.0472 |
| 18 | `18_mw001_amd_weekly_30k_ibkr.json` | `MW-001` | AMD | 0.7163 | 214.90 | `benchmark_failed` | -5.4114 | -0.1140 |
| 19 | `19_qs001_msft_basket_weekly_30k_ibkr.json` | `QS-001` | MSFT, AMZN, GOOGL, AVGO, GOOG, META | 0.6616 | 198.48 | `benchmark_failed` | -2.1076 | -0.1687 |
| 20 | `20_pairs001_cost_basket_weekly_30k_ibkr.json` | `PAIRS-001` | COST, NVDA, AAPL, MSFT, AMZN, GOOGL | 0.6573 | 197.18 | `benchmark_failed` | 0.7617 | -0.1731 |
| 21 | `21_qs001_lly_basket_weekly_30k_ibkr.json` | `QS-001` | LLY, MU, AMD, XOM, WMT, V | 0.6441 | 193.23 | `benchmark_failed` | -2.1388 | -0.1862 |
| 22 | `22_ts002_tsla_weekly_30k_ibkr.json` | `TS-002` | TSLA | 0.6391 | 191.72 | `benchmark_failed` | -0.1817 | -0.1913 |
| 23 | `23_matrend001_amd_weekly_30k_ibkr.json` | `MATREND-001` | AMD | 0.6266 | 187.99 | `benchmark_failed` | -5.5011 | -0.2037 |
| 24 | `24_qs001_aapl_basket_weekly_30k_ibkr.json` | `QS-001` | AAPL, MSFT, AMZN, GOOGL, AVGO, GOOG | 0.5349 | 160.48 | `benchmark_failed` | -1.7444 | -0.2954 |
| 25 | `25_qs001_jpm_basket_weekly_30k_ibkr.json` | `QS-001` | JPM, LLY, MU, AMD, XOM, WMT | 0.5154 | 154.63 | `benchmark_failed` | -1.7916 | -0.3149 |

Full optimizer metadata, source config paths, BackTester summaries, and benchmark details are in `index.json`.
