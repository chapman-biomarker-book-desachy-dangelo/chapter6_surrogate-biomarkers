
# Chapter 6: Statistical Evaluation of Biomarkers as Surrogate Endpoints

This repository contains R code for simulating and evaluating trial level surrogacy between HbA1c (surrogate endpoint), and mortality (true clinical endpoint).
We quantify how the correlation between treatment effects on these endpoints varies under different trial design characteristics, as well as under different survival distributions and alternative measures for treatment effect on mortality.

## Folder Instruction
- **code**: Rmarkdown file for the simulated evaluations

## Overview
The code evaluates trial-level surrogacy by:

1. Generating surrogate (HbA1c) and mortality treatment effects for multiple trials under pre-specified data generating mechanisms.
2. Simulating time to event outcomes under different follow up durations.
3. Estimating trial specific log hazard ratios for mortality using Cox proportional hazards models.
4. Quantifying surrogacy using inverse variance–weighted Pearson correlations with bootstrap confidence intervals.

The findings of these simulations can be used to assess the ability to meet established surrogacy criteria such as IQWiG’s requirement for a lower 95% CI bound of the correlation ≥ 0.85.

## Simulation description

### **Base-case setup**
- 19 RCTs, each with 7,226 participants (1:1 randomization).
- True treatment effects on the surrogate (δᵢ, mean difference in HbA1c) sampled from: δᵢ ~ Normal(-0.43, SD=0.17)

- True treatment effects on mortality (θᵢ) follow: θᵢ = α + β * δᵢ, α = 0 β = 0.52

- Survival times generated using:
- Comparator arm survival curves scaled to match various 1 year mortality risks.
- Treatment arm survival derived under proportional hazards: HR = exp(θᵢ).
- Administrative censoring at the follow-up duration of the trial.

- 1,000 datasets simulated per scenario (seed = 107).  
- Time-to-death analyzed using Cox PH models within each trial:
- Trial-level surrogate validation quantified by Pearson correlation between mean difference in HbA1c and estimated log HRs.
- Inverse variance weighting applied.
- Bootstrapped 95% CIs computed.

##  Simualted scenarios

The following elements are varied one at a time from the base case:

###  **Trial design parameters**
- Follow up duration: 1–10 years
- Number of trials
- Sample size per trial
- Variability of treatment effects on HbA1c
- Strength of relationship between treatment effects on HbA1c and mortality (β)
- Comparator group one year survival probabilities

### **Survival distributions**
- Weibull  
- Log-normal  
- Log-logistic  

###  **Alternative mortality effect measures**
(Scenarios without censoring)
- Relative risk  
- Risk difference  

###  **Additional restrictions**
- Minimum number of events per trial (≥ 20 deaths)
- Controlling the extent to which the true HR for mortality is explained by the effect on HbA1c (R² = 0.90, R² = 0.80)

## Outputs

For each simulated scenario, the code generates:
- Mean correlation between HbA1c effect and log‑HR across 1000 iterations
- Mean bootstrap lower/upper bounds (2.5th and 97.5th percentiles)
-  Plots summarizing correlation (mean, lower bound, upper bound across iterations) vs. follow up duration under the various simulation scenarios.

These outputs help to evaluate whether trial-level surrogacy criteria, such as the IQWiG threshold (lower CI ≥ 0.85), can be realistically be met.

