# Insights: Trader Performance vs Bitcoin Market Sentiment

**Dataset:** 211,224 Hyperliquid trade executions across 32 accounts and 246 symbols, full year 2024, merged with the daily Bitcoin Fear/Greed Index.

## 1. Headline Finding: Traders perform *better*, not worse, during Fear

| Sentiment | Trades | Avg PnL/trade | Win Rate | Avg Trade Size |
|---|---|---|---|---|
| Extreme Fear | 10,406 | $71.03 | 76.2% | $5,468 |
| Fear | 29,808 | **$112.63** | 87.3% | $8,041 |
| Neutral | 18,159 | $71.20 | 82.4% | $5,556 |
| Greed | 25,176 | $85.40 | 76.9% | $5,439 |
| Extreme Greed | 20,853 | $130.21 | **89.2%** | $2,780 |

A Welch's t-test comparing mean **daily total PnL** on Fear/Extreme-Fear days vs Greed/Extreme-Greed days gives:
- Fear-day mean daily PnL: **$46,025**
- Greed-day mean daily PnL: **$17,692**
- t = 2.40, **p = 0.018** (significant at α = 0.05)

This is the opposite of the naive "fear = panic = losses" assumption. On this dataset, **Fear days produced more than double the average daily profit of Greed days**, and win rates stayed high (76–89%) across every sentiment bucket rather than collapsing during Fear.

**Caveat:** this is a small, non-random sample — 32 accounts, most of whom look like active/professional Hyperliquid traders (position sizes in the thousands of USD, near-instant re-entries visible in `Start Position`). This is *not* representative of retail sentiment-driven behavior; it's closer to what a skilled or systematic trader base does when the crowd panics. The result should be read as "these particular traders monetize fear well," not "fear is safer than greed" in general.

## 2. Extreme Greed has the best win rate but smaller size — traders de-risk when euphoric

Extreme Greed shows the highest win rate (89.2%) and highest avg PnL/trade ($130.21), but the *lowest* average trade size ($2,780 — roughly half of the Fear-day average). This pattern suggests traders on this desk aren't chasing euphoric moves with size; they're taking smaller, higher-conviction bets and letting a favorable win rate compound. That's a healthier risk pattern than the "FOMO into bigger size at the top" behavior sentiment-based strategies usually try to guard against.

## 3. Volume is concentrated in Fear, not Greed

Total trading volume was highest during **Fear** ($239.7M) — nearly double Extreme Greed ($57.9M) and Extreme Fear ($56.9M) combined. Moderate fear, not panic or euphoria, is where this trader base is most active. This lines up with the "Fear" bucket also being the most common single classification in 2024 (781 of 2,645 days in the full historical index), so part of this is simply more Fear days existing — but volume-per-day would need a follow-up check to fully separate activity level from opportunity.

## 4. A small number of accounts drive most of the "Fear alpha"

Segmenting cumulative PnL by account and sentiment bucket shows the Fear-day profitability isn't evenly spread. The top 5 accounts by Fear-day PnL contributed the large majority of Fear-bucket profit, led by one account with **$1.24M** in Fear-day PnL alone. Several of these accounts were *also* profitable in Greed, but a couple (e.g. one account with $882K in Fear-day PnL vs essentially $0 in Greed) look like genuinely contrarian, sentiment-timed strategies rather than traders who simply do well in all conditions.

## 5. Practical takeaways for a trading strategy

- **Don't treat Fear as a de-risk signal by default.** For this trader population, Fear days were the most profitable and most active. A blanket "reduce exposure when Fear/Extreme Fear" rule would have cut off the best-performing regime.
- **Extreme Greed rewards smaller, selective size, not bigger bets.** Position sizing that shrinks (rather than grows) as sentiment gets more euphoric matches what the top-performing behavior in this data actually looks like.
- **Sentiment-conditioned account clustering is worth productizing.** A handful of accounts show a clear contrarian edge; identifying and following "Fear specialists" vs "all-weather" traders could be a copy-trading or signal feature.
- **Sample size is the biggest risk in this conclusion.** 32 accounts and one calendar year is not enough to treat p=0.018 as a durable edge — it's a hypothesis worth testing on a longer time window and a broader account sample before acting on it.

## Methodology Notes

- `Closed PnL` rows with value 0 represent non-closing executions (position increases) and are excluded from PnL/win-rate calculations, but included in volume figures.
- Dates were matched on calendar day (IST) between the two datasets; all 365 days of 2024 had a sentiment label.
- Outliers were trimmed at the 1st/99th percentile only for the boxplot visualization — all summary statistics use the full, untrimmed data.
