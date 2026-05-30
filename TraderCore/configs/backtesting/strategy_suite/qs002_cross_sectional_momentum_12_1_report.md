# QS-002 Cross-Sectional Momentum 12-1 First Pass

Config:
`TraderLogicConfigs/TraderCore/configs/backtesting/strategy_suite/qs002_cross_sectional_momentum_12_1_top_stocks_postgres.json`

Implementation notes:
- Uses `PortfolioAllocationStrategy` with `allocation_type` `QS-002`.
- The config marks `positioning` as `long_short` and `shortLegPolicy` as
  `short_bottom_ranked_symbols`; those metadata fields document the bottom-leg
  sell-short assumption while the strategy code enforces the actual weights.
- Scores each instrument by trailing return over `momentumLookback` periods,
  ending `momentumSkipPeriods` before the latest close.
- Selects long and short legs from `momentumLegQuantile` when present;
  otherwise it uses `momentumLegSize`.
- Keeps the strategy dollar neutral by allocating 0.50 gross exposure to the
  long leg and 0.50 gross exposure to the short leg before the existing gross
  exposure cap is applied.

Backtest status:
- Not run in this worktree because CMake configure currently fails before test
  target generation: `add_subdirectory` references a missing
  `third_party_libs` directory.
