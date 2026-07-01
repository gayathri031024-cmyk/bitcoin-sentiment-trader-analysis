# Bitcoin Market Sentiment vs. Hyperliquid Trader Performance

Data science assignment for PrimeTrade.ai — exploring the relationship between
Bitcoin market sentiment (Fear & Greed Index) and trader performance on
Hyperliquid.

## Datasets
- **Bitcoin Fear & Greed Index** — daily sentiment score (0–100) and
  classification (Extreme Fear, Fear, Neutral, Greed, Extreme Greed),
  Feb 2018 – May 2025.
- **Hyperliquid Trader Data** — ~211,000 individual trade executions across
  32 accounts and 246 coins, including execution price, size, side,
  direction, closed PnL, and fees.

The two datasets were merged on calendar date.

## Files
| File | Description |
|---|---|
| `Trader_Sentiment_Analysis.ipynb` | Full analysis notebook — data cleaning, merging, EDA, charts, and code |
| `Trader_Sentiment_Analysis_Report.docx` | Written report with charts, tables, and strategy recommendations |

## Key Findings
1. **Non-linear "W-shaped" performance** — traders performed best during
   **Fear** (87.3% win rate) and **Extreme Greed** (89.2% win rate), and
   worst during **Extreme Fear** (76.2%) and plain **Greed** (76.9%).
   Profit factor ranged from 2.16 (Extreme Fear) to 11.0 (Extreme Greed).
2. **Fear days saw the most activity** — highest trading volume, largest
   average position size, and a negative correlation between the sentiment
   score and trade count / volume / active accounts (traders lean in harder
   as fear rises).
3. **Greed (not Extreme Greed) is the highest-risk regime** — the single
   largest loss (-$117,990) and the dataset's only forced liquidation both
   occurred on Greed days; one account lost over $184,000 in a single day
   trading TRUMP.
4. **BTC dominates trading flow** — 54% of the ~$1.19B total volume, with a
   long tail of altcoin speculation across 246 coins.

## Methodology Notes
- ~50.6% of trade rows have `Closed PnL == 0` (position-opening trades);
  performance metrics focus on the ~104,000 realized trades unless noted.
- Only one explicit liquidation event is tagged in the data — actual forced
  closes may be under-represented if recorded under generic
  Close Long/Close Short entries.
- The dataset covers 32 accounts only, so findings describe this cohort's
  behavior rather than the full Hyperliquid user base.

## How to Reproduce
```bash
pip install pandas numpy matplotlib jupyter
jupyter nbconvert --to notebook --execute --inplace Trader_Sentiment_Analysis.ipynb
```
(Place the source CSVs — `hyperliquid_trader_data_csv.csv` and
`fear_greed_index_csv.csv` — in the same folder as the notebook before running.)
