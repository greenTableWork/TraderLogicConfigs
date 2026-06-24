# Remaining Strategy Config Plan

Generated: 2026-06-23

This plan covers strategy implementations that either have no checked-in
strategy-suite config yet, or only have thin placeholder coverage that can now
be expanded with the IBKR factor-proxy data set.

## Current Inventory

Current `TraderLogicConfigs` strategy JSON coverage:

| Strategy type | Config count | Coverage status |
| --- | ---: | --- |
| ConstantStepOffset | 451 | Covered; not part of this plan. |
| BuyCloseSellOpen | 50 | Covered for stock stress/strategy-suite use. |
| MovingAverageCross | 148 | Covered for `MW-001`, `MATREND-001`, and `MATREND-002`. |
| TechnicalSignal | 209 | Covered for `TS-002`, `TS-003`, `TS-004`, `TS-005`, `DONCHIAN-001`, and `PIVOT-001`; missing `TS-006`, `TS-007`, and `TS-008`. |
| PortfolioAllocation | 175 | All implemented modes have at least one config, but factor-specific coverage is thin for several modes. |
| SingleOrderTest | 2 | Test/runtime utility only; do not add strategy-suite configs. |

Implemented-but-missing config modes:

| Implementation | Alias | Mode | Config status | Priority |
| --- | --- | --- | --- | --- |
| `TechnicalSignalStrategy` | `TS-006` | Time-series momentum | No checked-in config found. | P0 |
| `TechnicalSignalStrategy` | `TS-007` | Donchian breakout | No checked-in config found. | P0 |
| `TechnicalSignalStrategy` | `TS-008` | Statistical mean reversion | No checked-in config found. | P0 |
| `TechnicalSignalStrategy` | `MW-001` | SMA cross | No `TechnicalSignal` config found, but `MovingAverageCross` already covers `MW-001`. | P2 |

Portfolio modes with only thin strategy-suite coverage:

| Implementation | Alias | Existing coverage | Expansion priority |
| --- | --- | --- | --- |
| `PortfolioAllocation` | `QS-002` | Stock momentum examples exist. | Expand to factor ETF momentum baskets. |
| `PortfolioAllocation` | `TSMOM-001` | One top-stock config exists. | Add stock-factor ETF configs first; add FX/crypto only as separate feed groups. |
| `PortfolioAllocation` | `LV-001` | One low-volatility stock config exists. | Add factor ETF/sector low-volatility basket. |
| `PortfolioAllocation` | `PAIRS-001` | Equity pair examples exist. | Add factor proxy pair sets such as market ETF pairs and sector/industry pairs. |
| `PortfolioAllocation` | `RESMOM-001`, `MULTIBAG-001`, `MLRET-001`, `REGIME-001` | Single/static target-weight examples exist. | Generate target-weight configs only after offline factor scoring artifacts exist. |
| `PortfolioAllocation` | `IVRV-001`, `DISP-001` | Proxy/static examples exist. | Use new vol-factor data for calibration first; dynamic multi-feed backtests need runner work. |

## Data Available Now

The IBKR factor-proxy probe reports `112/116` fetchable historical requests.
Remaining unresolved instruments are `ZB`, `ZN`, `ZT`, and `SI`.

Daily PostgreSQL coverage relevant to configs:

| Feed | Instruments | Rows | Window |
| --- | ---: | ---: | --- |
| `historical_bars`: `STK` / `TRADES` / `use_rth=true` | 91 | 46,761 | 2024-05-15 to 2026-06-22 |
| `historical_bars`: `IND` / `TRADES` / `use_rth=true` | 4 | 2,056 | 2024-06-03 to 2026-06-22 |
| `historical_bars`: `STK` / `HISTORICAL_VOLATILITY` / `use_rth=true` | 3 | 1,539 | 2024-06-03 to 2026-06-18 |
| `historical_bars`: `STK` / `OPTION_IMPLIED_VOLATILITY` / `use_rth=true` | 3 | 1,542 | 2024-06-03 to 2026-06-22 |
| `historical_bars`: `CASH` / `MIDPOINT` / `use_rth=false` | 6 | 3,168 | 2024-06-03 to 2026-06-18 |
| `historical_bars`: `CRYPTO` / `AGGTRADES` / `use_rth=false` | 2 | 1,068 | 2024-06-03 to 2026-06-22 |
| `futures_historical_bars`: `FUT` / `TRADES` / `use_rth=true` | 4 | 1,972 | 2024-06-03 to 2026-06-22, except `GC` starts 2024-09-30 |

