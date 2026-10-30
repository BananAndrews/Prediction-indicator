# Dynamic Time-Price Fibonacci Corridor

When working in D:\Dev, consult ../workspace-context/PROJECTS.md for workspace routing and ../workspace-context/WORKSPACE_CONTEXT.md for shared context if present. These workspace files are local context, not a dependency of the project.

- Read `README.md` and `dynamic_time_price_fib_corridor.pine`. Aliases: Prediction indicator, DTPFC, Fibonacci corridor. This is separate from the RSI and BOS strategy indicators.
- Stack: TradingView Pine Script v6. Historical same-direction impulses produce retracement zones Z1-Z4 and breakout zones B1-B2 with empirical hit rates and time windows.
- Preserve the distinction between tentative ATR-retracement endpoints and confirmed pivots, direction/size/duration filters, and sample counts. Manual start/end timestamps anchor to fixed bars and should not drift with incoming bars.
- Validation is compilation in TradingView Pine Editor plus chart inspection of tentative/confirmed, manual/automatic and up/down cases for actual logic changes. No local automated test suite was found; do not describe historical hit rates as guaranteed forecasts.
- Onboarding baseline, 2026-10-30: working tree was clean; latest local commit `1b9e5ad`. Recheck source and Git state when resuming.
