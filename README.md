Dynamic Time-Price Fibonacci Corridor (DTPFC)

A Pine Script v6 indicator for TradingView that turns historical price action
into probabilistic Fibonacci targets in both price and time.

For every detected price impulse the script draws six forward-looking boxes:
four retracement zones Z1–Z4 covering 0.382–0.5, 0.5–0.618, 0.618–0.786 and
0.786–1.0, and two extension (breakout) zones B1–B2 at 1.0–1.272 and
1.272–1.618.

Each box is positioned in time at the average ± 1σ delay at which similar
historical impulses first reached that zone, and labelled with the empirical
hit-rate for that zone.

How it works

Confirmed pivots from ta.pivothigh and ta.pivotlow split the chart into
directional impulses (low to high is an up-impulse, high to low is a
down-impulse). Pivots are confirmed pivRight bars late, so to reveal the
prediction earlier the script declares an impulse end tentatively as soon as
price retraces from the running extremum by tentativeMult × ATR. The
prediction is drawn in yellow while tentative and turns white once the pivot
confirms.

Only same-direction historical impulses count toward the statistics. Optional
filters narrow the sample to those with comparable absolute price range and
duration relative to the current impulse. For each historical impulse the
script checks within a user-defined lookforward window whether price entered
each zone, and how many bars it took. These observations are aggregated into
hit-rates and time windows.

Settings

Current impulse — override with manual impulse, manual start time, manual end
time. Timestamps anchor the impulse to fixed bars; new bars do not shift the
selection.

Detection — pivot left/right bars, tentative end ATR retracement multiplier,
ATR length.

Statistics — lookforward window in bars, filter history by impulse size,
filter history by impulse duration, max historical impulses to keep.

Display — panel position, box transparency, toggles for historical-impulse
lines and retroactive zone boxes, per-zone colours.

Reading the chart

The current impulse is a thick line: yellow while the end is tentative, white
once the opposite pivot has confirmed it. Coloured boxes are the predicted
zones — box height covers the price range, box width covers the historical
time window, and the label inside shows the hit-rate.

Thin coloured lines (optional) are the historical same-direction impulses used
in the statistics. Green means the impulse touched at least one retracement
zone, red means it was invalidated past its own start, gray means neither.

The stats table lists, for each zone, the hit-rate, the average time to first
touch, and the sample count, plus an Invalidated row showing the share of
impulses that broke past their start.

Manual mode

Toggle override with manual impulse and set the two timestamps to pin the
impulse to specific bars. Direction is inferred from the close-to-close
change between those two bars.

Requirements

TradingView Pine Script v6. The script declares max_bars_back = 5000.

Files

dynamic_time_price_fib_corridor.pine — the indicator source.

License

MIT.
