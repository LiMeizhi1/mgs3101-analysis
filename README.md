# Electric Vehicle Stock Analysis: Tesla, BYD, and NIO

## Research Question

How did Tesla, BYD, and NIO differ in stock performance and daily
return volatility during the same period in 2026? What business
events may help explain a significant price movement for each company?

## Business Story Overview

Our central question is how the conclusion changes with the measure and
the horizon. The three-company comparison now tests whether NIO's volatility
ranking depends on its largest day, whether the correlation ordering depends
on the three researched dates, and how the price reaction develops over the
next five trading days. This turns headline contrasts into inspectable checks.

The business cases concern different information: Tesla's investment costs,
BYD's sales, and NIO's reported profitability. The associated return and volume
patterns support possible explanations; they do not prove causes. The later
price path is examined separately rather than assigned to one announcement.

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

Our interest began with Elon Musk and the public attention surrounding Tesla.
That motivated a research question rather than a conclusion about its risk:
**Do stocks in the same EV industry show similar performance and daily-return
volatility, or do company events produce different stories?**

We chose Tesla as our starting point and added BYD and NIO, two Chinese
companies in the EV industry. This gives one U.S. company and two Chinese
companies a shared industry setting for comparison. These three securities
are a selected case study, not representative samples of the U.S., China,
or Asia. We do not test the effect of Musk's personal publicity on returns.

We compare a common date range, adjusted closes, normalized price indices,
and percentage returns. Starting each price index at 100 avoids confusing
share-price levels with performance. These methods support comparison but
do not eliminate differences in liquidity, depositary structures, or business
exposures, and do not identify the causes of return differences.

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
8. Compare middle-50% return ranges and daily standard deviations after
   excluding each stock's own largest absolute move as a sensitivity check.
9. Compare observed closing-price drawdowns and correlations excluding
   the three researched event dates.
10. Use a common trailing 20-day volume baseline and day +5 event horizon;
    decompose NIO's observed period return into multiplicative price factors.

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
All four notebooks were executed from fresh kernels during the October 17,
2026 review; see the reproducibility note below for the environment and
cache configuration.

| Measure | Tesla | BYD | NIO |
|---|---:|---:|---:|
| Closing-price observations | 194 | 194 | 194 |
| Valid daily returns | 193 | 193 | 193 |
| Mean daily return (%) | -0.03 | -0.11 | -0.14 |
| Daily return standard deviation (percentage points) | 2.86 | 2.38 | 3.24 |
| Minimum daily return (%) | -14.52 | -6.55 | -7.81 |
| Maximum daily return (%) | 8.46 | 8.06 | 15.38 |

### Findings beyond the headline rankings

**1. NIO's high variability extends beyond one favorable outlier.** Removing
each stock's largest absolute return leaves standard deviations of 3.05 pp for
NIO, 2.67 for Tesla and 2.31 for BYD, preserving the original ranking. NIO also
has the widest interquartile range (3.99 pp versus 3.60 and 2.69). This supports
a broader variability finding rather than attributing its rank to the single
15.38% gain. Exclusions are diagnostics; original observations remain in the
main charts. BYD's excluded extreme is its March 16 gain, not its case-study decline.

**2. Endpoint loss and losses along the path are different.** Tesla has the
smallest period decline (12.64%) but the worst single day (14.52%). NIO's
deepest observed closing-price drawdown is 50.95%, compared with 35.09% for
BYD and 33.95% for Tesla. For NIO, starting-to-ending loss of 30.35% therefore
does not describe the largest peak-to-later-trough decline observed within the
sample. Drawdowns use running closing-price peaks, not all-time or intraday peaks.

**3. BYD–NIO remains the strongest pair after the case dates are excluded.**
Removing July 23, February 2 and March 10 leaves 190 shared returns. BYD–NIO
correlation is 0.461, Tesla–NIO 0.263 and Tesla–BYD 0.160, compared with
0.419, 0.237 and 0.163 in the full sample. The ordering is not solely created
by the selected events. This does not establish statistical significance,
future stability, or a country or business-model explanation.

**4. Similar trading intensity does not imply the same event path.** Using
the same prior-20-day baseline, volume multiples are 2.97 for Tesla, 3.21 for
BYD and 4.06 for NIO. From the pre-event close through five trading days after
the event, changes are −17.42%, −2.99% and +20.65%, respectively. BYD's
rebound only partly recovers its initial loss; Tesla falls further; NIO retains
and extends its gain. Elevated volume measures activity, not bullishness.
The company reports are documented below [T1, T2, B1, N1]. The cases were
selected retrospectively for large moves, so they do not estimate the average
response to announcements.

**5. NIO's local gain survives the pullback, but a later decline outweighs it.**
The March 11 close remains 10.73% above March 9, and March 17 remains 20.65%
above it. The path then needs a longer horizon: the event-close-to-final-close
change is −37.19%. NIO's pre-event −3.89%, event-day +15.38%, and post-event
−37.19% multiply as price factors to produce the full-period −30.35%. They
must not be added. This establishes how the observations fit together, not
what would have happened without the report or why the later decline occurred.

