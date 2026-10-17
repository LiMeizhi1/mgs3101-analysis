# Electric Vehicle Stock Analysis: Tesla, BYD, and NIO

## Research Question

How did Tesla, BYD, and NIO differ in stock performance and daily
return volatility during the same period in 2026? What business
events may help explain a significant price movement for each company?

## Business Story Overview

The project compares three EV securities over one shared period and asks
whether large company-event reactions tell the same story as full-period
performance. It examines a Tesla earnings-period sell-off, a BYD decline
after vehicle-sales news, and a NIO jump on its results date. Event timing,
returns, and volume support possible explanations; they do not prove causes.
The findings below connect each event to the relevant charts and sources.

## Team Members

| Member | GitHub Username | Main Company |
|---|---|---|
| Meizhi Li | LiMeizhi1 | Tesla |
| Anthony Laporta | anthonylaporta5 | BYD |
| Jiayi Yu | yuj2-cloud | NIO |

Each member is responsible for their company's analysis and event
research. The group comparison, interpretation, and final review are shared
responsibilities; actual participation must be reflected in the contribution history.

## Why We Selected These Companies

Tesla, BYD, and NIO compete in the electric vehicle industry.
Comparing them allows us to examine how companies in the same
industry can experience different stock performance and volatility.

They differ in business scale, product range, and geographic
exposure. These differences help frame our comparison, but the
stock data alone cannot determine their effects on returns.

## Data and Study Period

| Company | Yahoo Finance Ticker | Price Currency | Notebook |
|---|---|---|---|
| Tesla, Inc. | TSLA | USD | [Tesla analysis](tesla_analysis.ipynb) |
| BYD Company Limited | BYDDY | USD | [BYD analysis](byd_analysis.ipynb) |
| NIO Inc. | NIO | USD | [NIO analysis](nio_analysis.ipynb) |

We obtain historical daily data from Yahoo Finance using
`yfinance.download()`.

The project studies January 1 through October 11, 2026.
The saved datasets for all three companies contain 194 trading-day
observations from January 2 through October 9, 2026.

All three company notebooks and the comparison notebook use
`start="2026-01-01"` and `end="2026-10-12"`. The end date is exclusive,
so the requested period ends on October 11; the saved observations
end on the last trading day in that period, October 9.

All three notebooks use `auto_adjust=True`, so the `Close`
column represents adjusted closing prices.

BYD is represented by its U.S. OTC-traded depositary receipt,
BYDDY. NIO is represented by its U.S.-traded depositary shares.
Trading arrangements and liquidity can differ across securities.

## Methods

We use Python, pandas, and matplotlib to:

1. Inspect dates, row counts, column names, data types, missing
   values, and duplicate dates.
2. Calculate daily percentage returns separately for each stock.
3. Report count, mean, median, minimum, maximum, and standard
   deviation for adjusted closing prices and daily returns.
4. Calculate monthly average adjusted closing prices.
5. Investigate at least one significant price movement per company.
6. Compare normalized prices and daily return distributions.
7. Calculate correlations between the companies' daily returns.

### Data Handling and Visualization Tools

The visualization tools are **matplotlib and pandas plotting** in Python.
Charts and tables are embedded in the saved Jupyter notebooks; no Power BI
or Tableau files are needed for this chosen workflow.

The notebooks report missing values and duplicate dates and sort data by
date. The saved company outputs report neither missing raw observations
nor duplicate dates, so no imputation or duplicate removal was needed.
The initial missing return is expected and is excluded from return statistics.
The comparison uses `pct_change(fill_method=None)` and complete shared
return dates for correlation; missing returns are not converted to zeros.
Large returns are retained rather than removed, because they are the events
being investigated. No news explanation is inferred from price alone.

Daily return is calculated as:

`Daily return (%) = (Today's adjusted close / Previous trading day's adjusted close - 1) × 100`

The first return is missing because the dataset does not include
a previous closing price for the first observation.

