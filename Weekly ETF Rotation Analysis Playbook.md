# Weekly ETF Rotation Analysis Playbook

## Objective

Build a weekly ETF fund-flow view that identifies where investment dollars are rotating across major asset classes and, optionally, industry sectors.

The output should include:

- Weekly ETF net flows
- Current-month-to-date aggregated flows
- Prior-month final week as a comparison anchor
- A heatmap showing inflows and outflows
- Commentary explaining the major capital-rotation themes

---

## 1. Primary Data Source

Use **ETF.com ETF Fund Flows** as the primary source.

Useful ETF.com sections include:

- Daily ETF Flows
- Weekly ETF Flows
- Monthly ETF Flows
- ETF sector flow reports

ETF.com flow data is generally sourced from **FactSet**.

Use **net fund flows**, not ETF price performance, when analyzing investment-dollar rotation.

---

## 2. Standard ETF Categories

Track the following asset classes consistently:

| Category | Purpose |
|---|---|
| U.S. Equity | Domestic equity allocation |
| International Equity | Geographic diversification |
| U.S. Fixed Income | Domestic bond allocation |
| International Fixed Income | Global bond exposure |
| Commodities | Gold, energy, agriculture, broad commodities |
| Alternatives | Managed futures, option strategies, alternative exposures |
| Currency | Currency and crypto-related ETF exposure where classified |
| Asset Allocation | Multi-asset ETFs |
| Leveraged | Leveraged directional exposure |
| Inverse | Downside / hedging exposure |

Do not change categories between weeks unless ETF.com changes its classification methodology.

---

## 3. Weekly Time Windows

For the current month, create columns using completed weeks.

Example:

```text
Aug 24–28
Sep 1–4
Sep 8–11
Sep 14–18
Sep 21–25
Sep 28–30
Sep MTD
```

If the month starts without sufficient historical context, always include:

> Last completed week of the previous month.

This provides a baseline for identifying whether flows are accelerating, reversing, or continuing.

For a partial current week, label it clearly:

```text
Sep 8–10*
```

And add:

```text
*Partial week through September 10.
```

Never represent partial-week data as a completed week.

---

## 4. Aggregate Daily ETF Flows

When ETF.com has daily data but has not yet published the weekly report, aggregate daily flows.

For each ETF category:

```text
Weekly Net Flow
=
Monday Flow
+ Tuesday Flow
+ Wednesday Flow
+ Thursday Flow
+ Friday Flow
```

Example:

```text
U.S. Fixed Income

Sep 8    +$2.08B
Sep 9    +$1.76B
Sep 10   +$0.52B
-----------------
Partial Week = +$4.36B
```

Use the same method for every asset class.

---

## 5. Calculate Month-to-Date Flows

Calculate current-month flows as:

```text
MTD Flow
=
Week 1
+ Week 2
+ Week 3
+ Week 4
+ Partial Week
```

Example:

```text
U.S. Fixed Income

Sep 1–4     +$10.11B
Sep 8–10     +$4.36B
--------------------
September MTD = +$14.47B
```

---

## 6. Build the Core Data Table

Create a table such as:

| ETF Category | Prior Week | Week 1 | Current Week | MTD |
|---|---:|---:|---:|---:|
| U.S. Equity | +2.3 | -1.3 | -4.9 | -6.2 |
| International Equity | +9.1 | +2.2 | +6.7 | +8.9 |
| U.S. Fixed Income | +8.6 | +10.1 | +4.4 | +14.5 |
| International Fixed Income | +2.6 | +3.0 | +1.7 | +4.7 |
| Commodities | +0.9 | +2.4 | +0.6 | +3.0 |
| Alternatives | +0.1 | +1.6 | +1.5 | +3.1 |

Use **$ billions** as the standard unit.

Convert ETF.com values reported in millions using:

```text
Flow ($B) = Flow ($M) / 1,000
```

---

## 7. Create the Heatmap

### Rows

ETF asset classes.

### Columns

Weekly periods plus MTD.

### Cell values

Net ETF flows in $ billions.

Example:

```text
                      Aug 24–28   Sep 1–4   Sep 8–10   Sep MTD

U.S. Equity              +2.3       -1.3       -4.9       -6.2
International Equity     +9.1       +2.2       +6.7       +8.9
U.S. Fixed Income        +8.6      +10.1       +4.4      +14.5
```

Heatmap interpretation:

```text
Strong positive = strong capital inflow
Near zero       = neutral
Strong negative = capital outflow
```

Keep the same scale across periods where practical so week-to-week changes remain visually comparable.

---

## 8. Calculate Weekly Flow Change

To detect acceleration and reversal:

```text
Weekly Change
=
Current Week Flow
-
Previous Week Flow
```

Example:

```text
U.S. Equity

Previous week = -$1.3B
Current week  = -$4.9B

Flow change = -$3.6B
```

Interpretation:

> U.S. equity outflows accelerated by approximately $3.6B.

For fixed income:

```text
Previous = +$10.1B
Current  = +$4.4B

Change = -$5.7B
```

Interpretation:

> Fixed-income inflows remained positive but slowed from the previous week.

---

## 9. Identify Capital Rotation

Do not analyze categories independently.

Compare where money is leaving against where money is arriving.

For example:

```text
U.S. Equity MTD             -$6.2B
U.S. Fixed Income          +$14.5B
International Equity        +$8.9B
International Fixed Income  +$4.7B
Alternatives                +$3.1B
```

Translate this into:

> Capital is rotating away from U.S. equities toward fixed income, international equities, and alternative strategies.

---

