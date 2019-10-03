# Granger-Causality-in-High-Dimensional-VARs (HDGC)

This Github repo contains the R scripts used to carry out Granger causality tests as used in the empirical applications of the paper: Hecq,A., Margaritella,L., Smeekes,S. (2019), "Granger Causality Testing in High-Dimensional VARs: a Post-Double-Selection Procedure" arXiv preprint arXiv:1902.10991.

                                             ########################
                                                   DESCRIPTION:
                                             ########################
# HDGC
Performs Granger causality test between serie x and serie y in a VAR(p) using the Post-Double-Selection LM test procedure described in Hecq,A., Margaritella,L., Smeekes,S.,(2019)

This is a function that takes as imputs: 
- A standardized (std=F) dataset (data) of stationary time series, labeled by columns with their names
- Two time series (x,y) of interest to be tested for Granger causality while taking into account the possible interaction of many others confounders
- The number of lags (lags) to be used in the VAR(p)
- The information criteria (crit) to be used to perform the Lasso selection; options are: AIC,BIC(suggested),EBIC,AICC,HQC (see also ic_glmnetboundT)
- The type of penalization procedure desired (alpha), options are: 1 for Lasso, 0.5 for Elastic net
- The significance level (sign) of the test

Ex: Money-Income Causality using FRED-QD dataset 
(all time series are stationary-transformed according to Matlab script available on the FRED website. https://research.stlouisfed.org/econ/mccracken/fred-databases/)
    
   HDGC(x="M1REALx",y="GDPC96",data=FREDQD_data,std=F,lags=2,crit="bic",alpha=1,sign = 0.05)

# ic_glmnetboundT
The function is a wrapper of glmnet, originally proposed by Vasconcelos (pkg HDeconometrics,2017). With our modifications it estimates Lasso using Information Criteria (AIC,BIC,EBIC,HQ) to tune the penalty and applies a lower bound of 50% of the sample size (T). This means that ic.glmnet is forced to stop selecting variables (K) after it selects K=50%(T); this is necessary in order to allow post-selection OLS estimation feasible (i.e. K<T). Note though that the more lags are used the more the lower bound becomes most likely insufficient.
ic_glmnetboundT is used in the code of both HDGC and NetGC.

# NetGC
NetGC<-function(data,log,crit,alpha,HR,sign,plot=c("circle","veins"),cluster,verbose)

The function build Granger causality networks of realized volatilities using the test procedure described in Hecq,A.,
Margaritella,L., Smeekes,S.,(2019).

This is a function that takes as imputs: 
- A dataset (data) of stationary realized volatility time series, labeled by columns with their names
- log=T takes the log of all the series
- The information criteria (crit) to be used to perform the Lasso selection; options are: AIC,BIC(suggested),EBIC,AICC,HQC (see also ic_glmnetboundT)
- HR=TRUE uses a Heteroscedasticity correction for the LM test, otherwise performs a standard LM as HDGC()
- The type of penalization procedure desired (alpha), options are: 1 for Lasso, 0.5 for Elastic net
- The significance level (sign) of the test
- plot=c("circle","veins") gives the type of plot desired: either a circle plot or a veins-type network
- cluster= TRUE calculate and plot clusters using edge-betweennes algorithm
- verbose= TRUE plot in console all the GC tests of the single series
 
 Ex: Networks in Realized volatilities (49 large capitalization stocks, daily transactions 01/01/1999-31/12/2007)
 
   NetGC(data=RVolatility_data,log=T,crit="bic",alpha=1,HR=T,sign=0.01,plot=c("circle"),cluster=T,verbose=F)