BackTester currently calls `PostgresInterface::forEachHistoricalBar`, which
queries `historical_bars` only. First-pass configs should therefore avoid
`FUT` instruments until BackTester supports `futures_historical_bars` or a
normalized union view. BackTester also applies one global `barSize`,
`whatToShow`, and `useRth` per run config, so do not mix `TRADES`, `MIDPOINT`,
`AGGTRADES`, volatility feeds, and RTH/all-hours instruments in the same
backtest run.

## Config Batches

### Batch A: Missing TechnicalSignal Configs

Add minimal, executable strategy configs for modes that currently have no
checked-in config:

| Config family | Proposed files | Feed group | Initial symbols | Parameters |
| --- | --- | --- | --- | --- |
| `TS-006` time-series momentum | `ts006_time_series_momentum_{symbol}_postgres.json` | `STK/IND TRADES use_rth=true` | `SPY`, `QQQ`, `IWM`, `GLD`, `TLT`, `UUP`, `XLK`, `SMH` | `momentumLookback` = 63 and 126 variants; `allowShort=false` first pass, then short-enabled run configs. |
| `TS-007` Donchian breakout | `ts007_donchian_breakout_{symbol}_postgres.json` | `STK/IND TRADES use_rth=true` | `SPY`, `QQQ`, `IWM`, `GLD`, `USO`, `TLT`, `XLK`, `SMH`, `VXX` | `channelWindow=55`, `exitWindow=20`; add 20/10 fast variant only after baseline runs. |
| `TS-008` statistical mean reversion | `ts008_stat_mean_reversion_{symbol}_postgres.json` | `STK TRADES use_rth=true` | `UUP`, `USDU`, `TLT`, `GLD`, `SLV`, `XLF`, `XLE`, `XLU`, `VXX` | `meanReversionWindow=20`, `entryZScore=2.0`, `exitZScore=0.25`; run with shorting enabled because the implementation emits short signals above positive z-score. |
| `TS-006` FX momentum | `ts006_time_series_momentum_{pair}_fx_postgres.json` | `CASH MIDPOINT use_rth=false` | `EURUSD`, `USDJPY`, `GBPUSD`, `AUDUSD`, `USDCAD`, `USDCHF` | Same as stock `TS-006`; keep in separate run configs because `whatToShow=MIDPOINT`. |
| `TS-008` FX mean reversion | `ts008_stat_mean_reversion_{pair}_fx_postgres.json` | `CASH MIDPOINT use_rth=false` | `EURUSD`, `USDJPY`, `GBPUSD`, `AUDUSD`, `USDCAD`, `USDCHF` | Same as stock `TS-008`; separate run configs. |
| `TS-006` crypto momentum | `ts006_time_series_momentum_{symbol}_crypto_postgres.json` | `CRYPTO AGGTRADES use_rth=false` | `BTC`, `ETH` | `momentumLookback=63`; separate run configs because `whatToShow=AGGTRADES`. |
| `TS-007` crypto breakout | `ts007_donchian_breakout_{symbol}_crypto_postgres.json` | `CRYPTO AGGTRADES use_rth=false` | `BTC`, `ETH` | `channelWindow=55`, `exitWindow=20`; separate run configs. |

Optional parity config:

- Add one `TechnicalSignal` `MW-001` SMA-cross config only if the reporting/UI
  needs every `TechnicalSignalMode` represented. It is not a trading-coverage
  gap because `MovingAverageCross` already owns the production `MW-001` path.

### Batch B: Factor Portfolio Configs

Add factor-aware `PortfolioAllocation` configs that only use one compatible
feed group per config:

