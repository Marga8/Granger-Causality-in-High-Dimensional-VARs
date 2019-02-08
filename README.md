# Granger-Causality-in-High-Dimensional-VARs (HDGC)

This Github repo contains the R scripts used to carry out Granger causality tests as used in the empirical applications of the paper: Hecq,A., Margaritella,L., Smeekes,S. 2019: "Granger Causality Testing in High-Dimensional VARs: a Post-Double-Selection Procedure" (forthcoming).

                                             ########################
                                                   DESCRIPTION:
                                             ########################
# HDGC
This is a function that takes as imputs: 
- A standardized (std=F) dataset (data) of stationary time series, labeled by columns with their names
- Two time series (x,y) of interest to be tested for Granger causality while taking into account the possible interaction of many others confounders
- The number of lags (lags) to be used in the VAR(p)
- The information criteria (crit) to be used to perform the Lasso selection; options are: AIC,BIC(suggested),EBIC,AICC,HQC (see also ic_glmnetboundT)
- The type of penalization procedure desired (alpha), options are: 1 for Lasso, 0.5 for Elastic net
- The significance level (sign) of the test

# ic_glmnetboundT
The function is a wrapper of glmnet for estimating Lasso using Information Criteria (AIC,BIC,EBIC,HQ) to tune the penalty by applying a lower bound of 50% of the sample size (T). This means that ic.glmnet is forced to stop selecting variables after it selects K=50%(T); this is rather important in order to allow post-selection OLS estimation feasible (i.e. K<T). Note though that the more lags are used the more the penalty becomes most likely insufficient.




#####################################################################################################################################
#####################################################################################################################################                                            
# TS Simulations 
The script contains three DGPs for simulating stationary VAR(p) with identity variance covariance matrix


# TS Simulations with Vcov 
The script contains three DGPs for simulating stationary VAR(p) with Toeplitz variance covariance matrix


# Lasso_info_criteria(ic.glmnet) 
The script contains the function (ic.glmnet) which is a wrapper of glmnet for estimating Lasso using Information Criteria (AIC,BIC,EBIC,HQ) to tune the penalty

# RV Contagion Network (LM)
The script allows to use the post-double selection method proposed in Hecq,A., Margaritella,L., Smeekes,S. 2019 in a Heterogeneous VAR modeling framework to estimate a Realized volatility contagion networks.

# RV contagion network (Bivariate GC)
Bivariate GC alternative to RV Contagion Network (LM)
