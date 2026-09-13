# ChatGPT ETF Flow Rotation

A lightweight playbook for using **ChatGPT + ETF.com data** to analyze weekly ETF fund flows, identify where investment dollars are rotating, and generate a current-month heatmap without building a separate application.

## What this project does

This workflow asks ChatGPT to:

- Research current ETF fund-flow data from **ETF.com**
- Use **ETF.com / FactSet** flow data as the primary source
- Compare the **last completed week of the prior month** with the current month's weekly data
- Aggregate daily flows when a full weekly report is not yet available
- Calculate **month-to-date (MTD)** ETF flows
- Compare major ETF asset classes
- Identify capital rotation between:
  - U.S. equities
  - International equities
  - U.S. fixed income
  - International fixed income
  - Commodities
  - Alternatives
  - Currency
  - Asset allocation
  - Leveraged ETFs
  - Inverse ETFs
- Create a **weekly ETF rotation heatmap**
- Explain the major risk-on / risk-off and allocation shifts

No local Python environment is required for the basic workflow. You can run the analysis directly in ChatGPT.

---

## Recommended GitHub repository name

```text
chatgpt-etf-flow-rotation
```

Suggested GitHub description:

> Use ChatGPT and ETF.com fund-flow data to analyze weekly ETF capital rotation, MTD trends, flow intensity, and sector momentum with heatmaps.

Suggested topics:

```text
etf
investing
fund-flows
asset-allocation
chatgpt
financial-analysis
market-rotation
heatmap
etf-com
factset
```

---

## Quick start

### 1. Open ChatGPT

Start a new ChatGPT conversation.

For current ETF flow analysis, allow ChatGPT to search the web so it can retrieve recent ETF.com information.

### 2. Paste the master prompt

Copy and paste the prompt below into ChatGPT.

```text
Analyze current ETF fund flows using ETF.com as the primary source.

OBJECTIVE
Build a weekly ETF capital-rotation view showing where investment dollars are moving across major ETF asset classes.

DATA SOURCE
1. Prioritize ETF.com ETF fund-flow data and ETF.com pages using FactSet data.
2. Use current web data and cite every material flow number.
3. Do not substitute ETF price returns for fund flows.
4. Clearly distinguish reported data from calculations you make.

TIME WINDOW
1. Include the last completed week of the prior month as the baseline.
2. Include every completed week of the current month.
3. If the current week is incomplete, aggregate the available ETF.com daily flow data.
4. Clearly label incomplete periods with an asterisk and the through-date.
5. Calculate current month-to-date flows.

TRACK THESE ETF CATEGORIES
- U.S. Equity
- International Equity
- U.S. Fixed Income
- International Fixed Income
- Commodities
- Currency
- Alternatives
- Asset Allocation
- Leveraged
- Inverse

CALCULATIONS

For each category calculate:

Weekly Net Flow
= Sum of daily ETF net flows in the period

Month-to-Date Flow
= Sum of all current-month weekly / daily flows

Week-over-Week Flow Change
= Current Week Flow - Previous Week Flow

Destination Ratio
= Destination Inflows / Absolute Value of Source Outflows

If reliable ETF-category AUM data is available, also calculate:

Flow Intensity %
= Weekly Net Flow / Category ETF AUM × 100

4-Week Momentum
= Sum of the latest four weekly net flows

Flow Acceleration
= Current Week Flow - Average of prior four weeks

OUTPUT

Create a table with:

ETF Category | Prior-Month Anchor Week | Current Week 1 | Current Week 2 | Current Partial/Completed Week | MTD

Use $ billions.

Create a heatmap:
- Rows = ETF categories
- Columns = weekly periods + MTD
- Cell value = net flow in $B
- Positive values = inflows
- Negative values = outflows
- Show the numerical value in every cell

If Flow Intensity % can be calculated reliably, create a second heatmap using Flow Intensity %.

ANALYSIS

Explain:

1. Top 3 ETF categories receiving investment dollars
2. Top 3 ETF categories losing investment dollars
3. Biggest week-over-week flow reversals
4. U.S. equity vs international equity rotation
5. Equity vs fixed-income rotation
6. Commodity and alternative-investment flows
7. Leveraged vs inverse ETF behavior
8. Whether the flow pattern indicates:
   - Risk-on
   - Risk-off
   - Diversification
   - Yield seeking
   - Geographic rotation
   - Hedging
9. Whether current moves appear to be:
   - New rotation
   - Accelerating rotation
   - Persistent allocation
   - Decelerating allocation
   - Reversal

SECTOR EXTENSION

After the asset-class analysis, analyze U.S. equity-sector ETF rotation where ETF.com data supports it.

Track:
- Technology
- Semiconductors
- Financials
- Industrials
- Energy
- Healthcare
- Biotechnology
- Consumer Discretionary
- Consumer Staples
- Communication Services
- Utilities
- Materials
- Real Estate

Representative ETFs may be used to help interpret sector direction, but do not double-count overlapping funds when estimating sector flows.

Common proxies include:
XLK, SOXX, SMH, XLF, XLI, XLE, XLV, XLY, XLP, XLC, XLU, XLB, XLRE.

FINAL SUMMARY

Finish with a concise statement of the primary investment-dollar rotation.

Use this format:

Capital Rotation:
[Source of funds] → [Destination 1] + [Destination 2] + [Destination 3]

Then state the strongest current ETF allocation signal and what would confirm or invalidate the trend next week.
```

