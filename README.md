# gbm_roulette_stox

Overview

This Python script simulates future stock prices for a predefined list of companies using a Monte Carlo simulation based on the Geometric Brownian Motion (GBM) model. The script fetches historical stock data, calculates key parameters (mean return and volatility), runs simulations, and generates visualizations and a summary of results.

Stocks Included

The script tracks the following stocks:
Apple (AAPL)
Alphabet (GOOGL)
Wells Fargo (WFC)
TaskUs (TASK)
Coca Cola (KO)
Boeing (BA)
Lockheed Martin (LMT)
Starbucks (SBUX)
Nvidia (NVDA)
Raytheon Technologies (RTX)
Accenture (ACN)
Samsung (SSNLF, OTC ticker, may have limited data)
Verizon (VZ)
Dexter (DXTR)
AT&T (T)

Features
Fetches historical stock data using the yfinance library.
Calculates annualized mean return and volatility from historical data.
Simulates 1000 price paths over 252 trading days (1 year) using GBM.
Generates plots of simulated price paths for each stock.
Saves a summary of results (last price, mean return, volatility, and mean final price) to a CSV file.
Includes robust error handling and logging for debugging.

Prerequisites
Python 3.6 or higher

Required Python libraries:
yfinance
numpy
pandas
matplotlib

Installation
Clone or Download the Script:
Ensure the insertscriptnamehere.py script is in your working directory.

Install Dependencies: Run the following command to install the required libraries:
pip install yfinance numpy pandas matplotlib

Verify Ticker Availability:
Some tickers (e.g., SSNLF for Samsung, DXTR for Dexter) may have limited or no data due to OTC trading or incorrect ticker symbols. Verify and replace these tickers if needed.

Usage
Run the Script: Execute the script in your Python environment:

Output
Plots: For each stock, a plot of the 1000 simulated price paths is saved as <ticker>_monte_carlo.png in the working directory.

Summary: A CSV file named stock_simulation_summary.csv is generated, containing:
Ticker symbol
Last closing price
Annualized mean return
Annualized volatility
Mean final price from simulations

Customization:
Modify the tickers list in the script to include different stocks.

Adjust NUM_SIMULATIONS (default: 1000) or NUM_DAYS (default: 252) for different simulation parameters.

Change RISK_FREE_RATE (default: 0.02) to reflect the current risk-free rate.

Notes:
Data Availability: Some tickers (e.g., SSNLF, DXTR) may not return data due to limited trading or incorrect ticker symbols. Check logs for warnings and verify tickers.

Performance: The script is optimized for the listed stocks but can be extended for more tickers. For large ticker lists, consider parallel processing.

Model Assumptions: The GBM model assumes constant volatility and log-normal price movements, which may not fully capture real-world market dynamics.

Logging: The script logs progress and errors to the console for debugging. Check logs for issues with data retrieval or processing.

Example Output

Sample Plot

For AAPL, a file named AAPL_monte_carlo.png will show 1000 simulated price paths over 252 days.

Sample Summary (stock_simulation_summary.csv)

Ticker,Last_Price,Mean_Return,Volatility,Final_Mean_Price
AAPL,175.23,0.15,0.25,185.67
GOOGL,142.56,0.12,0.30,150.89
...

Troubleshooting
No Data for Ticker: If a ticker returns no data, check the ticker symbol and ensure it is valid on Yahoo Finance. Replace or remove problematic tickers.
Library Errors: Ensure all dependencies are installed correctly. Re-run the pip install command if issues persist.
Plotting Issues: Ensure matplotlib is installed and your environment supports plotting. Check the working directory for saved PNG files.

acknowledgements: xAI, Grok 3, Google Colab, Microsoft Copilot and fresh tunes by wifiknight45
