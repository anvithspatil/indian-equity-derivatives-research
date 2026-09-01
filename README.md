# Indian Equity & Derivatives Research Engine

A systematic quantitative research study of the Indian equity market combining market regime analysis, equity factor selection, derivatives positioning, volatility analysis, and systematic momentum strategies.

## Research Question

Can a systematic process combining market regimes, equity fundamentals, momentum, volatility and derivatives positioning generate superior risk-adjusted characteristics in the Indian market?

## What This Project Covers

- Market regime classification
- NIFTY 50 return and volatility analysis
- India VIX analysis
- Equity quality, valuation and momentum factors
- NIFTY options open-interest analysis
- Implied-volatility analysis
- Systematic momentum strategy
- Backtesting and benchmark comparison
- Transaction-cost analysis
- Parameter robustness testing
- Risk and drawdown analysis

## Data

The research uses:

- NIFTY 50 daily market data from January 2018 to August 2026
- India VIX data
- A representative universe of 20 large-cap Indian equities
- NIFTY options-chain data for the 08-Sep-2026 expiry

## 1. Market Regime Analysis

NIFTY 50 observations were classified using two dimensions:

- 20-day market direction
- 20-day annualized volatility

This produced four regimes:

- Bullish / Low Volatility
- Bullish / High Volatility
- Bearish / Low Volatility
- Bearish / High Volatility

The combined NIFTY 50 and India VIX dataset contains 2,118 observations.

### Regime Distribution

| Market Regime | Trading Days | Percentage |
|---|---:|---:|
| Bullish / Low Volatility | 744 | 35.13% |
| Bullish / High Volatility | 558 | 26.35% |
| Bearish / High Volatility | 491 | 23.18% |
| Bearish / Low Volatility | 325 | 15.34% |

### Regime Performance

| Market Regime | Annualized Mean Daily Return | Annualized Volatility | Sharpe Ratio |
|---|---:|---:|---:|
| Bearish / High Volatility | -49.57% | 26.07% | -1.90 |
| Bearish / Low Volatility | -37.07% | 10.01% | -3.70 |
| Bullish / High Volatility | 66.49% | 16.89% | 3.94 |
| Bullish / Low Volatility | 30.66% | 9.44% | 3.25 |

The results show substantial differences in market behaviour across regimes. Bullish regimes generated positive benchmark returns, while bearish regimes generated negative returns.

## 2. Equity Factor Model

A representative universe of 20 large-cap Indian equities was ranked using three factors:

| Factor | Weight |
|---|---:|
| Quality | 35% |
| Valuation | 25% |
| Risk-adjusted Momentum | 40% |

### Quality Factor

The quality factor uses:

- Return on Equity
- Profit Margin

Quality Score:

55% ROE Score + 45% Profit Margin Score

Missing ROE observations were not imputed as zero. Where ROE was unavailable, the score was calculated from the available quality information.

### Valuation Factor

The valuation factor uses:

- Price-to-Earnings ratio
- Price-to-Book ratio

Lower relative valuation multiples receive higher percentile scores.

Valuation Score:

60% P/E Score + 40% P/B Score

### Momentum Factor

Momentum was measured using:

- 3-month return
- 6-month return
- 12-month return

Weighted momentum:

- 30% 3-month momentum
- 30% 6-month momentum
- 40% 12-month momentum

Momentum was adjusted using recent 60-day annualized volatility to obtain a risk-adjusted momentum measure.

### Current Equity Ranking

The multi-factor model produced the following top 10 ranking:

| Rank | Stock | Composite Score |
|---:|---|---:|
| 1 | SBIN | 0.783 |
| 2 | BAJFINANCE | 0.745 |
| 3 | KOTAKBANK | 0.718 |
| 4 | ICICIBANK | 0.705 |
| 5 | AXISBANK | 0.693 |
| 6 | SUNPHARMA | 0.659 |
| 7 | TCS | 0.518 |
| 8 | HCLTECH | 0.511 |
| 9 | INFY | 0.491 |
| 10 | NTPC | 0.481 |

These rankings represent a current cross-sectional analysis and are not presented as historical backtested stock-selection results.

## 3. Derivatives & Volatility Analysis

### India VIX and Future Realized Volatility

India VIX exhibited a strong positive relationship with subsequent 10-day NIFTY 50 realized volatility.

Key statistical results:

- Correlation: 0.708
- R-squared: 0.501
- P-value: < 0.001
- Regression slope: 0.0099

Average future 10-day realized volatility:

| VIX Regime | Future 10-Day Realized Volatility |
|---|---:|
| High VIX | 17.65% |
| Low VIX | 10.43% |

The relationship represents statistical association rather than causal proof and does not by itself establish a profitable trading signal.

### NIFTY Options Positioning

For the 08-Sep-2026 NIFTY expiry:

- NIFTY spot: 24,080.40
- Highest Call OI strike: 24,200
- Highest Put OI strike: 23,500
- Put-Call OI Ratio: 0.692

These open-interest concentrations represent areas of notable options positioning rather than guaranteed support or resistance levels.

## 4. Systematic Momentum Strategy

A long-only trend-following strategy was constructed using:

- 20-day moving average
- 50-day moving average
- Positive 20-day return filter

### Entry Condition

20-day MA > 50-day MA

AND

20-day return > 0

### Look-Ahead Bias Control

Trading signals were shifted by one trading day so that information available at the end of a trading day was only used for the following day's simulated return.

### Position Management

When the entry conditions were not satisfied, the strategy held no position and remained in cash.

### Strategy Rationale

The strategy was intentionally designed as a simple trend-following framework. The 20-day and 50-day moving averages capture medium-term trend direction, while the 20-day return filter provides an additional momentum condition.

The objective was not to optimize a large number of parameters or maximize historical returns. Instead, the strategy was designed to be transparent, reproducible and suitable for evaluating the relationship between trend signals, market regimes and portfolio risk.

## 5. Backtest Results

The systematic momentum strategy was evaluated against a buy-and-hold NIFTY 50 benchmark.

| Metric | NIFTY 50 | Momentum Strategy |
|---|---:|---:|
| CAGR | 9.85% | 5.56% |
| Annualized Volatility | 16.96% | 9.02% |
| Sharpe Ratio | 0.656 | 0.664 |
| Sortino Ratio | 0.797 | 0.634 |
| Maximum Drawdown | -38.44% | -16.21% |
| Win Rate | 53.76% | 55.29% |
| Market Exposure | 100% | 49.5% |

The strategy did not outperform NIFTY 50 in absolute CAGR. Its main advantage was risk reduction, with substantially lower volatility and maximum drawdown.

### Performance Across Market Regimes

| Market Regime | Strategy Annualized Mean Return | NIFTY 50 Annualized Mean Return |
|---|---:|---:|
| Bearish / High Volatility | -18.82% | -49.57% |
| Bearish / Low Volatility | -20.21% | -37.07% |
| Bullish / High Volatility | 25.02% | 66.49% |
| Bullish / Low Volatility | 19.50% | 30.66% |

The strategy captured substantially less upside than the NIFTY 50 during bullish periods, but experienced materially smaller losses during bearish periods.

### Strategy Exposure

Overall strategy exposure was approximately 49.5%.

| Market Regime | Strategy Exposure |
|---|---:|
| Bearish / High Volatility | 7.54% |
| Bearish / Low Volatility | 13.85% |
| Bullish / High Volatility | 61.65% |
| Bullish / Low Volatility | 84.95% |

The strategy's low exposure during bearish regimes is a key contributor to its defensive performance profile.

## 6. Transaction Costs & Parameter Robustness

### Transaction Cost Analysis

A simplified transaction cost of 10 basis points (0.10%) was applied whenever the strategy changed position.

| Metric | Before Costs | After 10 bps Costs |
|---|---:|---:|
| CAGR | 5.56% | 3.56% |
| Annualized Volatility | 9.02% | 9.03% |
| Sharpe Ratio | 0.664 | 0.444 |
| Sortino Ratio | 0.634 | 0.435 |
| Maximum Drawdown | -16.21% | -17.04% |

Transaction costs materially reduced risk-adjusted performance but did not eliminate the strategy's defensive characteristics.

### Moving-Average Parameter Robustness

Three moving-average configurations were tested:

| Parameters | CAGR | Volatility | Sharpe | Maximum Drawdown |
|---|---:|---:|---:|---:|
| 10 / 30 | 4.81% | 9.83% | 0.542 | -21.82% |
| 20 / 50 | 5.56% | 9.02% | 0.664 | -16.21% |
| 50 / 100 | 7.06% | 7.92% | 0.922 | -11.41% |