---

## Example follow-up prompts

After ChatGPT produces the first analysis, use follow-up prompts to deepen the view.

### Refresh the analysis

```text
Refresh the ETF rotation analysis with all ETF.com data available through today.
Do not change the methodology.
Add the newest daily or weekly observations and recalculate MTD.
```

### Focus on sectors

```text
Now drill into U.S. sector ETF rotation.

Build a weekly sector heatmap using ETF.com data and representative sector ETFs where needed.

Show:
- Weekly net flow
- Week-over-week change
- MTD flow
- 4-week momentum
- Flow intensity % when AUM is available

Identify which sectors are gaining and losing investor dollars.
```

### Find emerging rotation

```text
Compare the latest week with the previous four weeks.

Identify ETF categories where:
1. flows changed from negative to positive,
2. positive flows are accelerating,
3. positive flows are decelerating,
4. flows changed from positive to negative.

Rank the strongest rotation signals.
```

### Normalize by AUM

```text
For every ETF category where reliable AUM data is available, calculate:

Flow Intensity % = Weekly Net Flow / ETF Category AUM × 100.

Create a heatmap based on Flow Intensity % rather than raw dollars.

Explain which categories have the strongest flows relative to their size.
```

### Create an investment-rotation score

```text
Create an ETF Rotation Score from -100 to +100.

Use:
- latest weekly flow
- week-over-week change
- 4-week cumulative flow
- flow acceleration
- flow intensity %
- consistency of inflows/outflows

Positive scores indicate increasing allocation.
Negative scores indicate decreasing allocation.

Rank all ETF categories from strongest accumulation to strongest distribution.
Explain the scoring methodology.
```

---

## Recommended weekly workflow

Run the workflow after ETF.com has published the final available flow data for the week.

The process should be:

```text
ETF.com daily flows
        ↓
Aggregate weekly flows
        ↓
Add prior-month anchor week
        ↓
Calculate current MTD
        ↓
Calculate week-over-week changes
        ↓
Calculate flow intensity where possible
        ↓
Calculate 4-week momentum
        ↓
Build heatmap
        ↓
Interpret capital rotation
```

If Friday data is not yet available, do not estimate it. Use the available dates and label the period as partial.

Example:

```text
Sep 8–10*
```

With a footnote:

```text
* Partial week through Sep. 10.
```

---

## Suggested output table

ChatGPT should produce something similar to:

| ETF Category | Prior Week | Week 1 | Current Week | MTD |
|---|---:|---:|---:|---:|
| U.S. Equity | +2.3 | -1.3 | -4.9 | -6.2 |
| International Equity | +9.1 | +2.2 | +6.7 | +8.9 |
| U.S. Fixed Income | +8.6 | +10.1 | +4.4 | +14.5 |
| International Fixed Income | +2.6 | +3.0 | +1.7 | +4.7 |
| Commodities | +0.9 | +2.4 | +0.6 | +3.0 |
| Alternatives | +0.1 | +1.6 | +1.5 | +3.1 |

Values above are an **illustrative layout only**. Always use current cited data when running the workflow.

---

## How to read the heatmap

The heatmap answers a simple question:

> Where are ETF investors putting incremental dollars right now?

Interpret it as:

| Signal | Meaning |
|---|---|
| Strong positive | Strong ETF inflows |
| Moderate positive | Accumulation |
| Near zero | Neutral / low conviction |
| Moderate negative | Distribution |
| Strong negative | Significant ETF outflows |

Do not interpret a positive flow as proof that the underlying asset will rise.

Fund flows describe **investor allocation behavior**, not guaranteed future performance.

---

## Raw dollars vs flow intensity

Raw ETF flows are important, but they can favor very large categories.

For example:

```text
$5B inflow into a $2T category
```

may be less significant than:

```text
$1B inflow into a $20B category.
```

That is why the enhanced workflow uses:

```text
Flow Intensity %
= Net Flow / AUM × 100
```

Use raw-dollar flows to answer:

> Where are the most dollars going?

Use flow intensity to answer:

> Where is allocation changing most aggressively relative to category size?

---

## Capital-rotation framework

A useful way to summarize the result is:

```text
SOURCE → DESTINATION
```

Examples:

```text
U.S. Equity → U.S. Fixed Income
U.S. Equity → International Equity
Growth → Value
Technology → Industrials
Long Duration → Ultra-Short Treasuries
Leveraged ETFs → Inverse / Hedging ETFs
```

The strongest signals occur when:

1. the source category has persistent outflows,
2. the destination category has persistent inflows,
3. week-over-week momentum is accelerating, and
4. the pattern persists for multiple weeks.

---

## Optional risk regime classification

