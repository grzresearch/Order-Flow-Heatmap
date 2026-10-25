# Order Flow Heatmap

A Pine Script indicator for TradingView that simulates the visualization of
professional order flow tools such as Bookmap directly on the chart. It turns
historical price and volume data into a heatmap that shows liquidity zones,
volume concentrations and buying or selling pressure at a glance.

## Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Settings](#settings)
- [Alerts](#alerts)
- [Method and limitations](#method-and-limitations)
- [Project structure](#project-structure)
- [License](#license)

## Features

- **Volume profile heatmap**: the volume profile is calculated automatically
  and shows at which price levels the most volume has traded. Intensity is
  drawn with a selectable color scheme, from dark tones at low volume to
  bright colors at high liquidity. Five schemes are available: Bookmap Blue,
  Fire, Green Matrix, Purple and Thermal.
- **Point of Control and Value Area**: the indicator marks the Point of
  Control (POC), the price level with the highest traded volume, and the
  Value Area, where typically 70% of the volume is concentrated. These zones
  serve as important support and resistance areas.
- **High and Low Volume Nodes**: High Volume Nodes (HVN) are marked as
  potential reaction zones, Low Volume Nodes (LVN) as areas the price may move
  through quickly.
- **Volume bubbles**: above-average volume is shown in real time. Green
  circles signal buying pressure on bullish candles, red circles selling
  pressure on bearish candles. Bubble size scales with volume intensity
  across three levels.
- **Delta analysis**: approximates the ratio between buying and selling
  volume. The background is tinted green or red depending on the prevailing
  pressure. The Cumulative Volume Delta (CVD) is drawn as an area at the
  bottom of the chart and shows the accumulated difference between buying and
  selling.
- **Imbalances**: bars with an extreme imbalance between buyers and sellers
  are marked, and Stacked Imbalances are highlighted when several consecutive
  candles show the same directional bias.
- **Session VWAP** with optional ±1σ and ±2σ standard deviation bands.
- **Dashboard** with POC, VAH, VAL, VWAP, delta, CVD, volume ratio, imbalance,
  stacked imbalances, distance to the POC and Value Area status.
- **Alerts** for POC touches, imbalances, Value Area breakouts and
  high-volume events.

## Installation

The script requires Pine Script v6 (`//@version=6`).

1. Open a chart on [TradingView](https://www.tradingview.com) and open the
   **Pine Editor**.
2. Replace the editor contents with
   [`order_flow_heatmap.pine`](order_flow_heatmap.pine).
3. Click **Save**, then **Add to chart**.

## Usage

The indicator is an overlay named **Order Flow Heatmap** (short title
`OF-Heatmap`). After adding it to a chart, open its settings to choose the
color scheme, the lookback window and the components to display. Each
component (heatmap, liquidity levels, bubbles, delta background, CVD,
imbalances, POC and Value Area, VWAP, stacked imbalances) can be switched on
and off separately.

## Settings

The settings dialog uses German labels. Main inputs and their defaults:

| Group | Input | Default |
|-------|-------|---------|
| Heatmap-Einstellungen | Lookback Bars | 100 (20 to 500) |
| | Preis-Levels (Rows) | 40 (20 to 50) |
| | Heatmap Transparenz | 80 |
| | Heatmap nach rechts erweitern | 20 bars |
| Farbschema | Farbschema | Bookmap Blue |
| | Intensitäts-Multiplikator | 1.5 |
| | Dynamische Preis-Range | on |
| Liquiditäts-Levels | Liquiditäts-Schwelle (x Avg) | 1.8 |
| | High Volume Nodes (HVN) / Low Volume Nodes (LVN) | on / on |
| | LVN Schwelle (x Avg) | 0.3 |
| Volume Bubbles | Kleine / Mittlere / Große Bubble Schwelle (x Avg) | 1.3 / 1.8 / 2.5 |
| Delta & Imbalance | Imbalance Ratio | 2.5 |
| POC & Value Area | Value Area % | 70 |
| | POC Linien-Stil | Solid |
| VWAP & Anchors | Session VWAP, VWAP Bänder (±1σ, ±2σ) | on, on |
| Stacked Imbalances | Min. aufeinanderfolgende Imbalances | 3 |

## Alerts

Create an alert on the indicator and choose one of these conditions:

| Condition | Trigger |
|-----------|---------|
| POC Touch | price crosses the POC |
| Buy Imbalance / Sell Imbalance | strong buy or sell imbalance |
| Stacked Buy / Stacked Sell | the configured number of consecutive imbalances |
| VAH Breakout | close crosses above the Value Area High |
| VAL Breakdown | close crosses below the Value Area Low |
| High Volume | volume at or above the large bubble threshold |

## Method and limitations

TradingView does not provide access to real Level 2 order book data. This
indicator is therefore an approximation based on historical volume data: it
shows where volume was traded, not where limit orders currently sit.

Buying and selling volume are estimated from each bar's close position within
its range: buy volume = volume × (close − low) / (high − low), sell volume =
the remainder. Delta, CVD and the imbalance markers are built on this
estimate. The VWAP and its bands are computed from `hlc3` and reset at the
start of each day.

## Project structure

```
order-flow-heatmap/
├── order_flow_heatmap.pine   # the indicator (Pine Script v6)
├── README.md
└── LICENSE                   # Mozilla Public License 2.0
```

## License

Released under the Mozilla Public License 2.0, see [LICENSE](LICENSE).
