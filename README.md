# Dynamic Time-Price Fibonacci Corridor (DTPFC)

A Pine Script v6 indicator for TradingView that turns historical price action
into probabilistic Fibonacci targets in **both price and time**.

For every detected price impulse the script draws six forward-looking boxes:

- **Z1–Z4** — retracement zones at `0.382–0.5`, `0.5–0.618`, `0.618–0.786`, `0.786–1.0`
- **B1–B2** — extension (breakout) zones at `1.0–1.272`, `1.272–1.618`

Each box is positioned in time at the **average ± 1σ** delay at which similar
historical impulses first reached that zone, and labelled with the empirical
**hit-rate** for that zone.

## How it works

1. **Impulse detection.** Confirmed pivots (`ta.pivothigh` / `ta.pivotlow`) split
   the chart into directional impulses (low → high = up-impulse, etc.).
2. **Tentative end.** Pivots are confirmed `pivRight` bars late. To reveal the
   prediction earlier, the script declares an impulse end *tentatively* as soon
   as price retraces from the running extremum by `tentativeMult × ATR`. The
   prediction is drawn in **yellow** while tentative and turns **white** once
   the pivot confirms.
3. **Sample selection.** Only **same-direction** historical impulses count.
   Optional filters narrow the sample to those with comparable `|ΔP|` and/or
   duration relative to the current impulse.
4. **Statistics.** For each historical impulse, the script checks within a
   user-defined `lookforwardBars` window whether price entered each zone, and
   how many bars it took. These are aggregated into hit-rates and time windows.

## Settings

| Group | Key inputs |
|---|---|
| **Current impulse** | `Override with manual impulse`, `Manual Start time`, `Manual End time` (timestamps — bars do not drift) |
| **Detection** | `Pivot left/right bars`, `Tentative end — ATR retracement`, `ATR length` |
| **Statistics** | `Lookforward window (bars)`, `Filter history by impulse size`, `Filter history by impulse duration`, `Max historical impulses to keep` |
| **Display** | Panel position, box transparency, historical-impulse lines and zones, per-zone colours |

## Reading the chart

- **White / yellow line** — current impulse (yellow = tentative end).
- **Coloured boxes** — predicted zones; box height = price range, box width =
  historical time window, label = hit-rate.
- **Thin coloured lines** (optional) — historical same-direction impulses used
  in the statistics: green = touched at least one retracement zone, red =
  invalidated past start, gray = neither.
- **Stats table** — per-zone hit-rate, average τ to first touch, sample count,
  plus an `Invalidated` row (share of impulses that broke past their start).

## Manual mode

Toggle `Override with manual impulse` and set the two timestamps to pin the
impulse to specific bars. Direction is inferred from the close-to-close change
between those two bars. Timestamps anchor the impulse to a fixed point in
history — new bars do not shift the selection.

## Requirements

- TradingView Pine Script **v6**.
- `max_bars_back = 5000` (built-in).

## Files

- `dynamic_time_price_fib_corridor.pine` — the indicator source.

## License

MIT.
