# Granger-Causality-in-High-Dimensional-VARs (GCHDVAR)

This Github repo contains the R scripts used to carry out simulations and the empirical applications of the paper: Hecq,A., Margaritella,L., Smeekes,S. 2019: "Granger Causality Testing in High-Dimensional VARs: a Post-Double-Selection Procedure" (forthcoming).

                                             ########################
                                                   DESCRIPTION:
                                             ########################
# TS Simulations 
The script contains three DGPs for simulating stationary VAR(p) with identity variance covariance matrix


# TS Simulations with Vcov 
The script contains three DGPs for simulating stationary VAR(p) with Toeplitz variance covariance matrix


# Lasso_info_criteria(ic.glmnet) 
The script contains the function (ic.glmnet) which is a wrapper of glmnet for estimating Lasso using Information Criteria (AIC,BIC,EBIC,HQ) to tune the penalty


# Lasso_info_criteria_BOUND(T)(ic.glmnetboundedT) 
The script contains the function (ic.glmnetboundedT) which is a wrapper of glmnet for estimating Lasso using Information Criteria (AIC,BIC,EBIC,HQ) to tune the penalty by applying a lower bound on the penalty of 50% of the sample size (T). This means that ic.glmnet is forced to stop selecting variables after it selects K=50%(T); this is rather important in order to allow post-selection OLS estimation feasible (i.e. K<T).


# RV Contagion Network (LM)
The script allows to use the post-double selection method proposed in Hecq,A., Margaritella,L., Smeekes,S. 2019 in a Heterogeneous VAR modeling framework to estimate a Realized volatility contagion networks.


# RV contagion network (Bivariate GC)
Bivariate GC alternative to RV Contagion Network (LM)
