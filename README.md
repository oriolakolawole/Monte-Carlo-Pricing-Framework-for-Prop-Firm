# Prop Firm Challenges as Options — A Monte Carlo Pricing Framework

A quantitative finance project that models **proprietary trading firm evaluation challenges** as **down-and-out cash-or-nothing call options**, priced via Monte Carlo simulation. Using a strict 0-EV strategy as the underlying process, the analysis derives pass probabilities, expected withdrawal streams, ROI, and break-even conditions — with no trading edge assumed.

---

## Core Idea

A prop firm challenge is structurally equivalent to a **barrier option**:

| Option World | Prop Firm World |
|---|---|
| Option premium | Challenge fee |
| Down-and-out barrier | Max drawdown limit |
| Strike price | Profit target |
| Payoff if ITM | Funded account profit-split stream |
| Implied volatility | Daily P&L standard deviation |

The central question: **is the challenge EV-positive even with zero trading edge?**

> The answer depends entirely on whether the fee is below the actuarially fair break-even this is the same logic as buying a cheap out-of-the-money option.

> [Click Here to view the Project](monte_carlo.ipynb)
---

## Key Results

Using a 1-step $10,000 challenge at a $95 fee with a 0-EV strategy (50% win rate, 1:1 R:R):

| Metric | Value |
|---|---|
| Analytical pass probability (gambler's ruin, no rules) | **50%** |
| Simulated pass probability (with daily DD + discrete sizing) | **~36%** |
| Average days to pass | **~35 trading days** |
| Average funded account withdrawal (12-month horizon) | **~$618** |
| Expected value per attempt | **~+$127** |
| ROI per attempt | **~+139%** |
| Break-even challenge fee | **~$222** |

**The challenge is EV-positive at the $95 fee even with zero trading edge**, driven by 105x capital leverage on the challenge fee.

---

## What's Covered

- **Theoretical framework** — rigorous options analogy with full mathematical derivations.
- **Phase 1 simulation** — 100,000 Monte Carlo paths of the challenge phase (pass rate, days to completion, equity path distributions)
- **Phase 2 simulation** — 50,000 funded account paths modelling the withdrawal stream as a finite-horizon annuity
- **ROI & break-even analysis** — EV per attempt, multi-attempt geometric model, break-even fee
- **Sensitivity analysis** — pass rate and EV heatmaps across win rate × risk-per-trade combinations
- **Options Greeks analogy** — Delta, Gamma, Theta, Vega and Rho mapped to their prop firm equivalents

---

## Parameters (Configurable)

| Parameter | Default | Description |
|---|---|---|
| `ACCOUNT_SIZE` | $10,000 | Simulated capital |
| `CHALLENGE_FEE` | $95 | Upfront cost per attempt |
| `PROFIT_TARGET_PCT` | 10% | Profit target (α) |
| `MAX_TOTAL_DD_PCT` | 10% | Maximum total drawdown (δ) |
| `MAX_DAILY_DD_PCT` | 3% | Maximum daily drawdown |
| `PROFIT_SPLIT` | 90% | Trader's share of funded profits |
| `WIN_PROB` | 50% | 0-EV fair coin strategy |
| `RISK_PER_TRADE_PCT` | 1% | Fractional risk per trade |
| `COMMISSION_PER_TRADE` | $2.50 | Transaction cost |

---

## Installation

```bash
pip install numpy scipy matplotlib tabulate
```

---

## Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```
2. Install dependencies (see above).
3. Open the notebook:
   ```bash
   jupyter notebook monte_carlo.ipynb
   ```
4. Run all cells (`Kernel → Restart & Run All`).

> Simulation sizes are set to 100,000 (Phase 1) and 50,000 (Phase 2) paths. Runtime is typically a few minutes on a standard CPU.

---

## Dependencies

| Package | Purpose |
|---|---|
| `numpy` | Random number generation and vectorised simulation |
| `scipy` | Statistical functions and distributions |
| `matplotlib` | All charting and visualisation |
| `tabulate` | Formatted console output tables |

---

## Repository Structure

```
.
├── monte_carlo.ipynb    # Main analysis notebook
└── README.md            # This file
```

---

## Disclaimer

This project is for **educational and illustrative purposes only**. It does not constitute financial advice. All simulations assume a simplified trading model; real-world prop firm rules vary by provider.

---

## 📚 Background

This project applies financial derivatives theory — specifically **barrier option pricing** and the **gambler's ruin problem** — to evaluate the economic structure of proprietary trading firm challenges.