The supporting code and saved tables are in the
[comparison notebook](comparison_analysis.ipynb) and
[NIO notebook](nio_analysis.ipynb).

## Answer to the Research Question

The evidence supports comparing **multiple dimensions and horizons**, rather
than assigning the three stocks one overall risk or performance ranking.
NIO's volatility contrast survives a one-extreme-day check, while Tesla's
relatively smaller endpoint decline coexists with the worst daily loss.
The strongest return relationship survives removal of the researched dates,
but the stocks are still not interchangeable examples of an EV-industry move.

Company reports help interpret the selected local events. NIO's retained
day +5 gain and subsequent larger decline show why local reaction and
longer-period performance need separate explanations. These are descriptive
findings and sensitivity checks, not causal effects or investment advice.

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
a plausible demand-related explanation. The BYD notebook contains the full citation, chart captions, and an
event-window table and chart with dated high and low adjusted closes.

The January 26–February 9 BYD event window had a highest adjusted close
of $12.95 on January 28 and a lowest of $11.22 on February 4. BYD's
event-day volume was also 3.21 times its previous 20-trading-day average.
Use that baseline when comparing with Tesla and NIO; the original 3.41
ratio uses the full sample and is not directly comparable.

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
The new horizon table also shows that the next-day close remained 10.73%
above the pre-event baseline; day +5 remained 20.65% above it. From the
event close to October 9, however, the price fell 37.19%. These observations
distinguish a locally retained gain from a later reversal without explaining
that reversal's business causes.
See the [NIO notebook](nio_analysis.ipynb) for evidence and references,
including NIO's official financial results [N1] and contemporaneous
Sina Finance / Gelonghui reporting [N2].

## Visualizations

The current Tesla notebook contains:

- A normalized price chart for the full study period.
- A close-up price chart around the July 23 decline.
- A histogram of daily returns.

The BYD notebook contains price, daily return, trading volume, and an
event-window price chart, with captions and supporting event evidence.

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
four required visualization types. BYD also includes an event-window chart
and captions for each of its four charts.

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
- Extreme days and case dates were chosen after observing returns. These
  sensitivity checks do not turn selected cases into representative samples
  or estimate abnormal returns. No significance tests or causal event study
  are claimed.
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

## Reproducibility Verification

On October 19, 2026, the revised comparison and NIO notebooks were executed
top-to-bottom from separate fresh kernels with a new download of the same
study period. Both retained their three original charts, with no error
outputs. Their added risk, correlation, event-horizon and price-factor tables
were checked against the downloaded observations. The price-factor product
also reconciles independently to the direct first-to-last price ratio.
Tesla and BYD notebooks were not edited in this analysis revision. The
earlier four-notebook verification is recorded below.

On October 17, 2026, all four notebooks completed from fresh Python kernels
in a newly created virtual environment, with no notebook error outputs and
13 saved chart images. The environment used Python 3.12, yfinance 1.7.0,
pandas 3.0.6, matplotlib 3.11.2, and ipykernel 7.4.0. The optional execution
harness used nbclient 0.11.0 and nbformat 5.11.1; these are not needed for
manual Run All in VS Code. Tested analysis dependencies are recorded in
`requirements.txt`; install with `python -m pip install -r requirements.txt`.

The first attempt failed because this review environment could not write
yfinance's default cache. Verification used `yf.set_tz_cache_location(...)`
to select a writable temporary folder before executing each notebook. This
changed the cache location, not the downloaded data or analysis. If you see
`unable to open database file`, run the following in your kernel before
Run All (the directory will be created as needed):

```python
from pathlib import Path
import yfinance as yf
yf.set_tz_cache_location(str(Path(".yfinance-cache").resolve()))
```

An additional fresh download confirmed 194 prices per stock, 193 shared
returns, the displayed rounded period changes and standard deviations,
and correlations of 0.163, 0.237, and 0.419. Yahoo Finance can revise data;
a future run is not guaranteed to be numerically identical.

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

- [x] Add BYD's full source, chart captions, and event-window identification
      code with dated high/low output and a supporting chart.
- [ ] Finish checking financial claims in the unchanged company notebooks;
      the sources used in this README and NIO explanation were readable
      during this review, but accessibility can change.
- [x] Run all four notebooks from fresh kernels in an isolated environment,
      save successful outputs, and reconcile the reported metrics (October 17, 2026).
- [ ] Confirm the repository is public and all three members are collaborators.
- [ ] Confirm every member has at least three meaningful commits and all seven
      work-item stages have an incremental commit. The reviewed local history
      contains only one Anthony Laporta commit; additional actual work is needed.
- [ ] Commit and push the final reviewed files, then submit the repository URL.
