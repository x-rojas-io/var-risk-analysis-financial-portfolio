# 📘 Value at Risk (VaR) Analysis for a Canadian Financial Portfolio

## 📌 Overview
This project is a case study analyzing **Value at Risk (VaR)** for a portfolio of Canadian equities.  
It explores multiple VaR methodologies and introduces bootstrap confidence intervals to evaluate the reliability of risk estimates.  

The work demonstrates how **data science and machine learning techniques** can be applied in **financial risk management**.

---

## 🎯 Objectives
- Estimate **1-day and 10-day VaR** at **95% and 99% confidence levels**.  
- Compare **Historical Simulation, Parametric (Delta-Normal), and Monte Carlo** VaR approaches.  
- Construct **bootstrap confidence intervals** for VaR.  
- Assess model quality via **coverage percentage**.  
- Visualize portfolio risk exposure and backtest results.  

---

## 🧠 Theoretical Background

### What is VaR?
Value at Risk (VaR) measures the maximum expected portfolio loss over a specified horizon at a given confidence level.  

`VaRα(X) = inf { x ∈ R : P(X ≤ x) ≥ α }`

Example: A 1-day 99% VaR of **-$2M** means there is only a **1% chance** the portfolio loses more than $2M in a single day.  

---

### Methods Used
1. **Historical Simulation**  
   - Empirical, uses actual past returns.  
   - Captures fat tails & skewness.  

2. **Parametric (Delta-Normal)**  
   - Assumes normally distributed returns.  
   - Simple and widely used in banking.  
   - Tends to underestimate tail risks.  

3. **Monte Carlo Simulation**  
   - Simulates thousands of price paths (e.g., via Geometric Brownian Motion).  
   - Flexible but computationally heavy.  

---

### Bootstrap Confidence Intervals
- Motivation: VaR is sample-dependent. How *reliable* is the estimate?  
- Method: Resample historical returns with replacement to generate many VaR estimates.  
- Output: A confidence interval around VaR (e.g., 95% CI).  
- Evaluation: **Coverage percentage** = fraction of observed losses that fall within the estimated interval.  

---

## 📊 Dataset
- **Tickers:**  
  - RY.TO – Royal Bank of Canada (Financial)  
  - ENB.TO – Enbridge (Energy)  
  - BNS.TO – Bank of Nova Scotia (Financial)  
  - CP.TO – Canadian Pacific Kansas City (Industrials)  
  - BCE.TO – BCE Inc. (Telecom)  

- **Source:** Yahoo Finance (`yfinance`)  
- **Frequency:** Daily prices  
- **Period:** 2010–2025 (~15 years)  
- **Returns:** Log returns, `r_t = ln(P_t / P_{t-1})`  

---

## ⚙️ Methodology
1. Download adjusted closing prices.  
2. Compute daily log returns.  
3. Aggregate into portfolio returns (equal-weighted).  
4. Estimate VaR at multiple horizons and confidence levels using:  
   - Historical, Parametric, Monte Carlo.  
5. Apply **bootstrap (1,000 resamples)** to compute VaR confidence intervals.  
6. Evaluate model quality via **coverage percentage** and backtesting.  

---

## 📈 Results (Illustrative)
| Method        | 1-Day 95% | 1-Day 99% | 10-Day 95% | 10-Day 99% |
|---------------|-----------|-----------|------------|------------|
| Historical    | -18,500   | -28,200   | -58,400    | -91,200    |
| Parametric    | -16,800   | -25,100   | -55,200    | -82,700    |
| Monte Carlo   | -19,100   | -29,500   | -61,000    | -95,400    |

➡️ Historical captures fat tails, Parametric underestimates, Monte Carlo flexible but model-sensitive.  
➡️ Bootstrap reveals uncertainty bands around estimates.  

---

## 📊 Visualizations
- Distribution of portfolio returns.  
- VaR comparison across methods.  
- Rolling VaR estimates over time.  
- Bootstrap confidence intervals.  
- Backtesting exceptions vs expected exceedances.  

---

## 📌 Discussion
- **Historical Simulation** is more realistic for financial returns (fat tails).  
- **Parametric VaR** is quick but can be misleading.  
- **Monte Carlo** allows more advanced modeling but requires assumptions (e.g., volatility process).  
- **Bootstrap** improves interpretability by quantifying estimation uncertainty.  

---

## ✅ Conclusion
- VaR is useful but incomplete (does not capture magnitude of extreme losses).  
- For Canadian markets, Historical + Bootstrap provides a robust balance of **realism and statistical rigor**.  
- Future work: Expected Shortfall (ES), GARCH modeling, and stress testing.  

---

## 📚 References
- Jorion, P. *Value at Risk: The New Benchmark for Managing Financial Risk*.  
- Basel Committee on Banking Supervision (2016). *Minimum capital requirements for market risk*.  
- Efron, B. & Tibshirani, R. *An Introduction to the Bootstrap*.  

---

## 🚀 How to Run
```bash
# Clone repo
git clone https://github.com/x-rojas-io/var-risk-analysis-financial-portfolio.git
cd var-risk-analysis-financial-portfolio

# Create environment
python -m venv .venv
source .venv/bin/activate  # macOS/Linux
.venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook