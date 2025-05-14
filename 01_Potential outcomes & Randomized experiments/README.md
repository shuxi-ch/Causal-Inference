### Overview

This exercises applies foundational causal‐inference methods to two classic experimental designs—one in the lab and one in the field—to practice unbiased ATE estimation, robust regression adjustment, and heterogeneity analysis.

1. **Lab Experiment (Huber, Hill & Lenz, 2014)**

   * **Objective**: Replicate the incumbent–allocator game to estimate how allocator “type” (high vs. low performance) and recent “late luck” (winning streak) influence participants’ decisions to retain asset managers.
   * **Approach**:

     * Tabulated conditional retention rates (2×2 difference‐in‐means).
     * Fitted OLS models with HC2 robust standard errors for `kept ~ type + late.luck` and `kept ~ type * late.luck`.
   * **Results**:

     * High‐type allocator increases retention by **19.1 pp** (p < .001).
     * “Late luck” contributes a **6.1 pp** boost (p < .05).
     * No significant interaction effect.
   * **Reference**: Huber, G., Hill, S., & Lenz, R. (2014). *Sources of Bias in Experimental Design*. [NBER Working Paper No. 20498](https://www.nber.org/papers/w20498).

2. **Field Experiment (Olken, 2007)**

   * **Objective**: Assess the impact of community monitoring on missing expenditures in Indonesian village road‐building projects.
   * **Approach**:

     * Conducted balance diagnostics (means, SDs, t‐tests; omnibus F‐test p = .943).
     * Estimated ATE via difference‐in‐means and covariate‐adjusted OLS with HC2 SEs.
     * Performed subgroup analysis by village poverty (> 50% poor).
   * **Results**:

     * ATE on missing funds: **–2.5 pp** (SE = 3.3 pp), not statistically significant.
     * Covariate adjustment marginally reduced SE (0.0335 → 0.0326).
     * No evidence of heterogeneity by poverty (∆ATE SE = 0.068).
   * **Reference**: Olken, B. A. (2007). *Monitoring Corruption: Evidence from a Field Experiment in Indonesia*. *Journal of Political Economy*, 115(2), 200–249. [DOI:10.1086/517935](https://doi.org/10.1086/517935).

### Key Concepts

* **Difference‐in‐Means ATE**: Unadjusted and covariate‐adjusted estimates to quantify treatment effects under randomization.
* **Robust Regression**: OLS with HC2 standard errors to guard against heteroscedasticity.
* **Interaction Models**: Testing effect modification by including product terms.
* **Balance Diagnostics**:
  * Covariate means/SDs and t‐tests to verify randomization.
  * Omnibus F-test for joint balance.
* **Heterogeneity Analysis**: Subgroup ATE estimation and difference‐of‐coefficients testing to explore differential effects.

### Technical Stack

* **Languages & Tools**: R, RMarkdown
* **Packages**:

  * Data wrangling & visualization: `tidyverse` (dplyr, ggplot2, tidyr)
  * Import: `haven`
  * Regression & SEs: `estimatr`, `sandwich`, `lmtest`
  * Tables & reports: `modelsummary`, `gt`, `kableExtra`
