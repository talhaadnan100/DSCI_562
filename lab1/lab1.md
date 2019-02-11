DSCI 562 Lab 1: Parametric Assumptions and GLM
================

Global Rubrics (20%)
====================

These rubrics apply to your entire submission.

Tidy Submission (4%)
--------------------

rubric={mechanics:4}

To get these mechanics marks, you are expected to:

-   Complete the assignment using R.
-   Submit the assignment by filling in this worksheet with your answers embedded
-   Be sure to follow the [general lab instructions](https://ubc-mds.github.io/resources_pages/general_lab_instructions/).
-   Do not include any code that installs packages (this is not good practice anyway) -- note that this is different from loading packages, which is good!

Writing (4%)
------------

rubric={writing:4}

To get the marks for this writing component, you should:

-   Use proper English, spelling, and grammar throughout your submission.
-   Be succinct. This means being specific about what you want to communicate, without being superfluous.

Vis (4%)
--------

rubric={viz:4}

These marks apply to the collective visuals you make in this assignment.

Code (8%)
---------

rubric={quality:4, accuracy:4}

These marks apply to the collective code you write in this assignment.

Exercise 1 (55%)
================

Titanic data: predicting survival from `Fare` and `Sex`.

1.0 (5%)
--------

rubric={reasoning:5}

Make a plot examining how the covariates are related to the response. Comment on what you observe about the relationship of `Fare` and `Sex` on `Survived`.

1.1 Linear Regression (14%)
---------------------------

rubric={reasoning:14}

Fit a linear regression model, and plot the model function overtop of the data. Interpret the slope parameters. What probabilistic quantity does this model function represent an estimate of, and of what random variable?

One consequence of using this linear regression model is that the model function sometimes evaluates to numbers that don't make sense. How often does this happen on the training data? What problems would you have to put up with if you were to use this model in practice? When answering, be sure to also comment on how often this problem would happen, and roughly where on the predictor space the problem would occur.

1.2 Binomial Regression (18%)
-----------------------------

rubric={reasoning:18}

Adjust the assumptions of the linear regression model so that the model function always evaluates to a valid number, and so that the parameters carry an interpretation. Report the model function equation that you're assuming. Comment on whether you chose to transform the response or the model function, and why. Then, add a distributional assumption, being clear to indicate what random variable you are making an assumption on. Now fit the model using MLE. Comment on the advantage we get by estimating parameters using MLE under the distributional assumption, in comparison to *not* making the distributional assumption and fitting using least squares. Plot the model function overtop of the data. Interpret the model parameters now.

1.3 Predicting (5%)
-------------------

rubric={reasoning:5}

Evaluate the model function for a new individual of your choice. Compare this to the null model. What conclusion can you draw from this comparison?

1.4 (Optional)
--------------

rubric={reasoning:1}

Fit the model using least squares, ignoring your distributional assumption. Plot the model function overtop of the data. Is it quite different from the MLE fit?

1.5 (Optional)
--------------

rubric={reasoning:2}

Use bootstrapping to get many bootstrap estimates under both least squares (LS) and MLE. Plot the collection of bootstrap model functions for both LS and MLE, in separate panels (you'll probably need to use lots of alpha transparency), to give you a sense of the variability of the model function fits. Also, compare the bootstrap sampling distributions under both LS and MLE of the slope parameter (the coefficient of your predictor) by plotting kernel density estimates of both. Use these plots as evidence to comment on which estimator is better (LS or MLE).

1.6 (13%)
---------

rubric={reasoning:13}

Fit a local regression (kNN or loess) to the data, and plot the model function on top of the data. You can just choose the tuning parameters by eye (instead of more rigorous techniques like cross validation). Which model performs better? Just use the training data to calculate error. Even if the local method is better, what advantage does a parametric model hold over this local model?

Exercise 2 (25%)
================

We will use the Baseball dataset `Teams` available in the `Lahman` package in R. We will model the relationship between total number of runs scored by each team (`R`, response variable) to the total number of walks (`BB`) and the total number of hits (`H`) (covariates).

2.0 Exploring the data (5%)
---------------------------

rubric={reasoning:5}

Create a visualization to summarise the relationship between total number of runs scored to the total number of walks and the total number of hits. Comment on the shape of the relationships.

2.1 Model choice (5%)
---------------------

rubric={reasoning:5}

In what way(s) would linear regression be inappropriate for these data, if at all?

2.2 Poisson regression fit (10%)
--------------------------------

rubric={reasoning:10}

Fit a Poisson regression model with a log link function. Provide an interpretation of the regression coefficients (not the intercept parameter).

2.3 Model fit (5%)
------------------

rubric={reasoning:5}

Make a residual plot of your Poisson regression model, and comment on the fit.

Exercise 3: Optional Exercises
==============================

3.1 Overdispersion (underdispersion) (Optional)
-----------------------------------------------

rubric={reasoning:1}

-   Test for over/under dispersion. Is there over/under dispersion?
-   Estimate the overdispersion/underdispersion parameter. Report the estimated value.
-   Fit negative binomial regression model on the data with the same variables. Comment on the differences/similarities.

3.2 Likelihood (Optional)
-------------------------

rubric={reasoning:1}

Derive a mathematical formula for the negative log likelihood function for either the binomial-logit or binomial-probit models, beginning from the pmf's of the observations. Be sure to be clear what variable the function is of.
