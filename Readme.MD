# Trader Performance vs Market Sentiment

Analysis of how Bitcoin market sentiment (Fear/Greed) relates to trader behavior and
performance on Hyperliquid.

## Contents

- `DS_Internship.ipynb` — main analysis notebook (data cleaning, merging, metrics,
  segment analysis, clustering)
- `WRITEUP.md` — methodology, insights, and strategy recommendations (1-page summary)
- `outputs/` — exported charts and summary tables
  - `sentiment_comparison.png` — PnL / win rate / trade frequency / long-short ratio by sentiment
  - `sentiment_summary.csv` — aggregated metrics by sentiment group
  - `activity_segment_summary.csv` — PnL/win rate by trade-frequency segment × sentiment
  - `performance_segment_summary.csv` — PnL/win rate by consistency segment × sentiment
  - `cluster_features.csv` — per-account features and cluster assignment

## Data sources

1. **Bitcoin Fear/Greed Index** — `fear_greed_index.csv` (Date, Classification)
2. **Historical Trader Data (Hyperliquid)** — `historical_data.csv` (account, symbol,
   execution price, size, side, timestamp, direction, closed PnL, etc.)

Place both CSVs in the project root (same folder as the notebook) before running.

## Setup

Requires Python 3.9+ and the following packages:

```bash
pip install pandas matplotlib scikit-learn
```

## How to run

1. Ensure `fear_greed_index.csv` and `historical_data.csv` are in the project root.
2. Open `DS_Internship.ipynb` and run all cells top to bottom (Restart Session & Run All).
3. Outputs (charts and CSVs) are written to the `outputs/` folder.
4. See `WRITEUP.md` for the interpreted findings and strategy recommendations.

## Known limitations

- No reliable leverage/margin column exists in the trader dataset (`Start Position`
  reflects token quantity, not margin), so leverage-based metrics and the
  "high vs low leverage" segment from the brief could not be built. This is
  documented in the notebook rather than approximated with an invalid proxy.
- One account in the clustering step trades at an extreme frequency relative to the
  rest of the population and forms its own single-member cluster; see the
  Methodology section of `WRITEUP.md` for how this was handled.
