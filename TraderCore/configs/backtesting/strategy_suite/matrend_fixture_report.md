# Moving Average Trend Fixture Report

This fixture is intentionally small and deterministic. It proves the
new trend modes can emit both an entry and exit before they are run
against PostgreSQL `historical_bars` market data.

| ID | Mode | Windows | Trades |
| --- | --- | --- | --- |
| MATREND-001 | single_ma | trend=5 | BUY@6:99; SELL@11:102; BUY@17:99; SELL@22:104 |
| MATREND-002 | triple_ma | fast=2, middle=3, slow=5 | BUY@7:101; SELL@12:100; BUY@18:102; SELL@23:101 |