Normalized prices are calculated as:

`Price index = Adjusted close / Adjusted close on the common starting date × 100`

For the group comparison, returns are aligned by trading date.
Missing returns are not replaced with zeros; the correlation matrix uses
193 dates with valid returns for all three stocks.

## Findings from the Current Notebook Outputs

The following results come from the saved notebook outputs.
The [comparison notebook](comparison_analysis.ipynb) contains the combined
price comparison, return statistics, boxplot, and correlation matrix.
A fresh end-to-end run is still required before submission.

| Measure | Tesla | BYD | NIO |
|---|---:|---:|---:|
| Closing-price observations | 194 | 194 | 194 |
| Valid daily returns | 193 | 193 | 193 |
| Mean daily return (%) | -0.03 | -0.11 | -0.14 |
| Daily return standard deviation (percentage points) | 2.86 | 2.38 | 3.24 |
| Minimum daily return (%) | -14.52 | -6.55 | -7.81 |
| Maximum daily return (%) | 8.46 | 8.06 | 15.38 |

### Three Findings Linking Data, Charts, and Business Explanations

1. **Tesla: the earnings-period decline was unusually large and active.**
   The Tesla event-window chart shows the July 23 decline of 14.52%; the
   group boxplot places it below the other stocks' worst daily returns.
   Volume was 2.97 times the prior 20-day average. Tesla released results
   on July 22 [T1], and Reuters reported investment-related cash burn [T2].
   The timing and trading activity are consistent with concerns about
   profitability and investment costs, but cannot isolate the cause.

2. **BYD: the sales-news decline coincided with elevated trading.**
   The BYD daily-return chart shows February 2 at -6.55%, and its volume
   chart shows 5,599,500 shares, 3.41 times the full-period average.
   Reuters reported January sales down 30.1% on February 1 [B1], before
   the next U.S. trading session. The negative return and high activity
   fit a demand-concern explanation. The report concerns company sales,
   not a direct measurement of BYDDY investor motives; the full-period
   volume baseline also includes observations after the event.

3. **NIO: the profitability report fits the March jump, not the whole trend.**
   The NIO event chart and return histogram highlight March 10 at +15.38%,
   with volume 4.06 times the prior 20-day average. Official results [N1]
   showed positive quarterly net profit. Tesla +0.14% and BYD -1.84%
   that day provide a contrasting peer check, consistent with NIO-specific
   news but not excluding market influences. The normalized comparison
   chart ends NIO at -30.35% for the full period, showing why one event
   explanation cannot account for the entire sample.

### Further Descriptive Comparisons

Tesla had the smallest full-period decline (-12.64%), followed by BYD
(-24.09%) and NIO (-30.35%). BYD and NIO had the highest return correlation
(0.419); Tesla's correlations with BYD (0.163) and NIO (0.237) were weaker.
These describe performance and co-movement; they do not establish why
prices changed.

## Significant Price Movements

### Tesla: July 23, 2026

Tesla's adjusted closing price declined from $374.01 on July 22
to $319.69 on July 23, a daily decrease of 14.52%.

Trading volume reached 115,606,400 shares, approximately 2.97
times the previous 20-trading-day average.

Tesla published its Q2 results on July 22 [T1]. Reuters reported negative
free cash flow alongside increased investment [T2]. These provide a
plausible investment-cost explanation to investigate alongside the next-day
sell-off, without showing that cash burn alone caused it. The Tesla notebook
contains the event-window chart and additional analysis.

### BYD: February 2, 2026

BYDDY declined by 6.55%, with trading volume of 5,599,500 shares.
This was approximately 3.41 times its average daily volume over
the full study period.

Reuters reported on February 1 that January vehicle sales fell 30.1%
year over year [B1]. This preceded the February 2 U.S. session and offers
a plausible demand-related explanation. The BYD notebook still needs its
own full citation, chart captions, and clearly defined event-window evidence.

