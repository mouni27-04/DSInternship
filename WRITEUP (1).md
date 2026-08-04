# Trader Performance vs Market Sentiment — Write-Up

## Methodology
Merged Hyperliquid trade fills (rolled up to daily PnL, win rate, trade count, avg size, long/short ratio per account) with the daily Fear/Greed sentiment index. Two data gaps were handled explicitly rather than glossed over: no leverage field exists in the raw fills (`Start Position` is token quantity, not margin, so it wasn't a valid proxy — leverage was dropped), and sentiment data ends 2025-05-02 while trades run to 2025-06-15, so 25 trader-days lost their sentiment label and were excluded from sentiment analysis. After cleaning, 77 trader-days remained (Fear: 32, Greed: 37, Neutral: 8), heavily concentrated on just three trading dates — so results here read more as case studies than a robust time series.

## Insights
1. **Fear days show higher PnL than Greed days, but part of that is two volatile market dates, not sentiment itself.** Median PnL: Fear $81K vs Greed $21K. But the five largest PnL days all trace to just two dates (one Fear, one Greed) with 29-32 accounts active each — market-wide volatility, not sentiment causing better outcomes.
2. **Activity roughly triples on Fear days, and long bias intensifies sharply** (long/short ratio 720.6 on Fear vs 153.7 on Greed) — consistent with dip-buying rather than defensive pullback.
3. **Infrequent traders gain proportionally more from Fear than frequent traders do** (6.3x PnL jump vs 2.7x), even though frequent traders still win on absolute dollars.
4. **"Inconsistent" traders have the lowest win rate (23-35%) but the biggest Fear-day payouts** — looks like a few high-variance bets, not a repeatable edge, versus "Consistent Winners" who stay stable across regimes.
5. **Clustering (after removing 2 single-date outlier accounts) found two archetypes**: a low-win-rate/high-conviction group (26% win rate, $8.7K avg size) with the highest total PnL, and a high-win-rate/high-frequency group (47% win rate, smaller trades) with lower total PnL — win rate alone doesn't predict profitability here.
6. **Bonus predictive model (next-day profitability) underperformed the baseline** (43% vs 89% accuracy) on a small, imbalanced sample (45 rows, 5 unprofitable) — an honest negative result suggesting profitability isn't simply regime-persistent day to day at this sample size.

## Strategy Recommendations
1. **Infrequent traders should prioritize selective entries during Fear** rather than trading more often — that's where their relative edge shows up most in this data.
2. **Inconsistent traders should use fixed position-size limits instead of sizing up on conviction**, since their Fear-day gains look driven by a few large bets rather than skill.

*Full methodology detail, limitations, and supporting tables are in the notebook.*
