# Non-CSO Weekly Top 25

Generated from 200 execution-biased non-CSO strategy/ticker candidates and ranked by actual TraderCore BackTester return over the two-week local data window.

- Source data: PostgreSQL `historical_bars`, `1 min` `TRADES` RTH bars.
- Scoring window: `2026-05-11T10:30:00+00:00` through `2026-05-22T19:59:00+00:00`.
- Candidate grid: `10 strategies * 20 tickers = 200` configs.
- Single-strategy target order notional: `50000` USD; portfolio notional: `100000` USD.
- Deployment exchange: `IBKR`.
- Validation note: BackTester runs used generated temporary configs with exchange rewritten to `BACKTESTER` because the BackTester aborts on `IBKR` exchange instruments.
- Validation result: `177/200` candidates ran successfully in BackTester; all `25/25` selected configs passed a post-build BackTester rerun. `12/25` selected configs beat both same-stock hold and the available SPX overlap benchmark.

| Rank | Config | Variant | Anchor | Symbols | BackTester Return % | BackTester PnL | Sim Fills | Same-stock Excess % | SPX Excess %* |
| --- | --- | --- | --- | --- | ---: | ---: | ---: | ---: | ---: |
| 1 | `01_ts004_xom_weekly_ibkr.json` | `TS-004` | XOM | XOM | 3.1274 | 3127.45 | 18 | -2.4747 | 2.9198 |
| 2 | `02_qs001_brk_b_basket_weekly_ibkr.json` | `QS-001` | BRK.B | BRK.B, JPM, LLY, MU, AMD, XOM | 2.4384 | 2438.37 | 7794 | -0.4671 | 2.2307 |
| 3 | `03_ts004_jnj_weekly_ibkr.json` | `TS-004` | JNJ | JNJ | 2.4378 | 2437.78 | 15 | -3.4992 | 2.2301 |
| 4 | `04_mw001_amd_weekly_ibkr.json` | `MW-001` | AMD | AMD | 2.2108 | 2210.80 | 765 | 0.6477 | 2.0031 |
| 5 | `05_pairs001_intc_basket_weekly_ibkr.json` | `PAIRS-001` | INTC | INTC, COST, NVDA, AAPL, MSFT, AMZN | 2.0874 | 2087.42 | 11529 | 1.7767 | 1.8798 |
| 6 | `06_qs001_jnj_basket_weekly_ibkr.json` | `QS-001` | JNJ | JNJ, INTC, COST, NVDA, AAPL, MSFT | 1.8879 | 1887.89 | 9427 | 0.3534 | 1.6802 |
| 7 | `07_matrend001_amd_weekly_ibkr.json` | `MATREND-001` | AMD | AMD | 1.8517 | 1851.71 | 795 | 0.2886 | 1.6441 |
| 8 | `08_qs001_tsla_basket_weekly_ibkr.json` | `QS-001` | TSLA | TSLA, BRK.B, JPM, LLY, MU, AMD | 1.6962 | 1696.25 | 7161 | -0.3809 | 1.4886 |
| 9 | `09_ts004_wmt_weekly_ibkr.json` | `TS-004` | WMT | WMT | 1.5714 | 1571.44 | 10 | 8.9893 | 1.3638 |
| 10 | `10_ts004_aapl_weekly_ibkr.json` | `TS-004` | AAPL | AAPL | 1.5681 | 1568.14 | 15 | -4.0988 | 1.3605 |
| 11 | `11_qs001_goog_basket_weekly_ibkr.json` | `QS-001` | GOOG | GOOG, META, TSLA, BRK.B, JPM, LLY | 1.5548 | 1554.81 | 5036 | -0.8724 | 1.3472 |
| 12 | `12_ts005_avgo_weekly_ibkr.json` | `TS-005` | AVGO | AVGO | 1.5256 | 1525.61 | 252 | 4.9524 | 1.3180 |
| 13 | `13_ts004_cost_weekly_ibkr.json` | `TS-004` | COST | COST | 1.4514 | 1451.43 | 12 | -1.0959 | 1.2438 |
| 14 | `14_qs001_cost_basket_weekly_ibkr.json` | `QS-001` | COST | COST, NVDA, AAPL, MSFT, AMZN, GOOGL | 1.4207 | 1420.73 | 7151 | 0.2316 | 1.2131 |
| 15 | `15_ts003_mu_weekly_ibkr.json` | `TS-003` | MU | MU | 1.4070 | 1407.01 | 254 | 6.5634 | 1.1994 |
| 16 | `16_qs001_meta_basket_weekly_ibkr.json` | `QS-001` | META | META, TSLA, BRK.B, JPM, LLY, MU | 1.3820 | 1382.02 | 5730 | -0.6323 | 1.1744 |
| 17 | `17_ts002_cost_weekly_ibkr.json` | `TS-002` | COST | COST | 1.3282 | 1328.17 | 468 | -1.2191 | 1.1205 |
| 18 | `18_qs001_v_basket_weekly_ibkr.json` | `QS-001` | V | V, JNJ, INTC, COST, NVDA, AAPL | 1.3235 | 1323.55 | 9412 | -0.3024 | 1.1159 |
| 19 | `19_ts003_amd_weekly_ibkr.json` | `TS-003` | AMD | AMD | 1.3147 | 1314.74 | 318 | -0.2483 | 1.1071 |
| 20 | `20_matrend001_xom_weekly_ibkr.json` | `MATREND-001` | XOM | XOM | 1.2153 | 1215.29 | 843 | -4.3869 | 1.0076 |
| 21 | `21_ts004_tsla_weekly_ibkr.json` | `TS-004` | TSLA | TSLA | 1.2088 | 1208.77 | 15 | 0.5744 | 1.0011 |
| 22 | `22_ts003_tsla_weekly_ibkr.json` | `TS-003` | TSLA | TSLA | 1.1816 | 1181.58 | 288 | 0.5472 | 0.9739 |
| 23 | `23_ts002_tsla_weekly_ibkr.json` | `TS-002` | TSLA | TSLA | 1.1027 | 1102.73 | 447 | 0.4684 | 0.8951 |
| 24 | `24_pairs001_nvda_basket_weekly_ibkr.json` | `PAIRS-001` | NVDA | NVDA, AAPL, MSFT, AMZN, GOOGL, AVGO | 0.9907 | 990.72 | 10505 | 0.7973 | 0.7831 |
| 25 | `25_ts005_amd_weekly_ibkr.json` | `TS-005` | AMD | AMD | 0.8859 | 885.87 | 257 | -0.6772 | 0.6782 |

*SPX is available locally only from `2026-05-14T13:30:00+00:00` through `2026-05-22T19:59:00+00:00`; the selected configs were scored over the full two-week stock window.

All 200 candidates, simulator metrics, and BackTester validation details are in `../../candidate_configs/non_cso_weekly_20260522/index.json`.
