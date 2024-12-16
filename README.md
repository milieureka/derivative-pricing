# 1. Option Pricing comparison between Black-Scholes and Tree Models

## Overview

For further details, refer to the [code1](https://github.com/milieureka/derivative-pricing/blob/main/Derivative_Pricing_binomial_trinomial_tree.ipynb) and [code2](https://github.com/milieureka/derivative-pricing/blob/main/Derivative_Pricing_Black_Scholes.ipynb) and [report](https://github.com/milieureka/derivative-pricing/blob/main/Pricing%20Option%20with%20Tree%20Model%20and%20Black-Scholes.pdf) provided in the repository.

This project explores the pricing of financial options using various methodologies, including the Black-Scholes model, binomial/trinomial tree methods, and Monte Carlo simulations. It also analyzes exotic options like barrier options and validates financial relationships such as put-call parity.

## Objectives
1. Compare the performance of Black-Scholes, binomial/trinomial tree, and Monte Carlo models.
2. Analyze the pricing and sensitivities (Greeks) for European, American, and exotic barrier options.
3. Validate theoretical concepts like put-call parity and explore the effect of moneyness on option prices.

## Models Used
- **Black-Scholes Model**:
  - Provides a closed-form solution for European option pricing.
  - Formula for a European call option:
    
    $$C = S_0 N(d_1) - K e^{-rT} N(d_2)$$
    
    $$d_1 = \frac{\ln(S_0 / K) + (r + \sigma^2 / 2)T}{\sigma \sqrt{T}}$$
    
    $$d_2 = d_1 - \sigma \sqrt{T}$$
    
  - For a European put option, the formula is:
    
    $$P = K e^{-rT} N(-d_2) - S_0 N(-d_1)$$

- **Binomial and Trinomial Tree Models**:
  - Approximates option prices by modeling the price movements of the underlying asset as an up-and-down tree.
  - Steps: Create a tree structure, calculate payoffs at maturity, and discount backwards through the tree.

- **Monte Carlo Simulations**:
  - Simulates multiple paths of the underlying asset price using Geometric Brownian Motion (GBM):

    $$S_t = S_0 e^{(r - \sigma^2 / 2)t + \sigma W_t}$$

    Where:
    
    - $$S_t $$: Asset price at time $$t$$
      
    - $$r$$: Risk-free rate
      
    - $$\sigma$$: Volatility
      
    - $$W_t$$: Wiener process (random walk)

## Key Findings

### 1. Comparison of Black-Scholes and Tree Models
- For European ATM options, Black-Scholes and binomial tree models produced identical results:
  - Call Price: $$4.61$$
  - Put Price: $$3.37$$
- Both models confirmed put-call parity:
  $$C - P = S_0 - K e^{-rT}$$
  
  Example:
  
  $$4.61 - 3.37 = 100 - 100 \cdot e^{-0.05 \cdot 0.25} \approx 1.24$$

### 2. Monte Carlo Simulations
- Monte Carlo results converged to Black-Scholes outcomes as the number of simulations increased.
- Deviations (e.g., up to 10% for ATM put prices) were attributed to simulation variability.

### 3. Barrier Options (Exotic)
- Up-and-Out (UAO) and Up-and-In (UAI) options were priced using Monte Carlo simulations:
  - Vanilla option price: $$13.81$$
  - UAI option price: $$13.13$$
  - UAO option price: $$0.68$$
- Theoretical relationship validated:
  
  $$\text{UAI Price} + \text{UAO Price} \approx \text{Vanilla Price}$$

### 4. Moneyness Analysis

- Call prices decreased with higher moneyness (higher strike price):
  $$\text{Call Price: 90\% moneyness = 11.50, 110\% moneyness = 1.11}$$
- Put prices increased with higher moneyness:
  $$\text{Put Price: 90\% moneyness = 0.50, 110\% moneyness = 10.29}$$

## Conclusion
- Black-Scholes and tree models are consistent for basic European options.
- Monte Carlo simulations are effective for complex options (e.g., American and barrier options) but require computational resources.
- Exotic option pricing validates theoretical relationships, and moneyness impacts pricing as expected.

# 2. Option Pricing Analysis with Heston and Merton Models

## Overview

For further details, refer to the [code](https://github.com/milieureka/derivative-pricing/blob/main/Volatility_and_Jump_Diffusion_Models.ipynb) and [report](https://github.com/milieureka/derivative-pricing/blob/main/Pricing%20Options%20with%20Local%20Volatility-%20Stochastic%20Volatility-Jump%20Diffusion%20Models.pdf) provided in the repository.

This project focuses on analyzing financial derivatives, specifically European and American options, under advanced pricing models. The primary goal is to evaluate the impact of stochastic volatility and market jumps on option prices, validate key financial relationships like put-call parity, and assess risk metrics through Greeks.

## Requirements
The study aims to:
1. Price European and American options under realistic market conditions.
2. Analyze barrier options, such as up-and-in calls and down-and-in puts.
3. Validate financial principles like put-call parity.
4. Examine the effect of moneyness and model parameters (volatility, jumps, correlations) on option prices.

## Why Use These Models?
- **Heston Model**: Captures stochastic volatility, enabling a realistic representation of volatility clustering and skewed returns often observed in markets.
- **Merton Jump-Diffusion Model**: Accounts for discrete jumps in asset prices, providing a robust framework for pricing options in markets with shocks or significant events.

These models go beyond traditional approaches, like the Black-Scholes model, by addressing real-world complexities in financial markets.

## Key Mathematical Formulas

### Heston Model Volatility Dynamics
$$dv_t = \kappa(\theta - v_t)dt + \sigma \sqrt{v_t} dW_t$$

Where:
- $$v_t$$: Stochastic variance at time $$t$$
- $$\kappa$$: Rate of mean reversion
- $$\theta$$: Long-term variance
- $$\sigma$$: Volatility of variance
- $$dW_t$$: Wiener process

### Merton Model Stock Price Dynamics
$$ dS_t = S_t (\mu dt + \sigma dW_t) + J_t $$

Where:
- $$S_t$$: Stock price at time $$t$$
- $$\mu$$: Drift term
- $$\sigma$$: Volatility term
- $$J_t$$: Jump component modeled by a Poisson process

### European Option Price (General)
$$ C = e^{-rT} \mathbb{E}[\max(S_T - K, 0)] $$

Where:
- $$r$$: Risk-free rate
- $$T$$: Time to maturity
- $$S_T$$: Stock price at maturity
- $$K$$: Strike price

### Greeks
#### Delta

$$ \Delta = \frac{\partial C}{\partial S} $$

#### Gamma

$$ \Gamma = \frac{\partial^2 C}{\partial S^2} $$

## What Was Done
1. **Model Setup**: Defined key parameters, such as initial stock price, volatility, jump intensities, and correlations.
2. **Monte Carlo Simulations**: Simulated stock price paths for both models:
   - Used Cholesky decomposition for correlated processes in the Heston model.
   - Incorporated Poisson jumps in the Merton model.
3. **Option Pricing**:
   - Calculated European and American option prices.
   - Analyzed barrier options (up-and-in calls, down-and-in puts).
4. **Greeks Calculation**: Derived sensitivities (delta and gamma) to assess risk metrics.
5. **Validation**: Verified put-call parity and consistency of pricing across different parameter values.

## Results
- **Heston Model**:
  - Correlations (-0.30 and -0.70) had minimal impact on European call and put prices.
  - Barrier options (e.g., up-and-in calls) showed sensitivity to barrier levels (e.g., $0.26 for a $95 barrier).
  - Put-call parity discrepancies were negligible.

- **Merton Model**:
  - Higher jump intensities ($$\lambda = 0.75$$) increased option premiums compared to lower intensities ($$\lambda = 0.25$$).
  - American options were more valuable due to early exercise flexibility (e.g., $14.40 for American call vs. $15.12 for European call).
  - Put-call parity held within acceptable thresholds.

- **Comparison Across Models**:
  - Moneyness influenced premiums differently. The Heston model typically produced lower premiums for deep in-the-money or out-of-the-money options compared to the Merton model.


---

### How to Use
1. Clone the repository.
2. Install dependencies (if applicable).
3. Run the included scripts for replicating the analysis.

For further details, refer to the respective sections of the project documentation.
