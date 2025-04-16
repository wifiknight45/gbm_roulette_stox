# gbm_roulette_stox

Overview

This Python script simulates future stock prices for a predefined list of companies using a Monte Carlo simulation based on the Geometric Brownian Motion (GBM) model*. The script fetches historical stock data, calculates key parameters (mean return and volatility), runs simulations, and generates visualizations and a summary of results.

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

*Geometric Brownian Motion (GBM) is a stochastic process used to model the time evolution of asset prices, such as stocks, in financial mathematics. It assumes that the price of an asset follows a continuous-time random walk where the logarithm of the price changes exhibits a Brownian motion with drift. GBM is widely used in option pricing (e.g., Black-Scholes model) and Monte Carlo simulations for forecasting stock prices due to its ability to capture the random, yet trending, behavior of financial markets.

### Key Components of GBM
GBM describes the price \( S_t \) of an asset at time \( t \) using the following stochastic differential equation (SDE):
\[
dS_t = \mu S_t dt + \sigma S_t dW_t
\]
Where:
- \( S_t \): Asset price at time \( t \).
- \( \mu \): Expected annualized return (drift), representing the average rate of growth of the asset price.
- \( \sigma \): Annualized volatility, measuring the degree of price fluctuation.
- \( dW_t \): Increment of a Wiener process (Brownian motion), representing random shocks (normally distributed with mean 0 and variance \( dt \)).
- \( dt \): Infinitesimal time increment.

The solution to this SDE, assuming an initial price \( S_0 \), is:
\[
S_t = S_0 \exp\left( \left(\mu - \frac{\sigma^2}{2}\right)t + \sigma W_t \right)
\]
Where:
- \( W_t \): Standard Brownian motion at time \( t \).
- \( \mu - \frac{\sigma^2}{2} \): Adjusted drift, accounting for the volatility’s effect on the expected growth rate.
- \( \sigma W_t \): Random component scaled by volatility.

### Properties of GBM
1. **Log-Normal Distribution**: The asset price \( S_t \) follows a log-normal distribution because the logarithm of the price, \( \ln(S_t) \), is normally distributed:
   \[
   \ln(S_t) \sim N\left( \ln(S_0) + \left(\mu - \frac{\sigma^2}{2}\right)t, \sigma^2 t \right)
   \]
   This ensures prices remain positive, unlike regular Brownian motion, which could produce negative values.

2. **Drift**: The term \( \mu \) represents the expected return, driving the long-term trend of the price upward (if \( \mu > 0 \)) or downward.

3. **Volatility**: The term \( \sigma \) governs the magnitude of random fluctuations. Higher volatility leads to wider price dispersion over time.

4. **Random Walk**: The \( dW_t \) term introduces randomness, simulating unpredictable market movements. Each increment is independent and normally distributed.

5. **Continuous Paths**: GBM assumes continuous price paths, though in reality, stock prices move in discrete ticks and may exhibit jumps.

### Discrete-Time Approximation
In Monte Carlo simulations (like the Python script provided), GBM is approximated in discrete time. For a small time step \( \Delta t \), the price at the next time step is:
\[
S_{t+\Delta t} = S_t \exp\left( \left(\mu - \frac{\sigma^2}{2}\right)\Delta t + \sigma \sqrt{\Delta t} Z \right)
\]
Where:
- \( Z \): Random variable from a standard normal distribution (\( N(0,1) \)).
- \( \Delta t \): Time increment (e.g., 1/252 for one trading day in a year).

This formula is used iteratively to generate price paths over multiple time steps.

### Assumptions of GBM
1. **Constant Parameters**: \( \mu \) and \( \sigma \) are assumed constant over time, which may not hold in real markets where volatility and returns vary.
2. **No Jumps**: GBM assumes smooth price changes, ignoring sudden price jumps due to events like earnings reports or market crashes.
3. **Efficient Markets**: Implies that price changes are unpredictable and follow a random walk.
4. **Continuous Trading**: Assumes trading occurs continuously without gaps, which is an idealization.

### Applications in Stock Price Simulation
In the Monte Carlo Stock Generator script:
- **Drift**: Calculated as the historical mean log return minus half the variance (\( \mu - \frac{\sigma^2}{2} \)).
- **Volatility**: Derived from the standard deviation of historical log returns.
- **Randomness**: Simulated using normally distributed random variables to mimic \( W_t \).
- **Price Paths**: Multiple price paths are generated by iterating the discrete GBM formula, producing a distribution of possible future prices.

### Limitations
1. **Non-Stationary Volatility**: Real-world volatility changes over time, unlike the constant \( \sigma \) in GBM.
2. **Fat Tails**: GBM assumes normally distributed returns, but real markets often exhibit extreme events (leptokurtic distributions).
3. **No Mean Reversion**: GBM does not account for mean-reverting behavior seen in some assets.
4. **No Autocorrelation**: Assumes independent price changes, ignoring potential short-term correlations.

### Example
Suppose a stock has:
- Current price \( S_0 = \$100 \).
- Annual drift \( \mu = 0.1 \) (10% expected return).
- Annual volatility \( \sigma = 0.2 \) (20%).
- Time horizon \( t = 1 \) year.

The expected price after one year, using GBM, is:
\[
E[S_t] = S_0 e^{\mu t} = 100 e^{0.1 \cdot 1} \approx \$110.52
\]
However, due to volatility, simulated prices could range widely (e.g., from $80 to $140), as captured by the Monte Carlo simulation’s random paths.

### Conclusion
GBM is a foundational model for simulating stock prices because it balances simplicity with realistic features like positive prices and random fluctuations. Despite its limitations, it’s effective for generating probabilistic forecasts in tools like the Monte Carlo Stock Generator. 