# Modeling the Stock Market Using the Ising Model

This notebook models the stock market using the Ising model, inspired by the paper ["The stock market learned as Ising model"](https://iopscience.iop.org/article/10.1088/1742-6596/1113/1/012009) by L. Zhao, W. Bao, and W. Li.

## Overview

We analyze financial data from three major stock indices:

- **S&P 500** (US)
- **FTSE 250** (UK)
- **SSE 380** (China)

The notebook performs the following key steps:

1. **Data Acquisition**:
   - Fetch stock tickers for each index.
   - Download adjusted closing prices from Yahoo Finance using `yfinance`.
   - For SSE 380, scrape tickers from the Shanghai Stock Exchange website using Selenium.

2. **Data Preprocessing**:
   - Compute logarithmic returns of stock prices.
   - Binarize returns into spin states (\( s_i = \pm 1 \)) to represent positive or negative returns.
   - Filter out stocks with insufficient data points.
   - Align datasets by common dates and truncate to equal lengths.

3. **Correlation Analysis**:
   - Compute and visualize the correlation matrix of stock returns.
   - Analyze the mean, median, and mode of off-diagonal correlation coefficients.

4. **Ising Model Implementation**:
   - **Naive Mean Field (nMF) Approximation**:
     - Compute mean magnetizations and covariance matrix.
     - Estimate coupling strengths \( J_{ij}^{\text{nMF}} \) and external fields \( h_i^{\text{nMF}} \).
   - **Thouless-Anderson-Palmer (TAP) Approximation**:
     - Include higher-order corrections for coupling strengths \( J_{ij}^{\text{TAP}} \) and external fields \( h_i^{\text{TAP}} \).

5. **Statistical Analysis**:
   - Calculate statistical moments (mean, variance, skewness, kurtosis) of coupling strengths.
   - Filter out extreme coupling values by removing the top and bottom 5% to reduce the impact of outliers.
   - Shuffle data to remove correlations and recompute coupling strengths for significance testing.

6. **Visualization**:
   - Plot histograms of coupling strength distributions for both original and shuffled data.
   - Visualize external field distributions to understand individual stock tendencies.
   - Generate heatmaps of the coupling matrices to identify interaction patterns between stocks.

## How to Use This Notebook

1. **Install Required Packages**:
   ```python
   !pip install yfinance seaborn
   ```

2. **Import Libraries**:
   - Ensure all necessary libraries are imported, including `numpy`, `pandas`, `yfinance`, `seaborn`, `matplotlib`, and `scipy`.

3. **Data Acquisition**:
   - Run the provided functions to fetch and load stock data for S&P 500, FTSE 250, and SSE 380.
   - Save the datasets to CSV files for future use.

4. **Data Preprocessing**:
   - Compute logarithmic returns and binarize them into spin states.
   - Filter stocks with sufficient data and align datasets across all markets.

5. **Correlation Analysis**:
   - Compute the correlation matrix and visualize it using a heatmap.

6. **Ising Model Computation**:
   - Use the provided functions to compute coupling strengths and external fields using both nMF and TAP approximations.
   - Apply regularization to covariance matrices to ensure numerical stability.

7. **Statistical Analysis and Filtering**:
   - Filter out extreme coupling strengths by removing the top and bottom 5% of values.
   - Shuffle the data and repeat the analysis for comparison.

8. **Visualization**:
   - Plot coupling strength distributions and external field distributions.
   - Visualize coupling matrices using heatmaps with stock tickers as axis labels.

9. **Interpretation**:
   - Analyze the results to understand the interactions and tendencies within each stock market.
   - Compare the original and shuffled data to assess the significance of the inferred interactions.

## Dependencies

- Python 3.x
- Packages:
  - `numpy`
  - `pandas`
  - `yfinance`
  - `seaborn`
  - `matplotlib`
  - `scipy`
  - `selenium` (for web scraping SSE 380 tickers)
  - `webdriver-manager` (optional, for Selenium)

## Notes

- **Data Fetching**: Fetching data from Yahoo Finance and scraping websites may take time and requires an active internet connection.
- **Selenium Setup**: Scraping SSE 380 tickers with Selenium may require additional setup, such as installing ChromeDriver.
- **Data Files**: Datasets are saved as CSV files for convenience.
- **Execution Order**: Run the notebook cells sequentially to avoid errors.
- **Visualization**: Adjustments may be needed for visualization parameters based on the data and display preferences.