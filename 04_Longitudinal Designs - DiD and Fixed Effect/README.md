### Overview  

This exercise applies difference‐in‐differences and panel‐data methods to two causal‐inference problems: 

1. **DiD** – Vietnam’s 2009 re‐centralization on six public‐service indices.  
2. **Panel Data** – Union membership’s wage premium (U.S. 1980–1987).
   
By combining OLS with clustered SEs, parallel‐trends checks, placebo tests, and fixed‐effects estimators, we validate causal assumptions and quantify treatment effects.

1. **Difference‐in‐Differences (Vietnam Re‐centralization)**
     * **Objective:**   
       Assess whether the 2009 recentralization reform improved service delivery across Health, Communication, Infrastructure, Agriculture, Education, and Business Development indices.  
     * **Approach:**  
       - Computed raw DiD via group means for each index.  
       - Estimated OLS:  
         ```r
         lm(index ~ treatment * treat + lnarea + lnpopden + city + factor(reg8), data)
         ```  
         with SEs clustered by district.  
       - Visualized 2006–2010 parallel trends (±95% CI) with a 2009 cutoff.  
       - Conducted a placebo test using a fake 2007 treatment date.  
     * **Results:**  
       - **Health:** +0.123 (SE = 0.032, p < 0.001)  
       - **Communication:** +0.152 (SE = 0.071, p < 0.05)  
       - **Infrastructure:** +0.225 (SE = 0.125, p = 0.072)  
       - No effects on Agriculture, Education, Business Development.  
       - Placebo confirms valid pre‐trends for 5/6 indices (infrastructure marginal).  
     * **Reference:**  
       Malesky, E., Nguyen, C. V., & Tran, A. (2014). *The Impact of Recentralization on Public Services: A Difference-in-Differences Analysis of the Abolition of Elected Councils in Vietnam.* American Political Science Review, 108(1), 144–168. https://doi.org/10.1017/S0003055413000580

2. **Panel Data (Union Wage Premium, 1980–1987)**
     * **Objective:**   
       Estimate the causal wage premium of union membership, controlling for individual and time effects.  
     * **Approach:**  
       - Reshaped `wagepan_wide.csv` (545 workers × 8 years, N = 4 360) into long format.  
       - **Pooled OLS:**  
         ```r
         lm(lwage ~ educ + black + hisp + exper + I(exper^2) + married + union)
         ```  
       - **Manual Within Estimator:** Demeaned by worker and ran DF‐corrected OLS.  
       - **Fixed Effects:** Used `plm` for one‐way (individual) and two‐way (individual + year) FE with cluster‐robust SEs.  
       - Compared estimates across models.  
     * **Results:**  
       - **Pooled OLS:** +18.0 % (SE = 1.7 %, p < 0.001)  
       - **Within Estimator:** +16.1 % (SE = 1.9 %, p < 0.001)  
       - **Two‐Way FE:** +8.0 % (SE = 2.3 %, p < 0.001) – demonstrating bias reduction.  
     * **Reference:**  
       Card, D. (1996). *The Effect of Unions on the Distribution of Wages: A Panel Data Analysis.* Econometrica, 64(4), 921–958. https://doi.org/10.2307/2171830

### Key Concepts

* **Difference‐in‐Differences:** Pre‐post comparison across treatment/control groups.  
* **Parallel‐Trends Assumption:** Checked via event‐study plots and placebo regressions.  
* **Placebo Tests:** Fake treatment dates to detect pre‐existing trends.  
* **Fixed Effects:** Within‐unit demeaning and two‐way FE to control confounders.  
* **Clustered SEs:** Account for within‐cluster correlation (district or individual).  
* **Bias Reduction:** Illustrating how fixed‐effects mitigate omitted‐variable bias.

### Technical Stack

* **Languages & Tools:** R, RMarkdown  
* **Key Packages:**  
  * **Data Wrangling & Reshaping:** `tidyverse` (dplyr, tidyr)  
  * **Panel Data Models:** `plm`  
  * **Regression & Robust SEs:** `estimatr`, `sandwich`, `lmtest`  
  * **Visualization:** `ggplot2`, `gridExtra`  
  * **Reporting:** `modelsummary`, `kableExtra`  
