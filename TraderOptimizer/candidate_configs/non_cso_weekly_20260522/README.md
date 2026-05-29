# Non-CSO Weekly Candidates

This directory contains the full generated deployment grid for the non-CSO
strategy-suite variants.

- Candidate grid: `10 strategies * 20 tickers = 200` configs.
- Source data: PostgreSQL `historical_bars`, `1 min` `TRADES` RTH bars.
- Scoring window: `2026-05-11T10:30:00+00:00` through
  `2026-05-22T19:59:00+00:00`.
- Single-strategy target order notional: `50000` USD.
- Portfolio target notional: `100000` USD.
- Deployment exchange: `IBKR`.
- Selection artifact:
  `../../optimized_configs/non_cso_weekly_top25_20260522/`.

`index.json` contains all candidate metrics, BackTester validation summaries,
and selected flags. BackTester validation used temporary configs with exchange
rewritten to `BACKTESTER`; the checked-in deployment configs remain `IBKR`.
