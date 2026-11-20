# From Mechanistic Model to Digital Twin: A Framework for Real-Time Optimization of Ethanol Production in *Saccharomyces cerevisiae*

## Overview

This repository contains the code and supporting materials for the study **“From Mechanistic Model to Digital Twin: A Framework for Real-Time Optimization of Ethanol Production in *Saccharomyces cerevisiae*.”**

The study presents a digital twin framework for the optimization and closed-loop control of fed-batch ethanol fermentation using *Saccharomyces cerevisiae*. The framework combines a mechanistic bioprocess model with recursive Bayesian state estimation and nonlinear model predictive control (NMPC).

The main objective is to improve process monitoring and control under nonlinear biological dynamics, changes in metabolic activity, batch-to-batch parameter variability, and limited availability of online biomass measurements.

By integrating mechanistic modelling, state estimation, and predictive control, the framework supports real-time estimation of unmeasured process states and the calculation of glucose feeding strategies to improve ethanol production.

## Methodology

The proposed digital twin combines three main components.

### 1. Mechanistic Bioprocess Model

A mechanistic model describes the dynamics of fed-batch ethanol fermentation by *Saccharomyces cerevisiae* under both aerobic and anaerobic conditions.

The model provides the process representation required for state estimation, prediction, and optimization. It also serves as the basis for evaluating how estimation and control perform when the model differs from the actual process.

### 2. Bayesian State Estimation and Soft Sensors

Recursive Bayesian filters are used to estimate process states that cannot be measured continuously, particularly biomass. The following approaches are implemented and benchmarked:

- **Extended Kalman Filter (EKF):** Uses local linear approximations to estimate the process state.
- **Ensemble Kalman Filter (EnKF):** Uses an ensemble of state estimates to represent uncertainty in nonlinear systems.
- **Particle Filter (PF):** Uses weighted samples to represent potentially nonlinear and non-Gaussian state distributions.

The estimated states are evaluated against reference measurements from high-performance liquid chromatography (HPLC) and Raman spectroscopy biomass data.

The filters are assessed in terms of prediction accuracy and computational requirements, with particular attention to their suitability for integration into predictive control.

### 3. Nonlinear Model Predictive Control

The digital twin based on the EKF is incorporated into an NMPC framework to calculate glucose feeding strategies for ethanol-yield optimization.

The controller operates in a closed loop: process measurements update the state estimates, the digital twin predicts future process behaviour, and an optimization problem determines the feeding actions. This procedure is repeated as new measurements become available.

The control framework is evaluated under parametric model–plant mismatches of 15–20% and heteroscedastic measurement noise to assess robustness under imperfect process knowledge and variable measurement uncertainty.

## Key Results

### State Estimation Performance

The Bayesian filters improved mean squared error (MSE) relative to predictions from the mechanistic model.

The reported improvements include:

| Operating condition | Filter | Reference data | MSE improvement |
|---|---|---|---:|
| Anaerobic | EKF | HPLC | 85% |
| Anaerobic | EnKF | HPLC | 83% |
| Anaerobic | PF | Raman | 59% |
| Aerobic | PF | HPLC | 53% |
| Aerobic | EnKF | HPLC | 52% |
| Aerobic | EKF | Raman | 36% |

These results demonstrate the potential of Bayesian state estimation to improve predictions when process measurements are limited and the underlying biological dynamics are nonlinear.

### Closed-Loop Optimization

The NMPC framework identified three distinct feeding strategies during optimization and achieved a **2.3% improvement in mass production**, as reported in the study.

The control framework maintained robust performance under the tested model–plant mismatches and heteroscedastic measurement noise, supporting the use of the digital twin for fed-batch process optimization.

## Key Features

- Mechanistic modelling of ethanol fermentation by *Saccharomyces cerevisiae*.
- Representation of both aerobic and anaerobic operating conditions.
- Bayesian state estimation using EKF, EnKF, and PF.
- Soft sensors for estimating unmeasured process states, including biomass.
- Evaluation against HPLC and Raman spectroscopy reference data.
- Integration of state estimation with nonlinear model predictive control.
- Closed-loop optimization of glucose feeding strategies.
- Robustness assessment under model–plant mismatch and nonconstant measurement noise.
- A framework for moving from mechanistic process models towards data-informed, real-time bioprocess control.

## Repository Contents

The repository is intended to provide the implementation and supporting materials associated with the study.

The following structure can be adapted to match the files actually included in the repository:

```text
.
├── models/          # Mechanistic fermentation models
├── state_estimation/ # EKF, EnKF, and PF implementations
├── control/         # NMPC formulation and feeding optimization
├── data/            # Experimental data or example datasets
├── results/         # Simulation outputs and evaluation results
├── notebooks/       # Analysis and reproducibility notebooks
└── README.md
```

*Note: The directory names above are a suggested organization, not a claim about the repository's current contents.*

## Reproducibility

To reproduce the results, users should follow the instructions provided with the source code and associated datasets. The implementation should specify the required software dependencies, model parameters, initial conditions, measurement configurations, filter settings, NMPC constraints, and optimization settings.

Where experimental data cannot be redistributed, the repository should document the data sources and any applicable access restrictions.

## Applications

The framework may be useful for:

- Monitoring fermentation processes with limited online measurements.
- Estimating biomass and other unmeasured process states.
- Optimizing glucose feeding during fed-batch fermentation.
- Evaluating control performance under model uncertainty.
- Developing digital twins for advanced bioprocess monitoring and control.

## Authors

- **Omar Bayomie** — Department of Biochemical Engineering, University College London, London, UK. Corresponding author.
- **Mauditra Matin** — Delft Institute of Applied Mathematics, Delft University of Technology, Delft, The Netherlands.
- **Yusmel González-Hernández** — Université Paris-Saclay, CentraleSupélec, Laboratoire de Génie des Procédés et Matériaux, CEBB, Pomacle, France.
- **Cedric Guerin** — Université Paris-Saclay, CentraleSupélec, Laboratoire de Génie des Procédés et Matériaux, CEBB, Pomacle, France.
- **Patrick Perré** — Université Paris-Saclay, CentraleSupélec, Laboratoire de Génie des Procédés et Matériaux, CEBB, Pomacle, France.

**Corresponding author:** Omar Bayomie  
Email: ucbeoba@ucl.ac.uk

## Citation

If you use this repository in your research, please cite the associated publication:

Bayomie, O., Matin, M., González-Hernández, Y., Guerin, C., & Perré, P. *From Mechanistic Model to Digital Twin: A Framework for Real-Time Optimization of Ethanol Production in Saccharomyces cerevisiae.*

Add the publication year, journal, volume, page numbers, and DOI when these details are available.

## License

Please refer to the license included in this repository for the terms governing the use, modification, and redistribution of the code and associated materials.
