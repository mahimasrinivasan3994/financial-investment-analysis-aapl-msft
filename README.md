# 📈 Financial Investment Analysis — Apple (AAPL) vs Microsoft (MSFT) vs S&P 500

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![Excel](https://img.shields.io/badge/Microsoft%20Excel-Analysis-217346?logo=microsoft-excel)
![Yahoo Finance](https://img.shields.io/badge/Data-Yahoo%20Finance-purple)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

> **A comprehensive risk-return investment analysis of Apple Inc. and Microsoft Corp. benchmarked against the S&P 500 — using beta, volatility, correlation, and regression modeling to guide data-driven portfolio decisions.**

---

## 📌 Problem Statement

Technology stocks are among the most actively traded equities globally, yet their risk-return profiles relative to the broader market are often misunderstood by retail and institutional investors alike. Simply tracking price trends is insufficient for informed portfolio decision-making.

This project conducts a **rigorous financial analysis** of two of the world's largest companies — **Apple (AAPL)** and **Microsoft (MSFT)** — benchmarked against the **S&P 500 Index (^GSPC)**, to answer:
- How do these stocks perform on a **risk-adjusted** basis relative to the market?
- How **correlated** are they with each other and the broader index?
- What does **beta** tell us about their market sensitivity?
- Where are the significant **volume anomalies** and what events triggered them?
- How should investors position these stocks within a diversified portfolio?

---

## 🎯 Objectives

| # | Objective |
|---|-----------|
| 1 | Compare daily and annual returns across AAPL, MSFT, and S&P 500 |
| 2 | Analyze volatility and risk profiles for each asset |
| 3 | Compute Beta and R² through regression analysis |
| 4 | Identify trading volume outliers and link them to market events |
| 5 | Build a correlation matrix to assess diversification potential |
| 6 | Provide actionable investment strategy recommendations |

---

## 🏗️ System Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                     ANALYSIS PIPELINE                            │
│                                                                  │
│  Yahoo Finance (yfinance API)                                    │
│  └── AAPL, MSFT, ^GSPC | Jan 2023 – Apr 2025 (1699 records)    │
│                │                                                 │
│                ▼                                                 │
│  Python — Data Cleaning & Preparation                           │
│  ├── Load individual ticker sheets                               │
│  ├── Remove missing values (non-trading days)                   │
│  ├── Convert to float data types                                │
│  ├── Tag tickers (AAPL / MSFT / ^GSPC)                         │
│  ├── Merge into consolidated master dataset                     │
│  ├── Calculate daily returns (Adj Close based)                  │
│  └── Export: Cleaned_Stock_Data_AAPL_MSFT_SP500.xlsx           │
│                │                                                 │
│                ▼                                                 │
│  Microsoft Excel — Calculations & Visualizations                │
│  ├── Annual Return = AVG(Daily Return) × 252                   │
│  ├── Annual Volatility = STDEV(Daily Return) × √252            │
│  ├── Beta = Regression slope (stock vs market)                  │
│  ├── R² = Coefficient of determination                          │
│  └── Correlation matrix                                         │
│                │                                                 │
│                ▼                                                 │
│  Visual Analytics                                                │
│  ├── Price trend lines                                          │
│  ├── Histogram (price frequency distribution)                   │
│  ├── Annual return vs volatility (clustered bar)                │
│  ├── Risk vs return scatter plot                                │
│  ├── Beta regression lines                                      │
│  └── Correlation heatmap                                        │
└──────────────────────────────────────────────────────────────────┘
```

---

## 💡 Solution Approach

### 1. Data Collection & Cleaning

| Step | Detail |
|------|--------|
| Source | Yahoo Finance via `yfinance` Python library |
| Period | January 1, 2023 – April 2025 |
| Records | **1,699 daily trading records** |
| Columns | Date, Open, High, Low, Close, Adj Close, Volume |
| Cleaning | Removed NaN rows, converted all numerics to float, added Ticker column |
| Output | `Cleaned_Stock_Data_AAPL_MSFT_SP500.xlsx` (3 separate sheets + Combined) |

### 2. Key Financial Metrics Computed

| Metric | Formula |
|--------|---------|
| **Daily Return** | `(Today's Price − Yesterday's Price) / Yesterday's Price` |
| **Annual Return** | `AVERAGE(Daily Returns) × 252` |
| **Annual Volatility** | `STDEV(Daily Returns) × √252` |
| **Beta** | Slope from regression of stock daily returns vs S&P 500 daily returns |
| **R²** | Coefficient of determination from the same regression |

### 3. Volume Outlier Detection
Applied the **Interquartile Range (IQR)** method to identify statistically extreme trading days — days where institutional or retail activity spiked well beyond normal ranges.

---

## 📊 Results & Key Findings

### A. Price Trend Analysis (2023 – Q1 2025)
- All three assets showed **consistent growth from 2023 into 2024**, reflecting positive market sentiment
- **Sharp decline in Q1 2025** across all three — likely driven by macroeconomic corrections or market-wide volatility
- MSFT consistently maintained **higher adjusted closing prices** than AAPL throughout the period
- S&P 500 values dwarf individual stocks (aggregate of 500 companies) but serve as a trajectory benchmark

### B. Annual Return & Volatility

| Asset | Annual Return | Annual Volatility |
|-------|--------------|------------------|
| **AAPL** | -22.97% | 70.77% |
| **MSFT** | -22.91% | 70.62% |
| **S&P 500** | -30.91% | 68.20% |

> 📌 While all three recorded negative returns during the observed period (reflecting a broader market downturn), **AAPL and MSFT outperformed the S&P 500 by ~8%**, indicating relative tech stock resilience despite higher individual volatility.

### C. Beta & R² (AAPL vs S&P 500)

| Metric | Value | Interpretation |
|--------|-------|----------------|
| **Beta** | **0.9324** | Slightly less volatile than the market — for every 1% S&P 500 move, AAPL moves ~0.93% |
| **R²** | **0.9361** | 93.6% of AAPL's daily return variance is explained by S&P 500 movements |

> AAPL and MSFT both have Beta ≈ **1.08** on a broader summary basis — slightly more market-sensitive, but offering better relative returns.

### D. Correlation Matrix

| | AAPL | MSFT | S&P 500 |
|---|------|------|---------|
| **AAPL** | 1.000 | 0.947 | 0.968 |
| **MSFT** | 0.947 | 1.000 | 0.971 |
| **S&P 500** | 0.968 | 0.971 | 1.000 |

> ⚠️ Extremely high correlations (~0.95–0.97) indicate **limited diversification benefit** when holding AAPL, MSFT, and the S&P 500 together — they move in near-lockstep.

### E. Volume Outlier Analysis

**Top 5 Outlier Days:**

| Ticker | Date | Volume | Likely Driver |
|--------|------|--------|---------------|
| AAPL | Sep 20, 2024 | 318,679,900 | Triple witching + product cycle |
| AAPL | Jun 21, 2024 | 246,421,400 | Triple witching day |
| MSFT | Dec 15, 2023 | 78,478,200 | OpenAI/AI partnership speculation |
| S&P 500 | Mar 21, 2025 | 9,367,460,000 | Institutional rebalancing / Fed event |
| S&P 500 | Apr 4, 2025 | 8,853,500,000 | Macro shock / correction event |

### F. Risk vs Return Summary

```
High Risk, Negative Return Zone (All Three Assets):
├── AAPL:    Volatility 70.77% | Return -22.97% | Beta ~1.08
├── MSFT:    Volatility 70.62% | Return -22.91% | Beta ~1.08
└── S&P 500: Volatility 68.20% | Return -30.91% | Beta 1.00

→ AAPL and MSFT: Higher risk, but relatively better return than the market
→ S&P 500: Lower risk, but worst return — poor risk-reward in this period
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Python 3.x** | Data extraction, cleaning, statistical analysis |
| **yfinance** | Yahoo Finance API for historical OHLCV data |
| **Pandas** | Data manipulation, merging, return calculations |
| **NumPy** | Statistical computations (IQR, std dev) |
| **Matplotlib / Seaborn** | Preliminary visualization and outlier plots |
| **Microsoft Excel** | Financial metric calculations, regression, dashboards |

---

## 📁 Project Structure

```
financial-investment-analysis/
│
├── data/
│   ├── raw/
│   │   └── stock_data_raw.xlsx              # Raw Yahoo Finance data
│   └── cleaned/
│       └── Cleaned_Stock_Data_AAPL_MSFT_SP500.xlsx  # Cleaned + Combined
│
├── notebooks/
│   └── stock_analysis.ipynb                # Python: data pull, cleaning, outliers
│
├── excel/
│   └── financial_metrics.xlsx              # Returns, volatility, beta, R², correlation
│
├── visuals/
│   ├── price_trend_lines.png               # AAPL vs MSFT vs S&P 500 price trends
│   ├── price_histogram.png                 # Price frequency distribution
│   ├── annual_return_volatility.png        # Clustered bar chart
│   ├── risk_return_scatter.png             # Risk vs Return positioning
│   ├── beta_regression_aapl.png            # AAPL regression vs S&P 500
│   ├── beta_regression_msft.png            # MSFT regression vs S&P 500
│   ├── correlation_heatmap.png             # Correlation matrix heatmap
│   └── volume_outlier_boxplots.png         # IQR outlier visualization
│
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install yfinance pandas numpy matplotlib seaborn openpyxl
```

### Run Data Extraction
```bash
git clone https://github.com/yourusername/financial-investment-analysis.git
cd financial-investment-analysis
jupyter notebook notebooks/stock_analysis.ipynb
```

### Core Code Snippet
```python
import yfinance as yf
import pandas as pd
import numpy as np

tickers = ['AAPL', 'MSFT', '^GSPC']
data = yf.download(tickers, start='2023-01-01', end='2025-04-01')['Adj Close']

# Daily returns
returns = data.pct_change().dropna()

# Annual metrics
annual_return = returns.mean() * 252
annual_volatility = returns.std() * np.sqrt(252)

# Beta calculation (AAPL vs S&P 500)
cov_matrix = returns[['AAPL', '^GSPC']].cov()
beta_aapl = cov_matrix.loc['AAPL', '^GSPC'] / cov_matrix.loc['^GSPC', '^GSPC']

print(f"AAPL Beta: {beta_aapl:.4f}")
print(f"Annual Returns:\n{annual_return}")
print(f"Annual Volatility:\n{annual_volatility}")
```

---

## ⚠️ Limitations

- Analysis is bounded to **Jan 2023 – Apr 2025** — findings may not generalize to other market cycles
- **Negative returns** observed during this period likely reflect a specific macroeconomic correction phase, not long-term performance trends
- High correlations (~0.97) suggest this dataset period was **dominated by macro factors**, which may differ from typical conditions
- Beta calculated on daily returns — **intraday or weekly beta** may yield different sensitivity estimates
- Does not account for **dividends** beyond the Adjusted Close price adjustment
- **Currency effects** not considered for international investors

---

## 🌍 Project Impact & Business Implications

| Insight | Strategic Implication |
|---------|----------------------|
| AAPL & MSFT outperform S&P 500 by ~8% despite higher volatility | Justifies overweighting tech in growth-oriented portfolios |
| Beta ≈ 0.93–1.08 | These stocks move nearly 1:1 with the market — not a hedge |
| Correlation > 0.94 between AAPL & MSFT | Holding both provides minimal diversification benefit |
| Q1 2025 sharp decline | Signals need for stop-loss or hedging strategy during macro-uncertainty |
| Volume spikes tied to earnings/events | Event-driven trading strategies can capitalize on predictable volume surges |

---

## 📋 Investment Recommendations

| Strategy | Detail |
|----------|--------|
| **Diversify** | Balance AAPL/MSFT with low-beta assets or bonds to reduce correlated risk |
| **Monitor Events** | Earnings releases, Fed announcements, and product launches trigger high-volume, high-volatility days |
| **Long-Term Focus** | Despite short-term dips, strong fundamentals make both stocks sound long-term holds |
| **Risk Management** | Use stop-loss orders; reassess rolling volatility quarterly |
| **Event-Driven Awareness** | Triple witching days and AI-related announcements have historically triggered AAPL/MSFT volume spikes |

---

## 🔮 Future Enhancements

- Extend analysis to include **FAANG/Magnificent 7** comparison (GOOGL, AMZN, META, NVDA, TSLA)
- Incorporate **Sharpe Ratio** and **Sortino Ratio** for risk-adjusted return comparisons
- Apply **rolling beta** to track sensitivity changes over time
- Build a **Monte Carlo simulation** for portfolio risk forecasting
- Deploy a real-time **Streamlit dashboard** for dynamic ticker analysis

---

## 📚 References

- Yahoo Finance: https://finance.yahoo.com
- yfinance Library: https://pypi.org/project/yfinance/
- Sharpe, W.F. (1964). *Capital Asset Prices: A Theory of Market Equilibrium.*
- Fama, E.F. & French, K.R. (1993). *Common Risk Factors in the Returns on Stocks and Bonds.*
- Investopedia — Beta Definition: https://www.investopedia.com/terms/b/beta.asp

---

## 👤 Author

**[Mahima Srinivasan]**
- 📧 [mahima.s3994@gmail.com]
- 💼 [linkedin.com/in/mahimasrinivasan3994]

> *This project demonstrates end-to-end financial data analysis — from API-based data collection and Python preprocessing through Excel-based financial modeling, statistical analysis, and investment strategy formulation.*

---

*⭐ If you found this project valuable, please consider starring the repository!*
