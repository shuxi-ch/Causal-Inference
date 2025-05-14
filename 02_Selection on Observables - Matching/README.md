### Overview  
This exercise benchmarks causal‐inference estimators against a randomized gold standard by analyzing the National Supported Work (NSW) demonstration (LaLonde, 1986) and a PSID control sample. We compute the unbiased experimental ATE, then apply naive, matching, and weighting methods to the observational data—highlighting how design, overlap, and balance affect causal recovery.

### Problem Statement  
Estimate the causal effect of the NSW employment program on 1978 earnings and assess how well observational methods (matching, weighting) approximate the true experimental ATE under varying assumptions of ignorability and overlap.


1. **RCT Benchmark (LaLonde, 1986)**  
  - **Objective:**  
    Use the randomized NSW demonstration to establish the unbiased effect of job‐training on 1978 earnings.  
  - **Approach:**  
    - Difference‐in‐means: computed ATE = **\$1 794** (SE = \$671).  
    - OLS with HC2 robust SEs: estimated ATE = **\$1 720.8** (SE = \$678).  
  - **Results:**  
    These estimates validate the RCT’s internal validity and serve as our benchmark.  
  - **Reference:**  
    LaLonde, R. J. (1986). *Evaluating the Econometric Evaluations of Training Programs with Experimental Data.* American Economic Review, 76(4), 604–620.  

2. **Observational Analysis (Dehejia & Wahba, 1999)**
  - **Objective:**  
    Recover the NSW ATE using non‐experimental PSID controls and explore bias‐correction methods.  
  - **Approach:**  
    1. **Naïve Estimates:**  
       - Unadjusted diff‐in‐means: ATE = **–\$15 204.8** (SE = \$657)  
       - Regression‐adjusted: ATE = **–\$1 459.6** (SE = \$932.7)  
    2. **Balance Diagnostics:**  
       - Tabulated means, SDs, and standardized differences (|sdiff| > 100) for age, education, race, marital status, earnings ’74/’75, unemployment.  
       - Omnibus F‐test confirmed imbalance (p < .001).  
    3. **Propensity‐Score Modeling:**  
       - Fitted logistic regression of treatment on covariates.  
       - Visualized PS overlap: good in RCT, poor in PSID.  
    4. **Matching Methods:**  
       - **Mahalanobis Matching** (education, earnings ’74/’75, unemployment ’74/’75; M=1):  
         - ATT = **\$1 782.9** (SE = \$998.98; p ≈ 0.074)  
       - **Exact Matching** (education, race, ethnicity, marital status):  
         - ATT = **–\$5 821.6** (SE = \$840.65)  
    5. **PS‐Matching & IPW:**  
       - **PS‐Matching** (NN on estimated PS): ATT = **\$1 771.8** (SE = \$1 915.1)  
       - **IPW**: ATT = **\$746.8**  
    6. **Comparative Diagnostics:**  
       - Benchmarked each ATT against the RCT ATE to illustrate bias–variance trade‐offs.  

### Key Concepts

* **Randomized Benchmark**: Using the RCT’s difference‐in‐means (and OLS with robust HC2 SEs) as the gold‐standard ATE for comparison.
* **Naïve Observational Bias**: Demonstrating how unadjusted difference‐in‐means and regression on PSID controls can produce severely biased ATEs.
* **Covariate Balance Diagnostics**:

  * **Standardized Differences**: Comparing means/SDs (|sdiff|) across treatment groups to detect imbalance.
  * **Omnibus F‐Test**: Joint test of covariate equality under randomization.
* **Propensity‐Score Methods**:

  * **Estimation**: Logistic regression of treatment on pre‐treatment covariates.
  * **Overlap Assessment**: Visualizing PS distributions to check common-support violations.
* **Matching Estimators**:

  * **Mahalanobis Matching**: Matching on a distance metric over key covariates to recover the experimental ATT.
  * **Exact Matching**: Aligning treated and control on discrete factors, illustrating trade-offs when continuous confounders remain imbalanced.
  * **PS‐Matching**: Nearest‐neighbor on the estimated PS with/without calipers.
* **Weighting**:

  * **Inverse-Probability Weighting (IPW)** to adjust for covariate imbalance.
  * **Bias-Variance Trade-Off**: How extreme weights inflate variance despite bias correction.
* **Comparative Diagnostics**: Benchmarks all ATT estimates against the RCT ATE to highlight which methods approximate the gold standard under realistic overlap and balance conditions.

### Technical Stack

* **Languages & Tools**: R, RMarkdown
* **Key Packages**:

  * **Data Wrangling & Visualization**: `tidyverse` (dplyr, ggplot2, tidyr)
  * **Import**: `haven`
  * **Matching & Weighting**: `Matching`, `ebal`, `cobalt` (balance plots)
  * **Regression & Robust SEs**: `estimatr`, `sandwich`, `lmtest`
  * **Tables & Reporting**: `modelsummary`, `gt`, `kableExtra`
  * **Testing**: `testthat` for smoke tests or sanity checks
