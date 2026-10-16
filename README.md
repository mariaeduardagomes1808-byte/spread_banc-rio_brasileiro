# spread_bancario_brasileiro
Entendendo as variáveis que mais impactam o spread bancário
Overview
The bank spread is the difference between the rate banks charge on loans and their funding cost. It captures the cost of financial intermediation: default risk, operating costs, taxes, legal uncertainty, and profit margin. In Brazil it is high and reduces the power of monetary policy over the cost of credit.
This project investigates which macroeconomic variable best explains the behavior of the bank spread in Brazil. It combines:
a review of the econometric model of Oreiro et al. (2006), as discussed in the literature for 2002–2014;
own empirical tests with Banco Central do Brasil data (Selic, interest rate volatility, and exchange rate volatility);
an analysis of the spread over economic cycles and the role of public banks.
Research Question
Which macroeconomic variable is the most relevant, from a statistical point of view, to explain the behavior of the bank spread in Brazil?
Main Findings
Selic: the policy rate is the variable with the strongest fit among those tested, with a moderate positive correlation with the spread. This agrees with the literature model, in which the Selic coefficient is positive and statistically significant.
Lags: adding a one-month lag did not meaningfully increase the correlation, which suggests that the adjustment of the spread to the Selic is mostly contemporaneous (or that lagged effects are limited in the sample).
Interest rate volatility: the measure used (intramonth standard deviation of the daily rate) showed a low correlation with the spread.
Exchange rate volatility: also low correlation, with erratic behavior and isolated shocks that do not translate into persistent movements in the spread.
Cycles: the spread rises in periods of stress (recession, loss of confidence) and is compressed in periods of monetary easing. During the pandemic, the fall of the Selic kept the spread under control even as unemployment rose.
Public banks: they can act counter-cyclically, expanding credit when private banks retreat and pressing spreads down.
Literature model (Oreiro et al., 2006), reported in the report:
Variable	Reported effect on the spread	Consistent with theory?
Industrial production	-0.13	Yes
Selic	+1.02	Yes
Inflation (IPCA)	-1.56	No (possible multicollinearity with the Selic)
Reserve requirement	about -0.20	No (low variability in the period)
Conclusion: within the period and measures analyzed, level variables, especially the Selic rate, explain the spread better than volatility measures. The behavior of the spread is multifaceted and also depends on credit risk, default, and general macroeconomic conditions.
The distinction between observed associations and causal effects is essential: the report's own tests are correlations, not an estimated causal model.
Data Sources
All series come from the Banco Central do Brasil (SGS), downloaded with GetBCBData.
Series	SGS code	Used in
Selic (monthly average)	432	Graph 1
Consumer interest rate	20714	Graph 1
Bank spread	20783	Graphs 1, 2, 7 and 8 context
Bank spread (used in the correlation analysis)	20786	Graphs 3 to 6
Funding cost	10736	Graph 2
Default (credit risk)	21082	Graph 2
Selic (daily)	11	Graphs 3 to 5 and 7
US dollar (exchange rate)	1	Graph 6
Unemployment rate	24369	Graph 7
Credit from public banks (% of GDP)	20542	Graph 8
Credit from private banks (% of GDP)	20543	Graph 8
Data period and frequency: daily and monthly series. Graph 1 starts in 2005, Graph 2 in 2011, Graphs 3–7 in 2012, and Graph 8 in 2007.
Literature: Oreiro et al. (2006); Afonso, Kohler and Freitas (2009); Da Silva, Oreiro and De Paula (2007); academic article on monetary policy and the bank lending channel (spread 2002–2014).
Methodology
Data collection: SGS API through gbcbd_get_series().
Data preparation: daily series converted to monthly averages; the daily Selic is converted from % per day to % per year in Graph 7 with ((1 + r/100)^252 - 1) × 100.
Decomposition of the credit cost indicator (Graph 2): annual averages of funding cost, default, and spread. The remainder of the spread after default is split into administrative expenses, taxes and FGC, and margin using fixed weights (17.25, 14.25, and 13.44) from a table of reference weights.
Literature model: multiple regression in levels estimated by OLS (156 observations):
   Spread = β0 + β1·ind + β2·Infl + β3·Selic + β4·Comp + ε
where ind is industrial production, Infl is monthly IPCA, Selic is the policy rate, and Comp is the reserve requirement. 5. Correlation analysis: Selic vs. spread, with and without a one-month lag of the spread. 6. Volatility analysis: correlation of the spread with the monthly volatility of the Selic and of the exchange rate (standard deviation of daily values within each month). 7. Cycle analysis: spread, unemployment, and Selic during the 2015–2016 recession and the pandemic, and credit from public vs. private banks (2008 crisis, recession, and pandemic).
Repository Structure
text
.
├── spread_bancario.Rmd     
└── README.md
Rename spread_bancario.Rmd to match your file name. No local data files are needed, since all data are downloaded from the BCB API.
How to Reproduce
Requirements: R, RStudio (recommended), and internet access.
Open the .Rmd file in RStudio.
Install the required packages:
r
   install.packages(c(
     "dplyr", "tidyverse", "lubridate", "highcharter", "GetBCBData"
   ))
Click Knit to generate the HTML report.
Note: the series are downloaded when the document is knitted and are updated over time, so results may differ slightly from the published report.
Limitations
Descriptive evidence alone does not establish a causal relationship between the Selic and the bank spread.
The econometric model (Oreiro et al., 2006) is taken from the literature and refers to 2002–2014. It is not estimated in this code, and its coefficients should be read as direction and dynamics, not as current magnitudes.
Inflation and the reserve requirement have signs opposite to theory in the literature model, possibly due to multicollinearity and omitted variable bias (interest rate volatility).
The volatility proxies (intramonth standard deviation) may not capture the macroeconomic risk that matters for credit pricing. Broader indicators, such as country risk, could be tested.
The decomposition in Graph 2 uses fixed weights to split the remainder of the spread, so it is an illustration and not an observed breakdown.
The correlation analysis is bivariate and does not control for other determinants such as default, inflation, or economic activity.
Authors
Maria Eduarda de Oliveira Gomes
Matheus Coelho
Laura Borelli
