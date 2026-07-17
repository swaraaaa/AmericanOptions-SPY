# American Options Pricing & Delta Hedging on SPY

**Derivatives Pricing · LSMC · Binomial Tree · Crank-Nicholson · Greeks · Delta Hedging · Python**

> FE-620 Final Project — MS Financial Engineering, Stevens Institute of Technology (Dec 2024)

> Author: Swara Dave 

---

## 📌 Overview

This project implements and compares three numerical methods for pricing American options on SPY (S&P 500 ETF) across 1-month and 3-month maturities, using real market data from Bloomberg Terminal and Yahoo Finance.

**Three pricing methods implemented:**
1. **Least Squares Monte Carlo (LSMC)** — Longstaff-Schwartz simulation-based approach
2. **Binomial Tree** — Cox-Ross-Rubinstein discrete lattice model
3. **Crank-Nicholson Finite Difference** — PDE-based method with second-order accuracy

---

## 📊 Key Results

### 30-Day Options (Dec 20, 2024 expiry) — as of Nov 20, 2024

| Strike | Actual | LSMC | Binomial Tree | Crank-Nicholson |
|---|---|---|---|---|
| 590 | 10.86 | 10.57 | 10.84 | 10.58 |
| 600 | 5.41 | 6.14 | 6.31 | 6.25 |
| 610 | 2.21 | 3.21 | 3.34 | 3.40 |

### 98-Day Options (Mar 21, 2025 expiry) — as of Dec 13, 2024

| Strike | Actual | LSMC | Binomial Tree | Crank-Nicholson |
|---|---|---|---|---|
| 585 | 33.97 | 31.92 | 33.20 | 33.19 |
| 600 | 22.58 | 22.63 | 23.58 | 23.52 |
| 615 | 13.22 | 15.19 | 15.86 | 15.75 |

**Binomial Tree and Crank-Nicholson** most closely match market prices. LSMC introduces bias from regression approximation but handles high-dimensional problems better.

---

## 🗂️ Data Sources

- **SPY prices** — Yahoo Finance (3-month historical closing prices)
- **Options data** — Bloomberg Terminal (bid/ask for strikes 570–640)
- **Risk-free rate** — 13-week T-bill rate (IRX): **4.23%**
- **Historical volatility** — Estimated at ~13–14% across 1–6 month lookback windows

---

## ⚙️ Methodology

### Pricing Methods

**LSMC (Longstaff-Schwartz Monte Carlo)**
- Simulates GBM price paths; uses least-squares regression to estimate continuation value at each exercise date
- Determines early exercise optimality by comparing continuation value to immediate payoff

**Binomial Tree (Cox-Ross-Rubinstein)**
- Discrete recombining lattice; option value computed backward from expiration
- Early exercise handled explicitly at each node

**Crank-Nicholson Finite Difference**
- Discretizes Black-Scholes PDE using averaged explicit/implicit scheme
- Second-order accuracy; stable and fast convergence for single-asset options

### Greeks Computed
- **Delta** — finite difference approximation: (V(S+h) - V(S-h)) / 2h
- **Gamma** — second derivative: (V(S+h) - 2V(S) + V(S-h)) / h²
- **Vega** — sensitivity to volatility
- **Theta** — sensitivity to time decay

### Delta Hedging
Dynamic delta-neutral hedging implemented for SPY call option (Dec 6–13, 2024):
- Initial delta: 0.7152 → short 71.52 SPY shares
- Daily rebalancing based on spot price changes
- Total hedging cost tracked across 5 trading days

---

## 📁 Repository Structure

```
AmericanOptions-SPY/
├── 1_LSMC_MonteCarlo.ipynb                        # QMC/LSMC pricing implementation
├── 2_Volatility_DeltaHedging.ipynb                # Volatility estimation & delta hedging
└── 3_BinomialTree_CrankNicholson_Greeks.ipynb     # Binomial Tree, CN method & Greeks
```

---

## 🚀 How to Run

1. Clone the repo
2. Install dependencies:
```bash
pip install numpy scipy pandas matplotlib yfinance
```
3. Run notebooks in order:
   - `1_LSMC_MonteCarlo.ipynb` — Monte Carlo pricing
   - `2_Volatility_DeltaHedging.ipynb` — volatility & hedging
   - `3_BinomialTree_CrankNicholson_Greeks.ipynb` — Binomial Tree, Crank-Nicholson & Greeks

> **Note:** SPY historical prices are fetched automatically via `yfinance`. Options market data (bid/ask for strikes 570–640) was sourced from Bloomberg Terminal as of Nov 20, 2024 and Dec 13, 2024. If you don't have Bloomberg access, substitute with options data from Yahoo Finance (`yfinance` options chain) or CBOE for similar strike ranges.

---

## 👤 Author

**Swara Dave** — MS Financial Engineering, Stevens Institute of Technology
[![LinkedIn](https://img.shields.io/badge/LinkedIn-swara--dave-blue?style=flat&logo=linkedin)](https://linkedin.com/in/swara-dave) [![GitHub](https://img.shields.io/badge/GitHub-swaraaaa-black?style=flat&logo=github)](https://github.com/swaraaaa)