The defensive characteristics of the strategy persisted across the tested parameter configurations.

The 50 / 100 configuration produced the strongest tested risk-adjusted performance.

## 7. Key Findings

1. India VIX showed a strong positive association with subsequent NIFTY 50 realized volatility.
2. NIFTY 50 behaviour varied materially across market regimes.
3. The multi-factor equity model provides a transparent systematic stock-ranking framework.
4. The baseline momentum strategy reduced volatility and drawdown but did not outperform NIFTY 50 on absolute CAGR.
5. The strategy was strongly regime-dependent, reducing downside exposure while sacrificing part of the upside.
6. The strategy's defensive characteristics persisted across alternative moving-average configurations.

### Overall Research Takeaway

The evidence does not support the claim that the tested momentum strategy consistently outperforms the NIFTY 50 on an absolute-return basis.

Instead, the central result is a risk-return trade-off.

The strategy reduced market exposure during unfavourable conditions and therefore achieved substantially lower volatility and drawdown, while sacrificing a meaningful portion of the benchmark's upside.

The derivatives analysis provides complementary evidence that volatility conditions contain useful information about subsequent market behaviour.

## 8. Limitations

### Fundamental Data Limitation

The equity fundamental variables represent a current snapshot rather than a point-in-time historical dataset. Therefore, the quality and valuation scores were used for current cross-sectional equity research and were not used to claim historical backtested portfolio performance.

### Derivatives Data Limitation

The derivatives analysis is based on a NIFTY options-chain snapshot for the 08-Sep-2026 expiry rather than a complete historical options database.

### Strategy Scope

The backtested strategy is long-only and does not model short selling, leverage or complex derivatives strategies.

### Transaction Cost & Execution Assumptions

The transaction-cost model uses a simplified 10-basis-point assumption and does not fully model brokerage charges, taxes, bid-ask spreads, slippage, market impact or execution delays.

### Parameter Testing

The robustness analysis covers only three moving-average configurations and does not constitute comprehensive walk-forward validation.

### Statistical Interpretation

The India VIX relationship demonstrates statistical association rather than causality. Historical backtest performance should not be interpreted as a guarantee of future returns.

### Data & Sample Limitations

The equity analysis uses a representative sample of 20 large-cap Indian equities, while the derivatives analysis focuses on a single options expiry.

## 9. Conclusion

This study evaluated whether a systematic framework combining market-regime analysis, equity factor selection, derivatives positioning and trend-following signals could improve the risk-adjusted characteristics of an Indian equity portfolio.

The analysis found that India VIX was strongly associated with subsequent NIFTY 50 realized volatility, while the equity factor framework provided a transparent method for ranking stocks using quality, valuation and risk-adjusted momentum.

The baseline 20 / 50 momentum strategy did not outperform the NIFTY 50 in absolute returns. Its CAGR was 5.56% compared with 9.85% for the benchmark.

However, annualized volatility fell from 16.96% to 9.02%, while maximum drawdown decreased from -38.44% to -16.21%.

The results therefore suggest that the primary value of the tested strategy lies in risk control and dynamic exposure management rather than persistent benchmark outperformance.

## 10. Reproducibility & Project Structure

The research was implemented in Python using:

- Pandas
- NumPy
- Matplotlib
- SciPy
- yFinance
- Google Colab

### Project Structure

```text
indian-equity-derivatives-research/
│
├── Research_Analysis.ipynb
├── Indian_Equity_Derivatives_Research_Report.ipynb
└── README.md
```
## Research Analysis Notebook

Contains the complete analytical workflow for:

- Data collection and cleaning
- Market regime classification
- Equity factor construction
- Derivatives analysis
- Strategy construction
- Backtesting
- Risk metrics
- Transaction-cost testing
- Parameter robustness

## Research Report Notebook

Contains the presentation-focused research report covering:

- Research methodology
- Market and equity analysis
- Derivatives and volatility findings
- Backtest results
- Robustness analysis
- Key findings
- Limitations
- Conclusion

## Disclaimer

This project is an academic and quantitative research exercise. The analysis is not investment advice, and historical results do not guarantee future performance.
Research Report Notebook
Contains the presentation-focused research report with methodology, results, charts, findings, limitations and conclusion.
Disclaimer
This project is an academic and quantitative research exercise. The analysis is not investment advice, and historical results do not guarantee future performance.
