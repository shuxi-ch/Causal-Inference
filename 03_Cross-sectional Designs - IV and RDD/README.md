### Overview  

This exercise applies instrumental‐variables and regression‐discontinuity methods to two canonical political‐economy studies, using DAGs to justify identification and a suite of robustness checks to validate causal estimates:

1. **AJR Colonial-Origins IV Design (Acemoglu, Johnson & Robinson, 2001)**  
   * **Objective:** Estimate the causal effect of institutional strength (expropriation protection) on modern GDP per capita using historical settler mortality as an instrument.  
   * **Approach:**  
     - Specified a DAG with instrument (`log_mortality`), treatment (`exprop_prot`), outcome (`log_gdp`), and unobserved confounder.  
     - Fitted naive OLS:  
       ```r
       lm(log_gdp ~ exprop_prot)
       # β̂ = 0.522 (SE = 0.050)
       ```  
     - Estimated reduced form:  
       ```r
       lm(log_gdp ~ log_mortality)
       # β̂ = –0.573 (SE = 0.074)
       ```  
     - Conducted two‐stage least squares via `ivreg()`:  
       - Unadjusted LATE = **0.944** (SE = 0.157; F = 22.95)  
       - Covariate‐adjusted LATE = **1.107** (SE = 0.464; F = 3.46)  
   * **Results:** LATE estimates of 0.94–1.11 log points validate the instrument’s strength and substantiate institutions’ payoffs in GDP.  
   * **Reference:**  
     Acemoglu, D., Johnson, S., & Robinson, J. A. (2001). *The Colonial Origins of Comparative Development: An Empirical Investigation.* American Economic Review, 91(5), 1369–1401.  
     https://doi.org/10.1257/aer.91.5.1369  

2. **Sharp RDD: U.S. House Incumbency Advantage (Lee, 2008)**  
   * **Objective:** Quantify the causal vote‐share boost from barely winning a prior House election at the 50% margin cutoff.  
   * **Approach:**  
     - Constructed forcing variable (`margin_tm1`), treatment indicator (`incumbent`), and outcome (`share_t`).  
     - Estimated parametric RDDs:  
       ```r
       lm(share_t ~ incumbent + margin_tm1)               # β̂ = 0.113 (SE = 0.003)
       lm(share_t ~ incumbent * margin_tm1)               # β̂ = 0.108 (SE = 0.003)
       lm(share_t ~ incumbent * margin_tm1 + I(margin_tm1^2))  # β̂ = 0.070 (SE = 0.004)
       ```  
     - Ran local‐linear RDD with triangular kernel at Imbens–Kalyanaraman bandwidth (h ≈ 0.20):  
       - LATE = **0.086**  
     - Conducted robustness checks: bandwidth sweep (0.01–0.30) and McCrary density test (p = 0.925).  
     - Tested covariate continuity on office experience: jump = 1.574 terms (p < .001).  
   * **Results:** Estimated incumbency advantage of ≈11 pp (parametric) and ≈8.6 pp (local‐linear), with no manipulation at the cutoff.  
   * **Reference:**  
     Lee, D. S. (2008). *Randomized Experiments from Non‐random Selection in U.S. House Elections.* Journal of Econometrics, 142(2), 675–697.  
     https://doi.org/10.1016/j.jeconom.2007.05.015  


### Key Concepts

* **DAG Specification & Back-Door Criterion**: Visualize confounders and justify adjustment sets.  
* **Reduced-Form vs. Structural IV**: Compare direct OLS and two‐stage least squares (LATE) estimates.  
* **Weak‐Instrument Diagnostics**: Report F‐statistics to assess instrument strength.  
* **Sharp RDD**: Parametric and nonparametric estimation at a cutoff with kernel methods.  
* **Robustness & Validity Checks**: Bandwidth sensitivity, density manipulation tests, and covariate continuity.  

### Technical Stack

* **Languages & Tools**: R, RMarkdown  
* **Key Packages**:  
  - **Data Wrangling & Visualization**: `tidyverse` (dplyr, ggplot2, tidyr)  
  - **DAGs**: `dagitty`, `ggdag`  
  - **IV Estimation**: `AER` (`ivreg`), `sandwich` (HC2), `lmtest`  
  - **RDD**: `rdd`, `rdrobust`  
  - **Reporting**: `modelsummary`, `gt`, `kableExtra`  
  - **Diagnostics**: `cobalt` (balance), `rddensity` (McCrary test)  
