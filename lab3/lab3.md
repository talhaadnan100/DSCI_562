DSCI 562 Lab Assignment 3
================

In this lab assignment, you'll be predicting and making inference/interpretation when data are (1) censored, and (2) ordinal.

Global Rubrics (12%)
--------------------

These rubrics apply to your entire submission.

### Tidy Submission (4%)

rubric={mechanics:4}

To get these mechanics marks, you are expected to:

-   Complete the assignment using R.
-   Submit the assignment by filling in this worksheet with your answers embedded
-   Be sure to follow the [general lab instructions](https://ubc-mds.github.io/resources_pages/general_lab_instructions/).
-   Do not include any code that installs packages (this is not good practice anyway) -- note that this is different from loading packages, which is good!

### Writing (4%)

rubric={writing:4}

To get the marks for this writing component, you should:

-   Use proper English, spelling, and grammar throughout your submission.
-   Be succinct. This means being specific about what you want to communicate, without being superfluous.

### Code Quality (4%)

rubric={quality:4}

These marks apply to the collective code you write in this assignment.

Exercise 1: Survival Analysis (59%)
-----------------------------------

For this exercise, we'll use the `lung` dataset that ships with the `survival` R package. Consider the following variables:

-   Response variable: survival `time` (with censor status in `status`)
-   Categorical predictor: `ph.ecog` (remove the single instance of 3 and NA)
-   Numeric predictor: A numeric variable of your choice

### 1.1 Univariate Estimation: Survival Function (12%)

rubric={viz:6, accuracy:6}

Estimate the survival function using the Kaplan-Meier estimator. Then, estimate the survival function after making a Weibull distributional assumption. Display both estimates as a plot.

Hint: See the bottom of the `?survreg` documentation to convert the intercept and scale parameters to Weibull's shape and scale parameters.

### 1.2 Univariate Estimation: Mean and Median (12%)

rubric={reasoning:6, accuracy:6}

Does your Kaplan-Meier estimate of the survival function allow for estimation of the mean? What about quantiles, are there any quantiles that cannot be estimated using this survival function? Why or why not?

Estimate the median and mean using both estimates of the survival function. If you need to calculated a restricted mean, indicate the restriction. Hint: check out [Wikipedia's page on the Weibull distribution](https://en.wikipedia.org/wiki/Weibull_distribution) for the mean of a Weibull distribution, noting that the Gamma function in R is `gamma()`.

### 1.3 Univariate Estimation: Ignoring Censoring (6%)

rubric={reasoning:6}

Estimate the mean and median, this time ignoring the censoring (don't bother with the parametric assumption). How do the estimates compare? How would you expect them to compare, and why?

### 1.4 Plot (6%)

rubric={viz:6}

Plot the survival times along with the two predictors. The response should be mapped to the vertical axis. Be sure to indicate whether or not an observation is censored.

### 1.5 Regression with Proportional Hazards (12%)

rubric={reasoning:6, accuracy:6}

Fit a Proportional Hazards model to survival time using your predictors.

Which predictors appear to have an influence on the response under a 0.05 significance level? Don't concern yourself with the issue of multiple testing.

Choose one regression coefficient to interpret. Ideally, it should be "significant", but for the purpose of this exercise, it doesn't have to be. Be sure to also indicate its estimate.

### 1.6 Prediction (11%)

rubric={accuracy:11}

Use your proportional hazards regression model to obtain an estimate of the survival function associated with one of the patients in the dataset. Of the (hypothetical) population of patients having this same calorie intake and ECOG score, what is the 0.8-quantile?

### 1.7 Probabilistic Forecast of the Density (Optional)

rubric={accuracy:1}

For the same hypothetical population in Exercise 1.6, plot a density estimate. Hint: you could generate lots of data using the survival function, then use `ggplot2::geom_density()`.

### 1.8 Model Function (Optional)

rubric={accuracy:1}

Reproduce your plot from Exercise 1.4, this time adding a model function of your choice (mean? median? some other quantile?). The model function should exist at least somewhere within the span of the predictor space.

Exercise 2: Ordinal Regression (29%)
------------------------------------

For this exercise, we'll use the happiness survey data collected by the [GSS at NORC](http://gss.norc.org/Get-The-Data). Consider the following variables:

-   Response variable: `happiness`
    -   Note that `Not too happy` &lt; `Pretty happy` &lt; `Very happy`.
-   Numeric predictor: `hours`
-   Categorical predictor: a categorical variable of your choice.

### 2.1 Plot (6%)

rubric={viz:6}

Plot the data (only include the three variables). The response should be mapped to the vertical axis.

### 2.2 Regression using Proportional Odds (13%)

rubric={reasoning:6, accuracy:7}

Fit a Proportional Odds model, with no interaction term.

Choose one regression coefficient to interpret. Be sure to also indicate its estimate.

### 2.3 Regression assuming numeric (Optional)

rubric={reasoning:1}

Repeat the regression exercise, this time using linear regression (assuming that the response levels are actually numeric). In addition, state two negative consequences of using a linear regression model with these data. Are these consequences dire?

### 2.4 Prediction (10%)

rubric={accuracy:10}

Choose one survey respondent. Using your proportional odds model, make both a probabilistic forecast (displayed as a plot) and a modal (i.e. the mode) prediction.

### 2.5 Model Function (Optional)

rubric={accuracy:1}

Plot the model functions for both linear regression and the proportional odds model. No points will be awarded if you only plot the linear regression model.
