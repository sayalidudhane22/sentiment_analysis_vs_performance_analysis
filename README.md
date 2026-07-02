Bitcoin Market Sentiment vs Hyperliquid Trader Performance

Data science assignment exploring the relationship between Bitcoin Fear/Greed sentiment and trader performance on Hyperliquid, with the goal of surfacing patterns useful for a sentiment-aware trading strategy.

Repo Structure

.
├── data/
│   ├── historical_data.csv        # Hyperliquid trade executions (May 2023 – May 2025)
│   └── fear_greed_index.csv       # Daily Bitcoin Fear/Greed Index
├── notebooks/
│   └── sentiment_vs_performance_analysis.ipynb   # Full EDA, stats test, charts (main deliverable)
├── src/
│   └── analysis.py                # Same analysis as a standalone script (regenerates outputs/)
├── outputs/
│   ├── figures/                   # PNG charts
│   ├── sentiment_summary_table.csv
│   └── account_pnl_by_sentiment.csv
├── INSIGHTS.md                    # Written findings and takeaways
├── requirements.txt
└── README.md

How to Run

bashpip install -r requirements.txt
python src/analysis.py            # regenerates outputs/figures + summary CSVs
# or open notebooks/sentiment_vs_performance_analysis.ipynb for the full walkthrough

Approach


Clean & merge: Trade timestamps and the daily Fear/Greed Index are matched on calendar date. Closed PnL == 0 rows (position-building executions, not closes) are excluded from PnL/win-rate stats but kept for volume figures.
Segment: Aggregate PnL, win rate, average trade size, and volume across the five sentiment buckets (Extreme Fear → Extreme Greed).
Test: Welch's t-test on mean daily total PnL, Fear days vs Greed days, to check if the difference is statistically meaningful.
Behavioral view: Account-level PnL by sentiment regime, to see whether performance during Fear is broad-based or concentrated in a few "contrarian specialist" accounts.
Write-up: Findings and caveats in INSIGHTS.md.


Headline Result

Fear days were statistically significantly more profitable than Greed days for this trader population (p = 0.018) — the opposite of the naive assumption that panic causes losses. Full breakdown, caveats, and strategy implications are in INSIGHTS.md.

Data Sources


Historical trader data: Hyperliquid (provided for this assignment)
Market sentiment: Bitcoin Fear & Greed Index
