# Application of Monte Carlo Simulation in Financial Forecasting

## Overview

Business management typically forecasts future performance using three deterministic scenarios — best, normal, and worst case — by varying assumptions in a financial model. While useful, this approach has a fundamental limitation: no probability is assigned to each scenario, leaving management with no insight into how likely each outcome actually is.

This project demonstrates how **Monte Carlo Simulation** addresses this by generating thousands of simulations from stochastic models, producing a full probability distribution of outcomes. Instead of three point estimates, management can make statements like: "There is a 90% probability that profit will fall between X and Y."

## Methodology

### Random Walk

The simplest stochastic process, serving as the foundation for more advanced models. At each time step, the value changes by a random shock drawn from a normal distribution:

$$S_t = S_{t-1} + \sigma Z_t + \mu$$

where $\mu$ is the drift (expected change per step) and $\sigma Z_t$ is a random normal shock.

### Geometric Brownian Motion (GBM)

GBM is the standard model for financial asset prices and is used throughout this project to model revenue and cost dynamics. It is described by the stochastic differential equation:

$$dS_t = \mu S_t \, dt + \sigma S_t \, dW_t$$

where:

- $\mu$ = drift rate (expected growth)
- $\sigma$ = volatility
- $W_t$ = Wiener process (Brownian motion)

Because analytical solutions to SDEs are not always available, the notebook implements three discretization methods:

| Method | Notes |
| --- | --- |
| **Closed-Form** | $S_{t+\Delta t} = S_t \exp\!\left[(\mu - \frac{\sigma^2}{2})\Delta t + \sigma Z_t \sqrt{\Delta t}\right]$ — most accurate |
| **Euler-Maruyama** | $S_{t+\Delta t} = S_t \left[1 + \mu \Delta t + \sigma Z_t \sqrt{\Delta t}\right]$ — first-order approximation |
| **Milstein** | $S_{t+\Delta t} = S_t \left[1 + \mu \Delta t + \sigma Z_t \sqrt{\Delta t} + \tfrac{1}{2}\sigma^2(Z_t^2 - 1)\Delta t\right]$ — higher-order accuracy |

### Financial Forecasting Application

GBM is applied to two practical business forecasting scenarios:

#### 1. Stochastic Revenue Model

- Revenue follows a GBM process with defined drift and volatility
- Profit = Revenue − Fixed Cost − Variable Cost (as a % of revenue)
- 10,000 simulations produce a distribution of profit trajectories over a 12-month horizon

#### 2. Stochastic Cost Model with Demand Elasticity

- Raw material (variable) cost follows a GBM process
- Price is set as a markup on cost: Price = Markup × Cost
- Demand responds to price via an elasticity curve: Quantity = a − b × Price
- Profit = (Quantity × Price) − Fixed Cost − (Quantity × Cost)
- Captures the interaction between cost volatility, pricing strategy, and demand response

## Notebook Contents

The Jupyter notebook is structured progressively across three sections:

| Section | Description |
| --- | --- |
| **1. Random Walk** | Builds intuition for stochastic processes; introduces drift, volatility, and random shocks |
| **2. Geometric Brownian Motion** | Implements and compares Closed-Form, Euler-Maruyama, and Milstein discretization methods |
| **3. Financial Forecasting** | Applies GBM to business scenarios — stochastic revenue model and stochastic cost model with demand elasticity |

## Results

Running 10,000 simulations produces:

- **Fan charts** showing the expanding cone of uncertainty over the forecast horizon
- **5th and 95th percentile bands** defining a 90% confidence interval for profit
- **Downside risk quantification** — the probability that profit falls below any given threshold
- **Full terminal value distribution**, enabling probabilistic statements about business outcomes

![random_walk](https://github.com/tonytsoi/montecarlo_forecast/blob/main/assets/random_walk.png?raw=true)

## Getting Started

**Prerequisites:**

- Python 3.x
- `numpy`
- `pandas`
- `matplotlib`

**Run the notebook:**

```bash
jupyter notebook "Monte Carlo - Financial Forecasting.ipynb"
```

## Reference

For a full discussion of the methodology, read the accompanying article on Medium:

[Application of Monte Carlo Simulation in Financial Forecasting](https://medium.com/@tsoiyingkit/application-of-monte-carlo-simulation-in-financial-forecasting-1ddb231080f9)
