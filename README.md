# Granger-Causality-in-High-Dimensional-VARs (HDGC)

This Github repo contains the R scripts used to carry out Granger causality tests as used in the empirical applications of the paper: Hecq,A., Margaritella,L., Smeekes,S. (2019), "Granger Causality Testing in High-Dimensional VARs: a Post-Double-Selection Procedure" arXiv preprint arXiv:1902.10991.

                                             ########################
                                                   DESCRIPTION:
                                             ########################
# HDGC
Performs Granger causality test between x and y in a VAR(p) using the test procedure described in Hecq,A., Margaritella,L., Smeekes,S.,(2019)
This is a function that takes as imputs: 
- A standardized (std=F) dataset (data) of stationary time series, labeled by columns with their names
- Two time series (x,y) of interest to be tested for Granger causality while taking into account the possible interaction of many others confounders
- The number of lags (lags) to be used in the VAR(p)
- The information criteria (crit) to be used to perform the Lasso selection; options are: AIC,BIC(suggested),EBIC,AICC,HQC (see also ic_glmnetboundT)
- The type of penalization procedure desired (alpha), options are: 1 for Lasso, 0.5 for Elastic net
- The significance level (sign) of the test

# ic_glmnetboundT
The function is a wrapper of glmnet for estimating Lasso using Information Criteria (AIC,BIC,EBIC,HQ) to tune the penalty by applying a lower bound of 50% of the sample size (T). This means that ic.glmnet is forced to stop selecting variables after it selects K=50%(T); this is rather important in order to allow post-selection OLS estimation feasible (i.e. K<T). Note though that the more lags are used the more the penalty becomes most likely insufficient.

# NetGC
The function build Granger causality networks of realized volatilities using the test procedure described in Hecq,A.,
Margaritella,L., Smeekes,S.,(2019).
This is a function that takes as imputs: 
- A dataset (data) of stationary realized volatility time series, labeled by columns with their names
- log=T takes the log of all the series
- The information criteria (crit) to be used to perform the Lasso selection; options are: AIC,BIC(suggested),EBIC,AICC,HQC (see also ic_glmnetboundT)
- HR=TRUE uses a Heteroscedasticity correction for the LM test, otherwise performs a standard LM as HDGC()
- The type of penalization procedure desired (alpha), options are: 1 for Lasso, 0.5 for Elastic net
- The significance level (sign) of the test
- Plot type of plot desired: either a circle plot or a veins-type network
- cluster= TRUE calculate and plot clusters using edge-betweennes algorithm
- verbose= TRUE plot in console all the GC tests of the single series