The BYD volume multiple uses the full-period average, while the
Tesla multiple uses the previous 20 trading days. These ratios
are not directly comparable.

### NIO: March 10, 2026

NIO's adjusted close rose from $4.94 on March 9 to $5.70 on March 10,
a gain of 15.38%, its largest absolute daily return in the sample.
Volume reached 147,968,700 shares, 4.06 times the previous 20-day average.
Within March 3–17, the lowest close was $4.59 on March 3 and the highest
was $6.03 on March 16. A 4.04% pullback on March 11 preceded the recovery.

NIO released its Q4 2025 results on March 10. Reporting described its
first quarterly net profit, providing a plausible profitability-related
explanation for the jump. The timing and volume fit that explanation,
but do not establish causation. Tesla gained 0.14% and BYD fell 1.84%
that day; this contrast does not rule out market or industry influences.
See the [NIO notebook](nio_analysis.ipynb) for evidence and references,
including NIO's official financial results [N1] and contemporaneous
Sina Finance / Gelonghui reporting [N2].

## Visualizations

The current Tesla notebook contains:

- A normalized price chart for the full study period.
- A close-up price chart around the July 23 decline.
- A histogram of daily returns.

The BYD notebook contains price, daily return, and trading volume
charts.

The [comparison notebook](comparison_analysis.ipynb) contains:

- **Three-stock normalized price chart:** all three ended below their
  starting levels; Tesla had the smallest decline.
- **Daily return boxplot:** NIO had the greatest standard deviation,
  while Tesla had the largest negative daily return.
- **Correlation heatmap:** BYD and NIO were the most closely related
  pair, though their correlation was only moderate.

The [NIO notebook](nio_analysis.ipynb) contains a March 3–17 event-window
chart, a full-period normalized price chart, and a return histogram,
with captions connecting the March 10 jump to the wider price pattern.
Together with the Tesla event-window chart, the project contains all
four required visualization types. BYD's chart captions remain to be added.

### One-Sentence Captions for the NIO and Group Charts

| Notebook / chart | Caption explaining the finding and its relevance |
|---|---|
| Comparison: normalized prices | Normalized prices show Tesla declining 12.64%, BYD 24.09%, and NIO 30.35%, placing the company-event stories within a shared period in which every security ended below its starting level. |
| Comparison: daily-return boxplot | The boxplot compares the return distributions, highlighting NIO's largest positive daily return and Tesla's largest negative one and motivating research into the different company events behind those extremes. |
| Comparison: correlation heatmap | The heatmap shows a moderate BYD–NIO return correlation of 0.419 and weaker Tesla correlations, explaining why sharing the EV industry does not make the three event stories interchangeable. |
| NIO: March 3–17 event window | NIO's event chart marks the March 10 gain of 15.38%, next-day pullback, and later window high, showing the timing and persistence of the price response investigated alongside its profitability report. |
| NIO: full-period normalized price | NIO's normalized price ends the sample down 30.35% despite the March jump, showing that the earnings-event explanation does not explain the full-period decline. |
| NIO: daily-return histogram | NIO's histogram places the March 10 gain in the far positive tail, supporting its selection as an unusual day for business-event research. |

### How the Time-Based Summary Supports the Story

NIO's pandas monthly `groupby` table shows average adjusted close rising
from $4.72 in January to $6.40 in April, then falling to $3.67 in September.
This puts the March event into a broader rise-and-decline pattern rather
than treating a positive earnings-day return as evidence of lasting gains.
October's $3.46 average covers only seven trading days and is not a complete
month. Monthly average price levels are not monthly percentage returns.

## Limitations

- The sample covers only part of 2026 and may not represent
  long-term performance.
- October is a partial month containing seven trading days.
- Correlation measures co-movement and does not establish causation.
- Several company, industry, and market events can occur together.
  News timing alone cannot prove the cause of a price movement.
- Depositary securities and differences in liquidity can affect
  comparisons.