| Config family | Proposed file | Feed group | Universe | Notes |
| --- | --- | --- | --- | --- |
| Cross-sectional momentum | `qs002_factor_etf_momentum_postgres.json` | `STK TRADES use_rth=true` | Market, size, value/growth, momentum, quality, low-vol, dividend, sector, credit, commodity, crypto-proxy ETFs. | Exclude `IND`, `CASH`, `CRYPTO`, and `FUT` in first pass to keep one feed and avoid duplicate-symbol ambiguity. |
| Low-volatility factor | `lv001_factor_etf_low_volatility_postgres.json` | `STK TRADES use_rth=true` | Same ETF-only factor universe, with sector ETFs included. | Use `lowVolatilityLookback=20`, `lowVolatilityLegSize=5`. |
| Time-series momentum basket | `tsmom001_factor_etf_time_series_momentum_postgres.json` | `STK TRADES use_rth=true` | ETF-only factor universe. | Use `tsmomLookback=126`, `tsmomSkip=21`, `tsmomPositionPolicy=long_flat` first. |
| Pairs trading | `pairs001_factor_proxy_pairs_postgres.json` | `STK TRADES use_rth=true` | `SPY/IVV`, `SPY/VTI`, `QQQ/XLK`, `QQQ/SMH`, `GLD/SLV`, `HYG/JNK`, `IEF/TLT`, `UUP/USDU`. | Only include pairs whose symbols share the same feed. |
| Residual momentum | `resmom001_factor_target_weights_postgres.json` | `STK TRADES use_rth=true` | ETF-only target weights generated offline. | Requires a checked-in target-weight artifact or generator output before config creation. |
| Multibagger screen | `multibag001_factor_target_weights_postgres.json` | `STK TRADES use_rth=true` | ETF-only target weights generated offline. | Same target-weight prerequisite. |
| ML return signal | `mlret001_factor_target_weights_postgres.json` | `STK TRADES use_rth=true` | ETF-only target weights generated offline. | Same target-weight prerequisite. |
| Regime schedule | `regime001_factor_regime_schedule_postgres.json` | `STK TRADES use_rth=true` | ETF-only base weights plus generated regime exposure schedule. | Requires a regime feature/schedule artifact from factor data. |

### Batch C: Volatility/Dispersion Follow-Up

Do not treat `IVRV-001` and `DISP-001` as simple config-only expansions yet.
The new `HISTORICAL_VOLATILITY` and `OPTION_IMPLIED_VOLATILITY` rows are useful
for calibration, but BackTester currently feeds one bar stream into both signal
generation and fill pricing. A direct run over volatility bars would mark fills
at volatility values instead of trade prices.

Follow-up work:

1. Generate calibration artifacts from `SPY`, `QQQ`, and `IWM`
   `HISTORICAL_VOLATILITY` / `OPTION_IMPLIED_VOLATILITY` rows.
2. Add static calibrated configs such as
   `ivrv001_spy_calibrated_vol_postgres.json` only if the fixed
   `impliedVolatility` field is acceptable.
3. For dynamic IV/RV or dispersion signals, extend BackTester to support
   secondary factor feeds while keeping fills on `TRADES` bars.

### Batch D: Futures Follow-Up

The fetchable futures data is useful, but should not be included in first-pass
configs until BackTester reads `futures_historical_bars` or a normalized
historical-bars view:

- `GC`, `CL`, `NG`, `HG` are loaded.
- `ZB`, `ZN`, `ZT`, and `SI` remain unresolved at the IBKR contract level.
- After runner support exists, add commodity trend configs for `TS-006`,
  `TS-007`, and `TSMOM-001`.

## Acceptance Criteria

For each generated config batch:

1. Strategy JSONs live under
   `TraderCore/configs/backtesting/strategy_suite/` in `TraderLogicConfigs`.
2. Matching BackTester run configs live in `TraderCore` because
   `configs/backtesting/runs/strategy_suite/` is not part of this submodule.
3. Run configs keep feed-compatible groups separate:
   `TRADES/RTH`, `MIDPOINT/all-hours`, and `AGGTRADES/all-hours`.
4. Config validation passes through `StrategyConfigChecker`.
5. At least one smoke BackTester run per new mode completes against PostgreSQL.
6. Results are benchmarked against same-symbol buy-and-hold or a matching
   factor benchmark before publishing to UI-facing collections.

## Recommended Order

1. Add and validate Batch A `TS-006`, `TS-007`, and `TS-008` configs for
   `STK/IND TRADES use_rth=true`.
2. Add matching TraderCore run configs for those technical-signal modes.
3. Add Batch B ETF-only portfolio configs.
4. Add FX and crypto technical-signal configs in separate feed-specific run
   groups.
5. Generate target-weight and regime-schedule artifacts for `RESMOM-001`,
   `MULTIBAG-001`, `MLRET-001`, and `REGIME-001`.
6. Decide whether to implement BackTester secondary factor feeds and
   `futures_historical_bars` support before expanding `IVRV-001`, `DISP-001`,
   and futures trend configs.
