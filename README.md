# M/G/1 to M/M/1 Envelope Approximation

This repository contains an R Markdown document explores the approximation of queuing delays in an M/G/1 (Markovian arrival process, General service time distribution, single server) queuing system using an M/M/1 (Markovian arrival process, Exponential service time distribution, single server) envelope. The M/G/1 model is more general but can be challenging to analyze, especially with complex service time distributions. The M/M/1 model, while simpler, can provide an upper bound on the queuing delays experienced in the M/G/1 system.

## Table of Contents

- [Overview](#overview)
- [Installation and Usage](#usage)
- [Input Data](#inputdata)
- [Results](#results)
- [Polynomial Regression Model](#PolynomialR)

## Overview

The M/G/1 queuing model is more general and can accommodate various service time distributions, including non-exponential distributions. However, analyzing and obtaining closed-form solutions for the M/G/1 model can be challenging, especially when the service time distribution is complex or unknown. In contrast, the M/M/1 model assumes exponentially distributed service times, which simplifies the analysis and allows for exact analytical solutions.

The purpose of this project is to find an M/M/1 envelope that provides an upper bound on the queuing delays experienced in the M/G/1 system. By identifying an M/M/1 system with a higher queuing delay than the M/G/1 system for a range of quantiles, the M/M/1 envelope can be used as a conservative approximation for the M/G/1 system's performance.

Additionally, the project explores the relationship between the real M/G/1 load and the envelope M/M/1 load using polynomial regression.

## Installation and Usage

To use this project, you'll need to have R installed on your system. You can download R from the official website: [https://www.r-project.org/](https://www.r-project.org/)

The experiment utilizes the simmer package in R for discrete-event simulation of the M/G/1 system, you'll need to install the following R packages:

- `simmer`

You can install the required packages within R using the following command:

```r
install.packages("simmer")
```
Usage
1. Open the Queuing_envelope_mg1.Rmd file in RStudio or your preferred R IDE.
2. Set the input parameters, such as Capacity_Gbps, Load, PS_size, and PS_weights, as per your requirements.
3. The results, including plots and numerical outputs, will be displayed in the R Markdown document or PDF and HTML report.

The simmer_mg1 function simulates the M/G/1 system given parameters such as system capacity (Capacity_Gbps), load (Load), packet sizes (PS_size), and packet weights (PS_weights).
The envelope_load_calc function is used to determine the appropriate M/M/1 envelope load (rho_env) that upper-bounds the queuing delays for a given M/G/1 load. This is achieved by iterating over a range of candidate M/M/1 loads and finding the load where the quantiles of the exponential distribution (representing the M/M/1 delays) are above the quantiles of the simulated M/G/1 delays for the desired range (50% to 99% in this case).

## Input Data
The experiment uses the following input parameters:

Capacity_Gbps: 10 Gbps
Load: 0.7
PS_size: Packet sizes in bytes (40, 576, 1500)
PS_weights: Packet weights (7/12, 4/12, 1/12)

## Results
M/G/1 Simulation and Envelope M/M/1 Calculations
The M/G/1 system is simulated, and the packet delays (mg1_packets) are obtained.
The average delay (E_T_real) and other parameters (N, var_N, Cs2, nodes_capacity_Bps, Capacity_ps, E_X) for the M/G/1 system are calculated.
The envelope M/M/1 load (rho_env) is determined by finding the load where the M/M/1 quantiles upper-bound the M/G/1 quantiles for the desired range.
The identified rho_env is 0.77, and the corresponding average delay (E_X/(1-rho_env)) serves as an upper bound for the M/G/1 system's average delay (E_T_real).


## Polynomial Regression Model

A set of real M/G/1 loads (loads_real) is generated, and the corresponding envelope M/M/1 loads (loads_envelope) are computed using the envelope_load_calc function.
A quadratic polynomial regression model is fitted to the observed data points (loads_real, loads_envelope) to establish the relationship between the real M/G/1 load and the envelope M/M/1 load.

The coefficients of the fitted model are extracted, and the quadratic polynomial formula is constructed and printed:
```r
y(x) = 0.495076347314934 + 0.105061982739405 x + 0.414096953562388 x^2
```

This formula represents the relationship between the real M/G/1 load (x) and the predicted envelope M/M/1 load (y).

## Checking the Polynomial Prediction
The code then checks the polynomial prediction for a specific real M/G/1 load (loads_real = 0.57). The steps involved are:

Simulate the M/G/1 system using simmer_mg1 for the given load.
Predict the envelope M/M/1 load (load_envelope_predicted) using the fitted polynomial regression model.
Verify that all quantiles of the simulated M/G/1 delays (df_real) are below the quantiles of the corresponding M/M/1 exponential distribution (df_env) with the predicted envelope load.

## Polynomial Prediction for Different Packet Size Distributions
The final part of the code explores the polynomial prediction for different packet size distributions (PS_size and PS_weights). Three different distributions (V1, V2, and V3) are considered.
V1 - bytes (40, 576, 1500) with Packet weights (7/12, 4/12, 1/12);
v2 - https://www.ams-ix.net/ AMS-IX packet size statistics;
v3 -https://www.seattleix.net/ statistics from Internet Exchange Point in Seattle.

This analysis allows for evaluating the performance of the polynomial regression model in predicting the envelope M/M/1 load for different packet size distributions.
The provided code demonstrates the process of fitting a polynomial regression model to the data, checking the model's predictions against simulated values, and exploring the model's performance for different input parameters (packet size distributions).