- Data retrieved again from Yahoo Finance may change because of
  revisions or price adjustments.
- Mean daily returns are arithmetic averages and should not be
  interpreted as cumulative period returns.

### Open Questions

- How much of each event-day return would remain after accounting for a
  broad-market benchmark and an EV-industry benchmark?
- Were there other same-day announcements or changes in expectations that
  could explain part of the price and volume response?
- Would the conclusions change with a longer sample or another event-window
  length, and what explains NIO's later decline after its March results?

These questions remain unanswered by the current descriptive analysis.

## How to Run

1. Install Python and VS Code.
2. Install the Python and Jupyter extensions in VS Code.
3. Clone this repository:

   ```bash
   git clone https://github.com/LiMeizhi1/mgs3101-analysis.git
   cd mgs3101-analysis
   ```

4. Install the required packages:

   ```bash
   python -m pip install yfinance pandas matplotlib ipykernel
   ```

5. Open a notebook in VS Code and select the Python environment
   where the packages were installed.
6. Run `tesla_analysis.ipynb`, `byd_analysis.ipynb`, `nio_analysis.ipynb`,
   and `comparison_analysis.ipynb` separately. For each, restart the kernel,
   select **Run All**, check for errors, and save the resulting outputs.
   The notebooks download their own inputs and do not require a shared kernel.
7. An internet connection is required to download historical data.

Charts and tables are displayed inside the notebooks.
GitHub can display saved outputs, but it does not execute the code.

## Sources

- Historical stock data: [Yahoo Finance](https://finance.yahoo.com/),
  retrieved through `yfinance.download()`; daily figures in this summary
  refer to the saved notebook outputs.
- [T1] Tesla Investor Relations. [Tesla Releases Second Quarter 2026
  Financial Results](https://ir.tesla.com/press-release/tesla-releases-second-quarter-2026-financial-results). July 22, 2026.
- [T2] Reuters. [Elon Musk's Tesla posts cash burn as capex surges on AI,
  robotaxi push](https://www.investing.com/news/stock-market-news/elon-musks-tesla-posts-cash-burn-as-capex-surges-on-ai-robotaxi-push-4806872). July 22, 2026. Published through Investing.com.
- [B1] Reuters. [China's BYD vehicle sales fall for fifth month in a row](https://ca.investing.com/news/stock-market-news/chinas-byd-vehicle-sales-fall-for-fifth-month-in-a-row-4430774).
  February 1, 2026. Published through Investing.com.
- [N1] NIO Inc. [NIO Inc. Reports Unaudited Fourth Quarter and Full Year
  2025 Financial Results](https://ir.nio.com/news-releases/news-release-details/nio-inc-reports-unaudited-fourth-quarter-and-full-year-2025/). March 10, 2026.
- [N2] Sina Finance / Gelonghui. [Premarket reaction to NIO's Q4 results](https://finance.sina.com.cn/stock/bxjj/2026-03-10/doc-inhqpaek6240600.shtml).
  March 10, 2026. This report concerns premarket trading; our 15.38% figure
  is the saved daily close-to-close return.

## Work Remaining Before Submission

- [ ] Add the reference above to BYD's own notebook, complete its chart captions and
      event-window evidence. A BYD monthly table would be optional additional
      coverage; the project already includes time-grouped summaries.
- [ ] Finish checking financial claims in the unchanged company notebooks;
      the sources used in this README and NIO explanation were readable
      during this review, but accessibility can change.
- [ ] Restart and run all four notebooks from beginning to end in a clean
      environment, save outputs, and reconcile any changed data with the text.
- [ ] Confirm the repository is public and all three members are collaborators.
- [ ] Confirm every member has at least three meaningful commits and all seven
      work-item stages have an incremental commit. The reviewed local history
      contains only one Anthony Laporta commit; additional actual work is needed.
- [ ] Commit and push the final reviewed files, then submit the repository URL.
