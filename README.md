# K-Means Clustering Momentum Trading Strategy

**[View the strategy results in the Interactive Dashboard](https://sundarramdatla.github.io/K-Means-Clustering-Momentum-Strategy/)**

## 1. Background and Machine Learning Methodology

This project implements a systematic equity trading strategy using **unsupervised machine learning, technical indicators, Fama–French factor models, and mean-variance portfolio optimization** to identify and invest in momentum-driven S&P 500 stocks.

The strategy uses **K-Means clustering**, an unsupervised learning algorithm that groups stocks based on similarities across multiple financial features by minimizing the distance between observations and their assigned cluster centroids.

Each month, the algorithm groups stocks into four clusters initialized at RSI values of 30, 45, 55, and 70. Stocks in **Cluster 3**, associated with stronger historical momentum, are selected for portfolio construction. Portfolio weights are then optimized to maximize the expected Sharpe ratio using historical returns and covariance estimates.

The strategy is backtested against the S&P 500 ETF (SPY).

## 2. Feature Engineering

The strategy uses approximately eight years of historical S&P 500 market data from Yahoo Finance.

**Technical indicators and features:**
- Garman–Klass volatility
- Relative Strength Index (RSI-20)
- Bollinger Bands (20-period)
- Average True Range (ATR-14)
- MACD (12, 26, 9)
- Historical momentum returns (1, 2, 3, 6, 9, and 12 months)
- Rolling five-year average dollar volume for selecting the 150 most liquid stocks
- Rolling 24-month Fama–French five-factor betas (Mkt-RF, SMB, HML, RMW, CMA)

These features capture stock momentum, volatility, liquidity, and systematic market risk exposures.

## 3. Backtesting Performance and Results

The strategy was evaluated over **1,255 trading days from November 2021 to October 2026**, with monthly portfolio rebalancing.

| Performance Metric | K-Means Strategy | SPY Buy & Hold |
|---|---:|---:|
| Cumulative Return | +47.21% | +75.94% |
| Annualized Return | 8.07% | 12.01% |
| Annualized Volatility | 19.30% | 17.16% |
| Sharpe Ratio | 0.50 | 0.75 |
| Maximum Drawdown | −25.92% | −24.50% |

*Sharpe ratios assume a 0% risk-free rate. Returns exclude transaction costs and slippage.*

### Interpretation

K-Means successfully identified groups of equities with distinct momentum characteristics. However, **Cluster 3 exhibited an average historical monthly return of +11.44%, followed by an average next-month return of only +0.35%.**

Conversely, Cluster 0 exhibited an average historical return of −9.84%, followed by a next-month return of +1.87%.

These findings suggest **short-term mean reversion** within the historical sample, potentially explaining why the momentum-based strategy underperformed SPY by 28.73 percentage points.

The results demonstrate that identifying historical momentum through machine learning does not necessarily translate into predictive performance or superior risk-adjusted returns.

## 4. Future Improvements

- **Alternative cluster selection:** Investigate mean-reversion strategies using lower-momentum clusters and test different clustering configurations.
- **Improved portfolio optimization:** Incorporate covariance shrinkage, regularization, and transaction-cost constraints.
- **Market regime detection:** Adapt cluster selection based on market volatility and broader market conditions.
- **Out-of-sample validation:** Implement walk-forward testing and historical index membership to reduce look-ahead and survivorship biases.
- **Advanced machine learning:** Explore Gaussian Mixture Models, hierarchical clustering, and supervised return prediction.

---

**Technologies:** Python, Pandas, NumPy, Scikit-learn, Statsmodels, pandas-ta-classic, PyPortfolioOpt, yfinance, Matplotlib, HTML, CSS, JavaScript.
