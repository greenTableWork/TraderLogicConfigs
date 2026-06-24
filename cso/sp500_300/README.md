# S&P 500 CSO $300 Config Set

Generated at `2026-06-21T16:31:34Z` from `https://en.wikipedia.org/wiki/List_of_S%26P_500_companies`.

This directory contains `394` eligible `ConstantStepOffset` configs, one per S&P 500 listed stock whose minimum whole-share CSO order can satisfy the `300.0` USD budget. The original constituent pull contained `503` symbols; `109` were removed because their baseline price was above the budget.

Each config sets `orderQuantityInUSD` to `300.0`, uses whole-share `orderQuantity`, and keeps ledger state isolated under `CSO_SP500_300_*`.

See `index.json` for the full eligible symbol-to-config mapping and the removed-symbol metadata.
