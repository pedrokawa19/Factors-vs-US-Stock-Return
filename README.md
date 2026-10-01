# Momentum, Volatility, and Volume Factors in U.S. Stock Returns

**ISYE 4031 Final Project**  
*Industrial & Systems Engineering, Georgia Tech*

## Project Overview

This project analyzes the relationship between momentum, volatility, and volume factors in U.S. stock returns using S&P 500 data. We investigate how these three key market indicators influence stock performance and develop predictive models for return forecasting.

## Research Questions

- Do momentum indicators significantly predict future stock returns?
- How does volatility affect return predictability?
- Is trading volume a useful indicator of price direction?

## Methodology

### Data Collection
- **Universe**: A sample of the largest S&P 500 companies; 48 stocks were available in the saved weekly regression output
- **Source**: Yahoo Finance, using `yfinance`
- **Time Period**: January 2021 through December 2024
- **Frequency**: Daily prices and volume resampled to weekly observations

### Analysis Framework
1. **Data Preparation**: Resample daily prices and volume to weekly data
2. **Feature Engineering**: Calculate weekly log open-to-close returns and lagged ROC, BBW, and RVOL indicators
3. **Cross-Sectional Regression**: Fit a separate regression across available stocks for each week
4. **Factor-Series Analysis**: Examine the resulting weekly regression coefficients with ARIMA and simple exponential smoothing

## Results

The saved notebook output contains 209 weekly cross-sectional regressions. Across those weeks:

- The mean $R^2$ was **0.177**.
- **ROC** was statistically significant at the 5% level in **24.40%** of weeks; its average coefficient was **-0.0083**.
- **RVOL** was significant in **14.83%** of weeks; its average coefficient was **-0.2586**.
- **BBW** was significant in **37.32%** of weeks; its average coefficient was **0.0091**.
- The coefficient series' best AIC-selected models were **ARIMA(0,0,0)** for all three factors, indicating little evidence in this specification that their coefficients are linearly predictable from their own past values.
- Simple exponential smoothing produced test-set MAPE values above **100%** for all three coefficient series (ROC **132.97%**, RVOL **203.92%**, BBW **109.91%**), so these forecasts were not accurate in percentage-error terms.

Overall, the results show some week-specific associations, particularly for BBW, but do not establish reliable out-of-sample return predictability. These are exploratory findings from the current notebook analysis, not investment recommendations.

### Interpretation Notes

- The regressions are cross-sectional by week, with stocks as observations; the average coefficients summarize these weekly fits. They are not one pooled model of all stock-week observations.
- The notebook uses a **five-week ROC**, **seven-week Bollinger Band width window**, and **ten-week volume moving average**, with indicators lagged one week. These are weekly windows, despite older comments in the notebook referring to day-based windows.
- The displayed VIF diagnostic is for one week only: ROC **3.93**, RVOL **4.57**, and BBW **9.73**. BBW is near the conventional threshold of 10, so multicollinearity should not be dismissed based on that one diagnostic.
- The reported Durbin-Watson summaries calculate residuals across stocks within each week's cross-section. Since the observations are not ordered in time, those values do not establish temporal autocorrelation in model errors.
- MAPE can be misleading for coefficients close to zero; the large reported errors should be read alongside absolute or squared error metrics.

## Technical Stack

- **Python 3.x**
- **Data Processing**: pandas, numpy
- **Financial Data**: yfinance, pandas-datareader
- **Analysis**: scikit-learn, statsmodels
- **Visualization**: matplotlib, seaborn, plotly
- **Web Scraping**: BeautifulSoup, requests


## Team Collaboration

This project uses Git for version control and supports collaboration between team members using:
- **GitHub**: Central repository for code sharing
- **VS Code**: Local development environment

## Key References

- Fama-French factor models
- Momentum strategies in equity markets
- GARCH volatility modeling
- Volume-price relationship studies
- Risk-return analysis in financial markets

---

**Note**: This is an academic project for ISYE 4031 at Georgia Institute of Technology. All analysis is for educational purposes only and should not be considered as investment advice.
