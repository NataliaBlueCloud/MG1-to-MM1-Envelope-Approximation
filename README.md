# M/G/1 to M/M/1 Envelope Approximation

This repository contains an R Markdown document and accompanying code for approximating queuing delays from an M/G/1 (Markovian arrival process, General service time distribution, single server) queuing system using an M/M/1 (Markovian arrival process, Exponential service time distribution, single server) envelope.

## Table of Contents

- [Overview](#overview)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Overview

The M/G/1 queuing model is more general and can accommodate various service time distributions, including non-exponential distributions. However, analyzing and obtaining closed-form solutions for the M/G/1 model can be challenging, especially when the service time distribution is complex or unknown. In contrast, the M/M/1 model assumes exponentially distributed service times, which simplifies the analysis and allows for exact analytical solutions.

The purpose of this project is to find an M/M/1 envelope that provides an upper bound on the queuing delays experienced in the M/G/1 system. By identifying an M/M/1 system with a higher queuing delay than the M/G/1 system for a range of quantiles, the M/M/1 envelope can be used as a conservative approximation for the M/G/1 system's performance.

Additionally, the project explores the relationship between the real M/G/1 load and the envelope M/M/1 load using polynomial regression.

## Installation

To use this project, you'll need to have R installed on your system. You can download R from the official website: [https://www.r-project.org/](https://www.r-project.org/)

Additionally, you'll need to install the following R packages:

- `simmer`

You can install the required packages within R using the following command:

```r
install.packages("simmer")
```
## Usage
1. Open the Queuing_envelope_mg1.Rmd file in RStudio or your preferred R IDE.
2. Set the input parameters, such as Capacity_Gbps, Load, PS_size, and PS_weights, as per your requirements.
3. The results, including plots and numerical outputs, will be displayed in the R Markdown document or PDF and HTML report.

