# Market Stress and Breadth Analysis Tool

## Project Overview
This repository provides a quantitative framework for monitoring market stress through internal breadth indicators. By analyzing the individual components of the S&P 500, the tool identifies periods of systemic panic that may be obscured by the price action of the headline index alone.

The core objective is to measure "Participation in Downside Volatility" using three distinct methodologies to capture different market regimes and volatility environments.

## Technical Methodologies

The tool implements three specific filters to identify "significant daily drops" across the index components:

### 1. Fixed Threshold Method
- **Logic**: Counts stocks recording a daily return of -7.0% or lower.
- **Context**: Represents a "brute force" panic indicator. It is highly effective during high-volatility crashes (e.g., 2008, 2020) but may lack sensitivity in low-volatility bull markets where a -4.0% drop might be equally significant.

### 2. Volatility-Adjusted Method (Standard Deviation)
- **Logic**: Identifies drops exceeding 3x the 20-day rolling standard deviation of each individual stock.
- **Context**: This is a relative measure. It normalizes for the different "personalities" of stocks, treating a sharp move in a stable Utility company with the same significance as a larger move in a volatile Technology stock.

### 3. Absolute Volatility Method (Average True Range)
- **Logic**: Identifies drops where the price decline exceeds 3x the 14-day Average True Range (ATR).
- **Context**: Unlike percentage-based returns, ATR-based signals account for absolute price escursions and overnight gaps, offering a cleaner view of liquidity-driven stress.

## Data Pipeline and Processing
- **Universe**: S&P 500 constituents (dynamically fetched from Wikipedia).
- **Data Source**: Yahoo Finance via the `yfinance` API.
- **Aggregation**: Signals are aggregated using a 5-day rolling window to visualize sustained periods of selling pressure rather than isolated single-day events.
- **Visualization**: Interactive multi-panel charts powered by Plotly, featuring a logarithmic scale for the index to better visualize long-term trends alongside short-term stress spikes.

## Methodological Limitations and Bias
Users should be aware of the **Survivorship Bias** inherent in this analysis. The script currently fetches the *current* constituents of the S&P 500. When backtesting to 2000 or 2008, the analysis only considers companies that have survived and remained in the index until the present day. Delisted or bankrupt companies are not included in the historical count, which may result in an underestimation of historical market stress.

## Requirements
- Python 3.x
- pandas
- numpy
- yfinance
- plotly
- requests

## Usage
The code is provided in a modular block format suitable for Google Colab or Jupyter Notebooks. Ensure all dependencies are installed before execution.
