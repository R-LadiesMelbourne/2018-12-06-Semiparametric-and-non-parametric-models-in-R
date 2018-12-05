Non-parametric and Semi-parametric models in R
========================================================
author: Soroor Hediyehzadeh - Walter and Eliza Hall Institute of Medical Research
date: December 2018
autosize: true

About #rstats lunch seminars
========================================================

- 45 - 50 minutes online sessions via Zoom
- Aims to enhance the statistical knowledge and expertise of the RLadies community
- Topics include statistical and statistical learning models

Recent achievements of RLadies Melbourne Members
========================================================
**Congradulations!**
- To **Earo Wang** for 2018 ASA Statistical Graphics Student Paper Award
- And to our very own **Alexandra Garnham** for 2018 ABACBS Professional Bioinformatician Award

Non-parametric vs Parametric models
========================================================

- Strong distributional assumptions behind parametric models >> less flexibility
- No assumptions about distribution of the data in non-parametric modelling. Models are more flexible, and more complex.
- Parametric models are generalizable, while non-parametric models are not
-    >> Bias - variance trade-off: parametric estimates have smaller variance and large bias,
        non-parametric models have small bias, but large variance
        
Non-parametric Estimation
========================================================

- Non-parametric Density Estimation : 
	- Histogram
	- Kernel Density Estimation
- Non-parametric Regression : 
	- Nadyara-Watson estimator
	- Local Polynomial estimators
	- splines

Non-parametric Density Estimation
========================================================
- Histogram 
- Kernel Density Estimation (KDE)

![KDE_1](./semiparametric_models_RLadies-figure/KDE_def.png)

Kernel Density Estimation
========================================================
![](./semiparametric_models_RLadies-figure/KDE_sum.png)

KDE - choices for kernels
==========
![](./semiparametric_models_RLadies-figure/KDE_kernels.png)

Non-parametric Regression
========================================================
Typically used for trend estimation. Models conditional expectation of the response

![](./semiparametric_models_RLadies-figure/kernel_regression.png)

N-W estimator (local constant regression)
=======================

<img src="./semiparametric_models_RLadies-figure/NW_estimator.png" title="plot of chunk unnamed-chunk-1" alt="plot of chunk unnamed-chunk-1" width="1100px" />

N-W estimator
======================
<img src="./semiparametric_models_RLadies-figure/NW_plot.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" width="800px" />

Local Polynomial Regression
======================

<img src="./semiparametric_models_RLadies-figure/local_polynomial.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" width="1200px" style="display: block; margin: auto;" />

<img src="./semiparametric_models_RLadies-figure/local_polynomial_b.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" width="600px" style="display: block; margin: auto;" />

<img src="./semiparametric_models_RLadies-figure/local_polynomial_estim.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" width="1200px" style="display: block; margin: auto;" />



Splines
======================
- splines: Fix a number of data points. These points are called **knots**. Then, fit piecewise polynomials between knots. Typically local polynomial order 4 is used, which are called cubic splines.

<img src="./semiparametric_models_RLadies-figure/TPS.png" title="plot of chunk unnamed-chunk-6" alt="plot of chunk unnamed-chunk-6" width="950px" style="display: block; margin: auto;" /><img src="./semiparametric_models_RLadies-figure/B_splines.png" title="plot of chunk unnamed-chunk-6" alt="plot of chunk unnamed-chunk-6" width="950px" style="display: block; margin: auto;" />

*In the above expressions, epsilons are  __knots__*

Splines
========================

<img src="./semiparametric_models_RLadies-figure/locfit.png" title="plot of chunk unnamed-chunk-7" alt="plot of chunk unnamed-chunk-7" width="500px" style="display: block; margin: auto;" />

Smoothing Splines
================================

- Avoid selection of Knots
  * All distinct data points are taken as knots
- Have control on the curvature (i.e. smoothness) of the fit

<img src="./semiparametric_models_RLadies-figure/smooth_spline.png" title="plot of chunk unnamed-chunk-8" alt="plot of chunk unnamed-chunk-8" width="600px" style="display: block; margin: auto;" />


<img src="./semiparametric_models_RLadies-figure/smooth_spline_b.png" title="plot of chunk unnamed-chunk-9" alt="plot of chunk unnamed-chunk-9" width="450px" style="display: block; margin: auto;" />


<img src="./semiparametric_models_RLadies-figure/ghat.png" title="plot of chunk unnamed-chunk-10" alt="plot of chunk unnamed-chunk-10" width="410px" style="display: block; margin: auto;" />

Semi-parametric models
========================================================
- Non-parametric models require estimation of a large number of parameters, resulting in very complex models >> **curse of dimensionality**

- Use a combination of parametric and non-parametric models to avoid estimation of large # of parameters >> **semi-parametric models**

