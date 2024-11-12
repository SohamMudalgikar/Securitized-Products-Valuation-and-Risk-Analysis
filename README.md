# Securitized Products Valuation and Risk Analysis 
---

## Introduction

Mortgage-Backed Securities (MBS) are intricate financial instruments backed by a pool of mortgage loans. The valuation and risk assessment of MBS are pivotal for investors and financial institutions to make informed investment decisions, manage portfolios effectively, and comply with regulatory standards. Traditional valuation methods often fall short in capturing the dynamic nature of factors influencing MBS, such as prepayment rates, interest rate fluctuations, and borrower defaults. This project leverages simulated data and advanced modeling techniques to develop a comprehensive framework for valuing and analyzing the risks associated with MBS.

---

## Problem Statement

Accurate valuation and risk assessment of Mortgage-Backed Securities (MBS) are critical yet challenging due to the complexity of factors involved, including prepayment rates, interest rate changes, and borrower defaults. Traditional deterministic valuation methods may fail to capture these complexities, leading to potential mispricing and underestimation of risks. Additionally, obtaining detailed loan-level data is often difficult, hindering precise analysis. This project aims to address these challenges by simulating realistic loan-level and macroeconomic data and developing a robust valuation and risk analysis framework using advanced techniques like Monte Carlo simulations and Discounted Cash Flow (DCF) analysis.

---

## Objectives

### Primary Objective
- **Develop a simulation-based framework for accurate valuation and risk analysis of Mortgage-Backed Securities (MBS).**

### Secondary Objectives
- **Simulate realistic loan-level and macroeconomic data.**
- **Implement Monte Carlo simulations to model cash flows under various scenarios.**
- **Perform Discounted Cash Flow (DCF) analysis to estimate the present value of MBS.**
- **Conduct comprehensive risk analysis using metrics such as Duration, Convexity, Option-Adjusted Spread (OAS), and Yield Spread.**
- **Validate the simulation framework against known benchmarks or historical data.**

---

## Methodology

The methodology comprises several interconnected steps: data simulation, valuation modeling, risk analysis, and model validation. Each step integrates mathematical models and statistical techniques to ensure comprehensive analysis.

### Data Simulation

Simulating realistic datasets is foundational for the analysis, enabling the modeling of various scenarios and risk factors affecting MBS.

#### Loan-Level Data Simulation

**Variables Simulated:**
- **Original Loan Amount:** Modeled using a log-normal distribution to reflect the variability in loan sizes.
- **Interest Rate on Individual Loans:** Simulated using a normal distribution around a mean market rate.
- **Loan Term and Remaining Term:** Assigned standard terms (e.g., 15 or 30 years) with remaining terms calculated based on loan age.
- **Borrower Credit Score:** Simulated using a normal distribution, affecting default probabilities.
- **Loan-to-Value Ratio (LTV):** Derived from property value and current loan balance.
- **Debt-to-Income Ratio (DTI):** Simulated to assess borrower's ability to service the loan.
- **Geographic Location and Occupancy Type:** Categorized to capture regional risk variations and prepayment behaviors.
- **Prepayment History and Delinquency Status:** Simulated based on borrower characteristics and economic conditions.

**Mathematical Representation:**

- **Log-Normal Distribution for Original Loan Amount:**

 $X \sim LogNormal(\mu, \sigma^2)$

  Where $\mu$ and $\sigma$ are the parameters of the underlying normal distribution.

- **Amortization Schedule for Current Loan Balance:**
  
  $B(t) = P \frac{(1 + r)^n - (1 + r)^t}{(1 + r)^n - 1}$
  
  Where:
  - $B(t)$ = Balance at time $t$
  - $P$ = Original loan amount
  - $r$ = Monthly interest rate
  - $n$ = Total number of payments
  - $t$ = Number of payments made

#### Prepayment and Default Data Simulation

**Prepayment Rate (CPR):**
- Modeled using the Public Securities Association (PSA) prepayment model with added stochastic noise.
  
  \[
  \text{CPR}_t = \text{CPR}_{\text{PSA}}(t) + \epsilon
  \]
  Where $\epsilon$ is a random variable representing noise.