Ask ChatGPT to classify the flow environment.

### Risk-on

Typical characteristics:

- Equity inflows
- Growth / technology inflows
- Small-cap inflows
- Leveraged ETF inflows
- High-yield credit inflows

### Risk-off

Typical characteristics:

- Equity outflows
- Treasury inflows
- Gold / defensive asset inflows
- Inverse ETF inflows
- Leveraged ETF outflows

### Diversification rotation

Typical characteristics:

- U.S. equity outflows or slowing inflows
- International equity inflows
- Fixed-income inflows
- Alternatives inflows
- Continued overall ETF industry inflows

A diversification rotation is not necessarily bearish.

---

## Data-quality rules

To keep results comparable from week to week:

1. Prefer ETF.com reported flows.
2. Cite the original ETF.com page for material numbers.
3. Keep ETF category definitions consistent.
4. Never mix ETF price performance with net ETF flows.
5. Never extrapolate missing trading days.
6. Clearly flag partial weeks.
7. State when values were calculated by summing ETF.com daily observations.
8. Avoid double-counting overlapping sector ETFs.
9. Keep all heatmap values in the same unit.
10. Recalculate MTD whenever a new day is added.

---

## Using your own data

You can also download or maintain an ETF-flow CSV and upload it directly to ChatGPT.

A useful structure is:

```csv
date,category,net_flow_millions,aum_millions
2026-09-08,U.S. Equity,-9021.74,
2026-09-08,U.S. Fixed Income,2077.03,
2026-09-08,International Equity,2032.68,
```

Then ask:

```text
Analyze the attached ETF flow file using the methodology in this repository.

Aggregate it weekly, calculate MTD, compute flow intensity where AUM exists, and create the weekly capital-rotation heatmap.
```

---

## Recommended recurring prompt

Use this every week:

```text
Update my ETF Rotation Dashboard through the latest ETF.com data.

Keep the last completed week of the previous month as the anchor.

Add all completed weeks of the current month and the current partial week if necessary.

Update:
- weekly net flows
- MTD flows
- week-over-week change
- 4-week momentum
- flow acceleration
- flow intensity %
- asset-class heatmap
- sector heatmap
- risk regime
- top capital rotations

Cite ETF.com for all material source data.

Do not extrapolate missing trading days.

Finish with:
Capital Rotation:
[Source] → [Destinations]
```

---

## Using Deep Research for a broader market review

For a deeper version, run the same instructions with ChatGPT's **Deep Research** capability and ask it to prioritize ETF.com while also using other reputable market sources to explain *why* the ETF flows may be occurring.

Example:

```text
Use Deep Research to analyze the ETF rotation identified by ETF.com flows.

ETF.com should remain the primary source for fund-flow numbers.

Use additional reputable sources only to investigate the macroeconomic, earnings, rates, commodity, geopolitical, or valuation factors that may explain the rotation.

Separate measured ETF-flow facts from market interpretation.
```

---

## Expected deliverables

A strong ChatGPT run should return:

1. **Weekly ETF flow table**
2. **Weekly ETF flow heatmap**
3. **Current-month MTD aggregation**
4. **Top inflow destinations**
5. **Top outflow sources**
6. **Week-over-week reversals**
7. **Equity vs fixed-income analysis**
8. **U.S. vs international analysis**
9. **Sector rotation**
10. **Risk regime assessment**
11. **4-week momentum view**
12. **Concise capital-rotation conclusion**

---

## Example final conclusion

```text
Capital Rotation:
U.S. Equity → U.S. Fixed Income + International Equity + Alternatives

Strongest signal:
Persistent fixed-income accumulation combined with weakening U.S. equity flows.

Confirmation:
Another week of positive bond and international-equity flows with continued U.S. equity outflows.

Invalidation:
A strong reversal back into U.S. equities accompanied by declining bond flows.
```

---

## Important note

This project is for research and educational use. ETF fund flows can help describe investor positioning and allocation trends, but they are not a standalone trading signal and should not be treated as personalized investment advice.

---

## ChatGPT capabilities used by this workflow

This workflow relies on capabilities available in ChatGPT such as:

- Web search for current information and citations
- File uploads for CSV/spreadsheet analysis
- Data analysis for calculations, tables, and visualizations
- Follow-up conversation to refresh or refine the same analysis

Feature availability and usage limits may vary by ChatGPT plan, workspace, region, and account configuration.

Official references:

- ChatGPT FAQ: https://help.openai.com/en/articles/12677804-what-is-chatgpt-faq
- File Uploads FAQ: https://help.openai.com/en/articles/8555545
- Deep Research: https://help.openai.com/en/articles/10500283

---

## License

Consider using the **MIT License** if you want others to freely reuse and adapt the prompt methodology.

---

## Contributing

Useful future enhancements include:

- Automated ETF.com data ingestion
- ETF category AUM normalization
- Sector-flow history
- 4-week and 13-week momentum
- Rotation scoring
- Risk-regime scoring
- Historical backtesting of flow signals
- Interactive dashboard output
- Scheduled weekly ETF-flow reports