Semi-parametric models include:
=========================
* Additive Models 
<img src="./semiparametric_models_RLadies-figure/additive.png" title="plot of chunk unnamed-chunk-11" alt="plot of chunk unnamed-chunk-11" width="380px" style="display: block; margin: auto;" />
* Partial linear models   
<img src="./semiparametric_models_RLadies-figure/PL.png" title="plot of chunk unnamed-chunk-12" alt="plot of chunk unnamed-chunk-12" width="410px" style="display: block; margin: auto;" />

* Generalized Partial Linear models
<img src="./semiparametric_models_RLadies-figure/GPL.png" title="plot of chunk unnamed-chunk-13" alt="plot of chunk unnamed-chunk-13" width="410px" style="display: block; margin: auto;" />

* Generalized additive model
* Single Index model - link function unknown

Parkinson's Telemonitoring Dataset
===================
- Response variables:
 * motor_UPDRS
 * total_UPDRS
- Covariates:
 * NHR,HNR
 * RPDE - A nonlinear dynamical complexity measure
 * DFA - Signal fractal scaling exponent
 * PPE - A nonlinear measure of fundamental frequency variation
 * Jitter(Abs)
 * Shimmer
 
Parkinson's Telemonitoring Dataset
===================

* 2-D KDE


```r
# Generate 2-d density plots
contour(kde2d(Upd_avg[,param], Upd_avg$total_UPDRS, n=100),
				xlab = param, ylab = "total_UPDRS")
```

<img src="./semiparametric_models_RLadies-figure/2D_KDE.png" title="plot of chunk unnamed-chunk-15" alt="plot of chunk unnamed-chunk-15" width="710px" style="display: block; margin: auto;" />

Parkinson's Telemonitoring Dataset
===================
* Kernel regression

```r
plot(ksmooth(x, y, kernel = "normal", bandwidth =bw))
points(x,y)
```

<img src="./semiparametric_models_RLadies-figure/parkinson_nw.png" title="plot of chunk unnamed-chunk-17" alt="plot of chunk unnamed-chunk-17" width="710px" style="display: block; margin: auto;" />


Parkinson's Telemonitoring Dataset
===================
__Fitting GAM (Generalized Additive Models) with the *mgcv* CRAN package__
* Recall that the covariates in the dataset are a combination of linear and non-linear covariates
* We use the `gam()` function to fit a Generalized Additive model with a Gaussian link function. The model consists of linear fit for linear covariates, and regression splines, denoted by `s()`, for non-linear terms. This is an extention to the Generalized Partial Linear model.

Parkinson's Telemonitoring Dataset
===================
__Fitting GAM (Generalized Additive Models) with the *mgcv* CRAN package__


```r
library(mgcv)
fit <- gam(motor_UPDRS ~ age + sex + Jitter + 
					 	JitterAbs + JitterRAP + 
					 	JitterDDP + Shimmer +
					 	ShimmerAPQ3 + 
					 	NHR + HNR + DFA + s(PPE) + s(RPDE)+
						s(subject,bs="re"), data = dat, method = "REML")
```
`s(, bs="re")` is a way to incorporate random effect terms to GAMs.


===================

```r
summary(fit)
```

<img src="./semiparametric_models_RLadies-figure/summary_fit.png" title="plot of chunk unnamed-chunk-20" alt="plot of chunk unnamed-chunk-20" width="510px" style="display: block; margin: auto;" />


====================

```r
library(np)
fhat <- npcdens(motor_UPDRS~DFA,data=dat)
plot(fhat,view="fixed", theta = 310, phi=15,main="")
```

<img src="./semiparametric_models_RLadies-figure/density_plot.png" title="plot of chunk unnamed-chunk-22" alt="plot of chunk unnamed-chunk-22" width="510px" style="display: block; margin: auto;" />

Modeling interactions with splines
=========================

Tests for interactions between non-linear terms is done using `te()`, the tensor product smooths


```r
fit <- gam(motor_UPDRS ~ age + sex + Jitter + 
					 	JitterAbs + JitterRAP + 
					 	JitterDDP + 
					 	NHR + HNR + DFA + s(PPE) + s(RPDE)+
						te(PPE, RPDE), data = dat, method = "REML")
```

Acknowledgments and resources
==============
Definitions and figures in this presentation are taken from Liuhua Peng's material. The Parkinson's Telemonitoring data analysis is a joint work of Gavriel Olshansky and myself.

__Suggested readings__

* Generalized Additive Models, Second Edition. Simon Wood.
* RACINE, J. NONPARAMETRIC AND SEMIPARAMETRIC METHODS IN R
* mgcv package vignette


Feedback time!
===================
R-Ladies Melbourne will soon undergo substantial structural changes. Your feedback helps the committee to decide if #rstats lunch seminars should have a place in the upcoming changes.

Link to the Google Survey : 

https://goo.gl/forms/YgWlrWZU8AlmajN82