**Default Probability (CDR):**
- Estimated using logistic regression based on borrower attributes and macroeconomic variables.
  
  \[
  \text{CDR} = \frac{1}{1 + e^{-(\beta_0 + \beta_1 \cdot \text{Credit Score} + \beta_2 \cdot \text{DTI} + \beta_3 \cdot \text{Unemployment Rate})}}
  \]

**Severity Rate:**
- Calculated as a function of LTV ratio and economic conditions.
  
  \[
  \text{Severity} = \alpha \cdot \text{LTV} + \gamma \cdot \text{Economic Indicator}
  \]

#### Macroeconomic Data Simulation

**Interest Rates:**
- Simulated using the Vasicek or Cox-Ingersoll-Ross (CIR) models to capture mean-reverting behavior.

  - **Vasicek Model:**
    \[
    dr_t = \kappa (\theta - r_t) dt + \sigma dW_t
    \]
    Where:
    - $\kappa$ = Speed of mean reversion
    - $\theta$ = Long-term mean rate
    - $\sigma$ = Volatility
    - $W_t$ = Wiener process

**Home Price Index (HPI):**
- Modeled using Geometric Brownian Motion (GBM).

  \[
  dS_t = \mu S_t dt + \sigma S_t dW_t
  \]
  Where:
  - $S_t$ = Home price index at time $t$
  - $\mu$ = Expected return
  - $\sigma$ = Volatility

**Unemployment Rates and Other Economic Indicators:**
- Simulated using appropriate stochastic processes or historical data trends to influence prepayment and default behaviors.

### Valuation Models

Valuation models estimate the present value of MBS by projecting future cash flows under various economic scenarios.

#### Monte Carlo Simulations

**Purpose:**
- To model the distribution of possible future cash flows and assess the impact of uncertainty in interest rates, prepayments, and defaults.

**Process:**
1. **Simulate Interest Rate Paths:** Generate multiple interest rate scenarios using the chosen interest rate model (e.g., Vasicek).
2. **Simulate Prepayment and Default Rates:** For each path, simulate prepayment and default rates based on borrower and economic conditions.
3. **Generate Cash Flows:** Calculate expected cash flows from interest payments, principal repayments, prepayments, and defaults.
4. **Discount Cash Flows:** Discount future cash flows to present value using appropriate discount rates.
5. **Aggregate Results:** Compile results across all simulations to derive valuation metrics (e.g., mean, median, confidence intervals).

**Mathematical Representation:**

- **Present Value of Cash Flows:**
  \[
  PV = \sum_{t=1}^{T} \frac{CF_t}{(1 + r_t)^t}
  \]
  Where:
  - $CF_t$ = Cash flow at time $t$
  - $r_t$ = Discount rate at time $t$
  - $T$ = Total number of periods

#### Discounted Cash Flow (DCF) Analysis

**Purpose:**
- To estimate the present value of MBS by discounting expected future cash flows at a risk-adjusted discount rate.

**Process:**
1. **Estimate Future Cash Flows:** Project interest and principal payments based on current loan balances and interest rates.
2. **Determine Discount Rate:** Incorporate risk factors such as prepayment and default risks to adjust the discount rate.
3. **Calculate Present Value:** Discount the projected cash flows to their present value.

**Mathematical Representation:**

\[
DCF = \sum_{t=1}^{T} \frac{CF_t}{(1 + r)^t}
\]

Where:
- $CF_t$ = Cash flow at time $t$
- $r$ = Discount rate
- $T$ = Total number of periods

#### Scenario Testing

**Purpose:**
- To evaluate the impact of different economic conditions on MBS valuation and risk metrics.

**Process:**
1. **Define Scenarios:** Create scenarios such as interest rate shocks, housing market downturns, and economic recessions.
2. **Simulate Cash Flows:** For each scenario, simulate how these conditions affect prepayment rates, default rates, and interest rates.
3. **Assess Impact:** Analyze the resulting cash flows and valuation metrics under each scenario to identify sensitivities and potential vulnerabilities.

