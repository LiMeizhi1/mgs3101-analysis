# Electric Vehicle Stock Analysis: Tesla, BYD, and NIO

## Research Question

How did Tesla, BYD, and NIO differ in stock performance and daily
return volatility during the same period in 2026? What business
events may help explain a significant price movement for each company?

## Team Members

| Member | GitHub Username | Main Company |
|---|---|---|
| Meizhi Li | LiMeizhi1 | Tesla |
| Anthony   | anthonylaporta5 | BYD |
| Jiayi YU  | yuj2-cloud | NIO |

Each member is responsible for their company's analysis and event
research. All members also contribute to the group comparison,
interpretation, and final review.

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

Tesla and BYD currently use `end="2026-10-12"`, while NIO uses
`end="2026-10-10"`. The end date is exclusive. These settings
produce the same observed trading-date range in the saved outputs.
We will standardize the download settings during the final review.

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

Daily return is calculated as:

`Daily return (%) = (Today's adjusted close / Previous trading day's adjusted close - 1) × 100`

The first return is missing because the dataset does not include
a previous closing price for the first observation.

Normalized prices are calculated as:

`Price index = Adjusted close / Adjusted close on the common starting date × 100`

For the group comparison, returns will be aligned by trading date.
Missing returns will not be replaced with zeros.

## Findings from the Current Notebook Outputs

The following results come from the saved notebook outputs.
They have not yet been reproduced together in a combined notebook.

| Measure | Tesla | BYD | NIO |
|---|---:|---:|---:|
| Closing-price observations | 194 | 194 | 194 |
| Valid daily returns | 193 | 193 | 193 |
| Mean daily return (%) | -0.03 | -0.11 | -0.14 |
| Daily return standard deviation (percentage points) | 2.86 | 2.38 | 3.24 |
| Minimum daily return (%) | -14.52 | -6.55 | -7.81 |
| Maximum daily return (%) | 8.46 | 8.06 | 15.38 |

### Finding 1: Daily Volatility Differed Across Companies

NIO had the highest daily return standard deviation at 3.24
percentage points, followed by Tesla at 2.86 and BYD at 2.38.
NIO therefore had the greatest daily return variability during
the observed period.

### Finding 2: Tesla Had the Largest Single-Day Decline

Tesla's minimum daily return was -14.52%, compared with -6.55%
for BYD and -7.81% for NIO. Tesla experienced the largest
single-day percentage decline among the three stocks.

### Finding 3: NIO Had the Largest Single-Day Gain

NIO's maximum daily return was 15.38%, compared with 8.46%
for Tesla and 8.06% for BYD. Its larger positive extreme,
together with its higher return standard deviation, shows that
its daily movements included substantial upside as well as downside.

These are historical observations for this sample period,
not predictions of future performance.

## Significant Price Movements

### Tesla: July 23, 2026

Tesla's adjusted closing price declined from $374.01 on July 22
to $319.69 on July 23, a daily decrease of 14.52%.

Trading volume reached 115,606,400 shares, approximately 2.97
times the previous 20-trading-day average.

The Tesla notebook investigates the preceding earnings release
as a possible explanation and contains the event-window chart,
numeric evidence, source links, and limitations.

### BYD: February 2, 2026

BYDDY declined by 6.55%, with trading volume of 5,599,500 shares.
This was approximately 3.41 times its average daily volume over
the full study period.

The BYD notebook discusses vehicle-sales news as a possible
explanation. Full source details and event-window evidence
still need to be added and verified.

The BYD volume multiple uses the full-period average, while the
Tesla multiple uses the previous 20 trading days. These ratios
are not directly comparable.

### NIO

Event selection, numeric evidence, external sources, and the
business explanation are still in progress.

## Visualizations

The current Tesla notebook contains:

- A normalized price chart for the full study period.
- A close-up price chart around the July 23 decline.
- A histogram of daily returns.

The BYD notebook contains price, daily return, and trading volume
charts.

The group still needs to complete:

- A normalized price comparison of all three stocks.
- A comparison of daily return distributions.
- A daily return correlation heatmap or return scatter plot.
- NIO's event analysis and supporting chart.

Every final chart should include a title, axis labels, and a
caption explaining its relevance to the research question.

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
6. Restart the kernel and select **Run All**.
7. An internet connection is required to download historical data.

Charts and tables are displayed inside the notebooks.
GitHub can display saved outputs, but it does not execute the code.

## Sources

- Historical stock data: [Yahoo Finance](https://finance.yahoo.com/),
  retrieved through `yfinance.download()`.
- Tesla event sources are listed in
  [tesla_analysis.ipynb](tesla_analysis.ipynb).
- Full BYD and NIO event references will be added as those
  analyses are completed.

## Work Remaining Before Submission

- [ ] Replace the two team-member name placeholders.
- [ ] Standardize download settings across notebooks.
- [ ] Complete BYD's monthly summary, event-window evidence,
      source references, and chart captions.
- [ ] Complete NIO's event analysis, sources, charts, and findings.
- [ ] Add the combined comparison and daily return correlations.
- [ ] Reproduce and verify the final results.
- [ ] Update this README to reflect completed work.
- [ ] Check that every member has at least three meaningful commits
      and that the required project stages are covered.