## 10. Calculate Destination Ratios

A useful rotation metric is:

```text
Destination Ratio
=
Destination Inflows
/
Absolute Value of Source Outflows
```

Example:

```text
U.S. Fixed Income = +$14.5B
U.S. Equity       = -$6.2B

14.5 / 6.2 = 2.34x
```

Interpretation:

> U.S. fixed-income ETF inflows are approximately 2.3× the magnitude of U.S. equity ETF outflows.

This helps distinguish major allocation shifts from normal weekly noise.

---

## 11. Add Flow Intensity %

Raw dollars can be misleading because ETF categories have very different asset bases.

Calculate:

```text
Flow Intensity %
=
Weekly Net Flow
/
Category ETF AUM
× 100
```

Example:

```text
Weekly Flow = $4B
ETF AUM = $200B

Flow Intensity = 2%
```

A smaller ETF category receiving $2B may therefore represent a much stronger signal than a $5B inflow into a trillion-dollar category.

Create a second heatmap using **Flow Intensity %** when AUM data is available.

---

## 12. Sector-Level Extension

Repeat the same framework for U.S. equity sectors.

Recommended rows:

```text
Technology
Semiconductors
Financials
Industrials
Energy
Healthcare
Biotechnology
Consumer Discretionary
Consumer Staples
Communication Services
Utilities
Materials
Real Estate
```

Use ETF.com sector-flow data where available.

When necessary, representative ETFs can help identify direction:

```text
Technology               XLK
Semiconductors            SOXX / SMH
Financials                XLF
Industrials               XLI
Energy                    XLE
Healthcare                XLV
Consumer Discretionary    XLY
Consumer Staples          XLP
Utilities                 XLU
Materials                 XLB
Real Estate               XLRE
Communication Services    XLC
```

Avoid double-counting overlapping ETFs when calculating total sector dollars.

---

## 13. Classify Rotation Signals

Assign each category one of five simple signals:

```text
Strong Inflow
Moderate Inflow
Neutral
Moderate Outflow
Strong Outflow
```

Example thresholds can be based on Flow Intensity:

```text
> +1.0%       Strong Inflow
+0.25–1.0%    Moderate Inflow
-0.25–0.25%   Neutral
-1.0–-0.25%   Moderate Outflow
< -1.0%       Strong Outflow
```

Adjust thresholds after observing several months of actual ETF-flow distributions.

---

## 14. Calculate Momentum

For each ETF category calculate:

```text
4-Week Momentum
=
Week 1
+ Week 2
+ Week 3
+ Week 4
```

Optionally calculate acceleration:

```text
Flow Acceleration
=
Current Week
-
4-Week Average
```

This helps distinguish:

```text
New rotation
Accelerating rotation
Persistent allocation
Decelerating allocation
Reversal
```

---

## 15. Weekly Commentary Template

Use the following structure.

### Market Rotation

> ETF flows this week indicate a rotation from **[source category]** toward **[destination categories]**.

### Biggest Outflow

> **[Category]** experienced approximately **$XB** of net outflows versus **$YB** in the previous week.

### Biggest Destination

> **[Category]** attracted approximately **$XB**, making it the largest destination for ETF capital.

### Geographic Rotation

> International equity flows were **+$XB** compared with **-$YB / +$YB** for U.S. equities, suggesting **increasing/decreasing geographic diversification**.

### Risk Signal

Evaluate:

```text
Equity flows
Bond flows
Commodity flows
Alternatives
Leveraged flows
Inverse flows
```

Example interpretation:

> Positive fixed-income and inverse ETF flows combined with negative leveraged ETF flows indicate a moderately more defensive investor posture.

---

## 16. Recommended Final Dashboard

Maintain four views.

### View 1 — Weekly Dollar Flow Heatmap

```text
ETF Category × Week
Metric = Net Flow ($B)
```

Shows where dollars are moving.

### View 2 — Flow Intensity Heatmap

```text
ETF Category × Week
Metric = Net Flow / AUM %
```

Shows how significant the flow is relative to category size.

### View 3 — 4-Week Momentum

```text
Category
4-week cumulative flow
Weekly acceleration
Flow intensity
```

Shows persistence.

### View 4 — Sector Rotation

```text
Technology
Semiconductors
Financials
Energy
Industrials
Healthcare
Consumer sectors
Utilities
Materials
Real Estate
```

Shows where money is rotating within equities.

---

## 17. Recommended Weekly Output

Produce the analysis in this order:

```text
1. Weekly ETF Flow Heatmap
2. Current Month MTD Table
3. Top 3 Inflow Categories
4. Top 3 Outflow Categories
5. Biggest Week-over-Week Changes
6. U.S. vs International Rotation
7. Equity vs Fixed Income Rotation
8. Risk-On / Risk-Off Assessment
9. Sector Rotation
10. 4-Week Momentum Signal
```

End with a concise summary such as:

> ETF flows currently indicate a rotation from U.S. equity exposure toward fixed income and international equities. The strongest persistent destination is U.S. fixed income, while international equities are also gaining share. Within U.S. equities, flows should be examined at the sector level because technology and semiconductor exposure may behave differently from broad-market equity ETFs.

---

## 18. Weekly Update Rule

Run this process after the final ETF.com daily flow report of each week becomes available.

For incomplete weeks:

```text
Use available daily observations
Label them as partial
Do not annualize or extrapolate missing days
```

At month-end:

```text
Replace MTD with Final Month
Start the following month with the last full week of the prior month as the anchor
```

This maintains continuity in the heatmap and makes rotation changes immediately visible.