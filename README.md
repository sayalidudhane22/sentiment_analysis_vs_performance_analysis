# Bitcoin Market Sentiment vs Hyperliquid Trader Performance

Data science assignment exploring the relationship between Bitcoin Fear/Greed sentiment and trader performance on Hyperliquid, with the goal of surfacing patterns useful for a sentiment-aware trading strategy.


## Approach

1. **Clean & merge**: Trade timestamps and the daily Fear/Greed Index are matched on calendar date. `Closed PnL == 0` rows (position-building executions, not closes) are excluded from PnL/win-rate stats but kept for volume figures.
2. **Segment**: Aggregate PnL, win rate, average trade size, and volume across the five sentiment buckets (Extreme Fear → Extreme Greed).
3. **Test**: Welch's t-test on mean daily total PnL, Fear days vs Greed days, to check if the difference is statistically meaningful.
4. **Behavioral view**: Account-level PnL by sentiment regime, to see whether performance during Fear is broad-based or concentrated in a few "contrarian specialist" accounts.
5. **Write-up**: Findings and caveats in `INSIGHTS.md`.

## Headline Result

Fear days were **statistically significantly more profitable** than Greed days for this trader population (p = 0.018) — the opposite of the naive assumption that panic causes losses. Full breakdown, caveats, and strategy implications are in [`INSIGHTS.md`](./INSIGHTS.md).