### Risk Analysis

Risk analysis quantifies the exposure of MBS to various risk factors, providing insights into potential price fluctuations and returns.

#### Duration and Convexity

**Duration:**
- Measures the sensitivity of the MBS price to changes in interest rates.

  \[
  \text{Duration} = \frac{\sum_{t=1}^{T} t \cdot PV(CF_t)}{\sum_{t=1}^{T} PV(CF_t)}
  \]

**Convexity:**
- Captures the rate of change in duration with respect to interest rate changes, providing a more accurate measure of interest rate risk.

  \[
  \text{Convexity} = \frac{\sum_{t=1}^{T} t(t + 1) \cdot PV(CF_t)}{\sum_{t=1}^{T} PV(CF_t)}
  \]

#### Option-Adjusted Spread (OAS)

**Purpose:**
- To measure the spread over a risk-free rate that compensates for the embedded prepayment option in MBS.

**Calculation:**
- Adjust the yield spread to account for the optionality, typically using models that incorporate prepayment behavior.

  \[
  \text{OAS} = \text{Yield Spread} - \text{Option Cost}
  \]

#### Yield Spread Analysis

**Purpose:**
- To compare the yield of MBS against benchmark yields (e.g., Treasury securities) to assess relative value and attractiveness.

**Calculation:**
  
  \[
  \text{Yield Spread} = \text{MBS Yield} - \text{Benchmark Yield}
  \]

### Model Validation and Calibration

Ensuring the accuracy and reliability of the models through validation and calibration techniques.

#### Backtesting

- To compare simulated outcomes with historical MBS performance data, assessing the model's predictive accuracy.

**Process:**
1. **Historical Data Comparison:** Align simulated results with historical performance metrics.
2. **Error Metrics Calculation:** Use metrics such as Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE) to quantify discrepancies.

  $MAE = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|$

  $RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}$

Where:
- $y_i$ = Actual value
- $\hat{y}_i$ = Predicted value
- $n$ = Number of observations

#### Sensitivity Analysis

**Purpose:**
- To assess how changes in key model parameters affect valuation and risk metrics, ensuring robustness.

**Process:**
1. **Identify Key Parameters:** Such as discount rates, default probabilities, and prepayment rates.
2. **Vary Parameters Systematically:** Adjust parameters within realistic ranges.
3. **Analyze Impact:** Observe changes in valuation and risk metrics to identify sensitivities.

### Mathematical Models and Equations

This section consolidates the key mathematical models and equations used throughout the project.

#### Log-Normal Distribution for Loan Amounts

$X \sim \text{LogNormal}(\mu, \sigma^2)$

#### Amortization Formula for Loan Balance

\[
B(t) = P \frac{(1 + r)^n - (1 + r)^t}{(1 + r)^n - 1}
\]

#### Vasicek Interest Rate Model

\[
dr_t = \kappa (\theta - r_t) dt + \sigma dW_t
\]

#### Geometric Brownian Motion for Home Price Index

\[
dS_t = \mu S_t dt + \sigma S_t dW_t
\]

#### Present Value of Cash Flows

\[
PV = \sum_{t=1}^{T} \frac{CF_t}{(1 + r_t)^t}
\]

#### Duration

\[
\text{Duration} = \frac{\sum_{t=1}^{T} t \cdot PV(CF_t)}{\sum_{t=1}^{T} PV(CF_t)}
\]

#### Convexity

\[
\text{Convexity} = \frac{\sum_{t=1}^{T} t(t + 1) \cdot PV(CF_t)}{\sum_{t=1}^{T} PV(CF_t)}
\]

#### Option-Adjusted Spread (OAS)

\[
\text{OAS} = \text{Yield Spread} - \text{Option Cost}
\]

#### Yield Spread

\[
\text{Yield Spread} = \text{MBS Yield} - \text{Benchmark Yield}
\]



