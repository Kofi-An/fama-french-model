# Fama-French 5-Factor Model

> Quantitative factor analysis decomposing stock returns
> into systematic risk factors. Rolling OLS regression,
> alpha significance testing, and factor-tilted portfolio
> construction. All five portfolios beat SPY on a
> risk-adjusted basis.

---

## Key results at a glance

| Metric | Value |
|--------|-------|
| Stocks analysed | AAPL, BRK-B, TSLA, JNJ, SPY |
| Period | 2010-01-01 to 2024-12-31 |
| Trading days | 3,773 |
| Factor model | Fama-French 5-Factor (daily) |
| Best portfolio Sharpe | 1.140 (Equal Weight) |
| SPY Sharpe | 0.831 |
| Sharpe premium | +0.309 above benchmark |
| TSLA alpha | 37.43% annualised (p=0.004) |

---

## Static factor loadings

| Ticker | Alpha (ann) | Sig | Mkt Beta | HML | RMW | R² |
|--------|------------|-----|---------|-----|-----|----|
| AAPL | 7.48% | ns | 1.148 | -0.487 | +0.588 | 0.528 |
| BRK-B | 1.19% | ns | 0.889 | +0.548 | -0.128 | 0.738 |
| TSLA | 37.43% | *** | 1.245 | -0.490 | -0.631 | 0.258 |
| JNJ | -0.60% | ns | 0.625 | -0.042 | +0.201 | 0.364 |
| SPY | -0.14% | ns | 0.984 | +0.023 | +0.056 | 0.995 |

SPY validates the model, beta 0.984 ≈ 1.0, R² = 0.995.
Only TSLA shows statistically significant alpha (p=0.004).

---

## Rolling regression findings 

Window: 756 trading days (3 years) | Step: 5 days

| Ticker | Peak Alpha | % Positive | % Significant |
|--------|-----------|------------|---------------|
| AAPL | 22.22% | 92.7% | 0.9% |
| BRK-B | 7.72% | 83.8% | 0.0% |
| TSLA | 116.68% | 92.4% | 39.9% |
| JNJ | 9.30% | 56.1% | 0.0% |
| SPY | 0.42% | 27.5% | 0.0% |

## Critical findings from rolling analysis:
- TSLA alpha peaked at 116.68% but collapsed to 12.3%
  in 2024, narrative premium eroding in real time
- AAPL HML loading drifted from +0.13 to -0.77,
  quantifying Apple's transformation from value to growth
- BRK-B: zero statistically significant windows in 14
  years, Buffett's edge is factor discipline, not alpha
- JNJ alpha: +3.5% in 2013 declining to -7.5% in 2024

---

## Alpha significance

| Ticker | Alpha | HAC sig | IR | Appraisal | Evidence | Verdict |
|--------|-------|---------|-----|-----------|---------|---------|
| AAPL | 7.47% | ns | 0.393 | 0.393 | 2/6 | Weak alpha |
| BRK-B | 1.19% | ns | 0.122 | 0.122 | 2/6 | Weak alpha |
| TSLA | 37.43% | *** | 0.757 | 0.757 | 5/6 | Strong alpha |
| JNJ | -0.60% | ns | -0.045 | -0.045 | 0/6 | No alpha |
| SPY | -0.14% | ns | -0.124 | -0.124 | 0/6 | No alpha |

---

## Portfolio construction

| Portfolio | Ann Return | Sharpe | Sortino | Max DD | CVaR 95% |
|-----------|-----------|--------|---------|--------|----------|
| Alpha-Informed | 40.41% | 1.079 | 1.572 | -54.61% | -5.02% |
| Growth+Momentum | 35.84% | 1.136 | 1.634 | -47.72% | -4.24% |
| Equal Weight | 24.44% | 1.140 | 1.542 | -34.29% | -2.94% |
| Value+Quality | 17.10% | 0.977 | 1.266 | -29.67% | -2.39% |
| SPY Benchmark | 15.23% | 0.831 | 1.016 | -33.72% | -2.59% |

All four factor portfolios outperform SPY on Sharpe ratio.
Value+Quality has the smallest drawdown (-29.67%) and
best CVaR (-2.39%), superior downside protection.

**Factor exposure verification (intended vs achieved):**
- Value+Quality: HML +0.111 ✓ RMW +0.071 ✓
- Growth+Momentum: HML -0.363 ✓

---

## The five factors

| Factor | Description | BRK-B | TSLA |
|--------|-------------|-------|------|
| Mkt-RF | Market excess return | 0.889 | 1.245 |
| SMB | Small Minus Big (size) | -0.259 | +0.397 |
| HML | High Minus Low (value) | +0.548 | -0.490 |
| RMW | Robust Minus Weak (profit) | -0.128 | -0.631 |
| CMA | Conservative Minus Aggressive | +0.003 | -0.962 |

---

## Methodology

- HAC (Newey-West) standard errors, obust to
  autocorrelation and heteroskedasticity
- 756 trading day rolling window (3-year academic
  standard for factor regressions)
- Alpha tested at 1%, 5%, 10% significance levels
- Bootstrap permutation test (1000 draws)
- Information ratio and appraisal ratio per stock
- SPY used as benchmark validation throughout
- Mean-variance efficient frontier with max-Sharpe
  and min-variance optimal portfolios

---

## Notebooks

| Notebook | Description |
|----------|-------------|
| 01_data_preparation.ipynb | FF5 download, stock prices, excess returns |
| 02_ols_regression.ipynb | Static OLS, HAC errors, factor loadings |
| 03_rolling_regression.ipynb | 3-year rolling betas, regime analysis |
| 04_alpha_analysis.ipynb | Bootstrap, IR, alpha decay, attribution |
| 05_portfolio_construction.ipynb | Efficient frontier, regime performance |

---

## Tech stack

![Python](https://img.shields.io/badge/Python-3.11-blue?style=flat)
![statsmodels](https://img.shields.io/badge/statsmodels-green?style=flat)
![numpy](https://img.shields.io/badge/numpy-orange?style=flat)
![yfinance](https://img.shields.io/badge/yfinance-purple?style=flat)
![Plotly](https://img.shields.io/badge/Plotly-red?style=flat)

---

## Data sources

- Fama-French 5-Factor data: Kenneth French Data Library
  mba.tuck.dartmouth.edu/pages/faculty/ken.french
- Stock prices: Yahoo Finance via yfinance.

---

## Limitations

- Analysis period (2010-2024) is a growth-dominated
  regime, value and size premia were negative
- Only 5 stocks, not a diversified portfolio study
- Transaction costs estimated, not observed
- Bootstrap p-values unreliable for fat-tailed
  daily return distributions with 1000 draws
- Forward-looking alpha cannot be guaranteed

---

## Related projects

- [Credit Risk Scorecard](https://github.com/Kofi-An/credit-risk-scorecard)
  — AUC 0.71, $275M loss reduction
- [Portfolio Risk Dashboard](https://kofi-an-portfolio-risk-dashboard.streamlit.app)
  — Live VaR, CVaR, Monte Carlo
- [Fraud Detection](https://github.com/Kofi-An/fraud-detection)
  — AUC-PR 0.80, 479x over random
- [Macro Dashboard](https://github.com/Kofi-An/macro-dashboard)
  — FRED + World Bank + Ghana

---

## Author

Kofi-Anku | Financial Data Scientist
Accra, Ghana | Open to remote roles globally

[GitHub](https://github.com/Kofi-An) ·
[LinkedIn](https://linkedin.com/in/kfam88) ·
[Portfolio](https://kofi-an.github.io)