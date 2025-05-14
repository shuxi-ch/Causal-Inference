# Causal Inference in Political Science

## Overview  
This repository aggregates four self-contained causal‐inference exercises—ranging from lab experiments to longitudinal panel analysis—each in its own folder with detailed READMEs:

1. **01_Potential outcomes & Randomized experiments**  
   - **Lab:** Replicates Huber, Hill & Lenz’s allocator‐retention game.  
   - **Field:** Reproduces Olken’s Indonesian road‐audit RCT.  
   - **Focus:** Difference‐in‐means ATE, OLS with HC2 SEs, balance diagnostics, subgroup heterogeneity.

2. **02_Selection on Observables – Matching**  
   - **RCT Benchmark:** LaLonde’s NSW demo ATE.  
   - **Observational:** PSID controls with propensity‐score modeling, Mahalanobis/exact/PS matching, IPW.  
   - **Focus:** Unadjusted vs. adjusted ATE, overlap diagnostics, bias–variance trade‐offs.

3. **03_Cross‐sectional Designs – IV & RDD**   
   - **IV:** Acemoglu–Johnson–Robinson colonial‐origins design.  
   - **RDD:** Lee’s U.S. House incumbency advantage.  
   - **Focus:** DAGs, reduced‐form vs. 2SLS LATE (weak‐instrument F‐tests), parametric & local‐linear RDD, manipulation/continuity checks.

4. **04_Longitudinal Designs – DiD & Fixed Effects**  
   - **DiD:** Vietnam’s 2009 re‐centralization on six service indices.  
   - **Panel:** U.S. union membership wage premium (1980–1987).  
   - **Focus:** Raw DiD, OLS with clustered SEs, parallel‐trends & placebo tests, within estimator, one‐ and two‐way FE.


## Directory layout  

   ```bash
   .
   ├── .gitignore
   ├── README.md
   ├── 01_Potential outcomes & Randomized experiments
   │   ├── README.md
   │   ├── data
   │   │   ├── [Field Experiment]olken_data.csv
   │   │   └── [Lab Experiment]incumbentGame.csv
   │   ├── docs
   │   │   └── Lab & Field Causal Analysis: Game & Olken Audit.pdf
   │   └── R
   │       └── Lab & Field Causal Analysis: Game & Olken Audit.Rmd
   ├── 02_Selection on Observables – Matching
   │   ├── README.md
   │   ├── data
   │   │   ├── nsw_exper.dta
   │   │   └── nsw_psid_withtreated.dta
   │   ├── docs
   │   │   └── NSW Experiment & Observational Matching.pdf
   │   └── R
   │       └── NSW Experiment & Observational Matching.Rmd
   ├── 03_Cross-sectional Designs – IV and RDD
   │   ├── README.md
   │   ├── data
   │   │   ├── ajr_data.dta
   │   │   └── lee.dta
   │   ├── docs
   │   │   └── Acemoglu IV & Lee Sharp RDD.pdf
   │   └── R
   │       └── Acemoglu IV & Lee Sharp RDD.Rmd
   └── 04_Longitudinal Designs – DiD and Fixed Effect
       ├── README.md
       ├── data
       │   ├── maleskyetal_placebo.dta
       │   ├── maleskyetal.dta
       │   └── wagepan_wide.csv
       ├── docs
       │   └── DID on Public Services & Wage Panel Estimators.pdf
       └── R
           └── DID on Public Services & Wage Panel Estimators.Rmd
   ```
