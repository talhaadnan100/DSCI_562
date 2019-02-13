
<!-- rnb-text-begin -->

---
title: "Horeshoe crab case study: models under various assumptions"
output: html_notebook
editor_options: 
  chunk_output_type: inline
---

Let's continue working with the horseshoe crab data from last time. Today, we'll fit three models under different assumptions, evaluating their usefulness.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuc3VwcHJlc3NQYWNrYWdlU3RhcnR1cE1lc3NhZ2VzKGxpYnJhcnkodGlkeXZlcnNlKSlcbmBgYCJ9 -->

```r
suppressPackageStartupMessages(library(tidyverse))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoicGFja2FnZSDjpLzjuLF0aWJibGXjpLzjuLIgd2FzIGJ1aWx0IHVuZGVyIFIgdmVyc2lvbiAzLjUuMnBhY2thZ2Ug46S847ixcmVhZHLjpLzjuLIgd2FzIGJ1aWx0IHVuZGVyIFIgdmVyc2lvbiAzLjUuMnBhY2thZ2Ug46S847ixcHVycnLjpLzjuLIgd2FzIGJ1aWx0IHVuZGVyIFIgdmVyc2lvbiAzLjUuMlxuIn0= -->

```
package <U+393C><U+3E31>tibble<U+393C><U+3E32> was built under R version 3.5.2package <U+393C><U+3E31>readr<U+393C><U+3E32> was built under R version 3.5.2package <U+393C><U+3E31>purrr<U+393C><U+3E32> was built under R version 3.5.2
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuY3JhYiA8LSByZWFkX3RhYmxlKFwiaHR0cHM6Ly9uZXdvbmxpbmVjb3Vyc2VzLnNjaWVuY2UucHN1LmVkdS9zdGF0NTA0L3NpdGVzL29ubGluZWNvdXJzZXMuc2NpZW5jZS5wc3UuZWR1LnN0YXQ1MDQvZmlsZXMvbGVzc29uMDcvY3JhYi9pbmRleC50eHRcIiwgY29sX25hbWVzID0gRkFMU0UpICU+JSBcbiAgc2VsZWN0KC0xKSAlPiUgXG4gIHNldE5hbWVzKGMoXCJjb2xvdXJcIixcInNwaW5lXCIsXCJ3aWR0aFwiLFwid2VpZ2h0XCIsXCJuX21hbGVcIikpICU+JSBcbiAgbXV0YXRlKGNvbG91ciA9IGZhY3Rvcihjb2xvdXIpLFxuICAgICAgICAgc3BpbmUgID0gZmFjdG9yKHNwaW5lKSlcbmBgYCJ9 -->

```r
crab <- read_table("https://newonlinecourses.science.psu.edu/stat504/sites/onlinecourses.science.psu.edu.stat504/files/lesson07/crab/index.txt", col_names = FALSE) %>% 
  select(-1) %>% 
  setNames(c("colour","spine","width","weight","n_male")) %>% 
  mutate(colour = factor(colour),
         spine  = factor(spine))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiUGFyc2VkIHdpdGggY29sdW1uIHNwZWNpZmljYXRpb246XG5jb2xzKFxuICBYMSA9IFx1MDAxYlszMm1jb2xfZG91YmxlKClcdTAwMWJbMzltLFxuICBYMiA9IFx1MDAxYlszMm1jb2xfZG91YmxlKClcdTAwMWJbMzltLFxuICBYMyA9IFx1MDAxYlszMm1jb2xfZG91YmxlKClcdTAwMWJbMzltLFxuICBYNCA9IFx1MDAxYlszMm1jb2xfZG91YmxlKClcdTAwMWJbMzltLFxuICBYNSA9IFx1MDAxYlszMm1jb2xfZG91YmxlKClcdTAwMWJbMzltLFxuICBYNiA9IFx1MDAxYlszMm1jb2xfZG91YmxlKClcdTAwMWJbMzltXG4pXG4ifQ== -->

```
Parsed with column specification:
cols(
  X1 = [32mcol_double()[39m,
  X2 = [32mcol_double()[39m,
  X3 = [32mcol_double()[39m,
  X4 = [32mcol_double()[39m,
  X5 = [32mcol_double()[39m,
  X6 = [32mcol_double()[39m
)
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxua25pdHI6OmthYmxlKGhlYWQoY3JhYikpXG5gYGAifQ== -->

```r
knitr::kable(head(crab))
```

<!-- rnb-source-end -->
preserve1a7993834d719d7b

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Case study: how do features of nesting female horseshoe crabs influence the number of males found nearby? Let's see how carapace width influences the mean number of males nearby.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucCA8LSBnZ3Bsb3QoY3JhYiwgYWVzKHdpZHRoLCBuX21hbGUpKSArIFxuICBnZW9tX3BvaW50KGFscGhhPTAuMjUpICtcbiAgbGFicyh4ID0gXCJDYXJhcGFjZSBXaWR0aFwiLCBcbiAgICAgICB5ID0gXCJOby4gbWFsZXNcXG5uZWFyYnlcIikgK1xuICB0aGVtZV9idygpICtcbiAgdGhlbWUoYXhpcy50aXRsZS55ID0gZWxlbWVudF90ZXh0KGFuZ2xlPTAsIHZqdXN0PTAuNSkpXG5wbG90bHk6OmdncGxvdGx5KHApXG5gYGAifQ== -->

```r
p <- ggplot(crab, aes(width, n_male)) + 
  geom_point(alpha=0.25) +
  labs(x = "Carapace Width", 
       y = "No. males\nnearby") +
  theme_bw() +
  theme(axis.title.y = element_text(angle=0, vjust=0.5))
plotly::ggplotly(p)
```

<!-- rnb-source-end -->
preserve3e677572dde25cf8

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Data source: [H. Jane Brockmann's 1996 paper](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1439-0310.1996.tb01099.x); found online [here](https://newonlinecourses.science.psu.edu/stat504/sites/onlinecourses.science.psu.edu.stat504/files/lesson07/crab/index.txt); another regression demo with this data is found [here](https://newonlinecourses.science.psu.edu/stat504/node/169/).


## Approach 1: Estimate regression curve / model function locally

Optimize the loess fit by eye. Just modify span, to keep things simple.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ3JpZCA8LSBzZXEobWluKGNyYWIkd2lkdGgpLCBtYXgoY3JhYiR3aWR0aCksIGxlbmd0aC5vdXQ9MTAwMClcbmdyaWRfZGYgPC0gdGliYmxlKHdpZHRoID0gZ3JpZClcbm1vZGVsMSA8LSBsb2VzcyhuX21hbGUgfiB3aWR0aCwgZGF0YT1jcmFiLCBkZWdyZWUgPSAyLCBzcGFuID0gMC41KVxuZ3JpZF9kZiAlPiUgXG4gIG11dGF0ZSguLCB5aGF0ID0gcHJlZGljdChtb2RlbDEsIC4pKSAlPiUgXG4gIGdncGxvdChhZXMod2lkdGgsIHloYXQpKSArXG4gIGdlb21fbGluZShjb2xvdXI9XCJibHVlXCIpICtcbiAgZ2VvbV9wb2ludChkYXRhPWNyYWIsIG1hcHBpbmc9YWVzKHdpZHRoLCBuX21hbGUpLCBhbHBoYT0wLjI1KVxuYGBgIn0= -->

```r
grid <- seq(min(crab$width), max(crab$width), length.out=1000)
grid_df <- tibble(width = grid)
model1 <- loess(n_male ~ width, data=crab, degree = 2, span = 0.5)
grid_df %>% 
  mutate(., yhat = predict(model1, .)) %>% 
  ggplot(aes(width, yhat)) +
  geom_line(colour="blue") +
  geom_point(data=crab, mapping=aes(width, n_male), alpha=0.25)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0LCJzaXplX2JlaGF2aW9yIjoxLCJ3aWR0aCI6Nn0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


What's the error of this model? Training error is fine.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucmVzaWQxIDwtIGNyYWIkbl9tYWxlIC0gcHJlZGljdChtb2RlbDEpXG4oZXJyb3IxIDwtIG1lYW4ocmVzaWQxXjIpKVxuYGBgIn0= -->

```r
resid1 <- crab$n_male - predict(model1)
(error1 <- mean(resid1^2))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIDguNjQ4NTJcbiJ9 -->

```
[1] 8.64852
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


How well does this model answer our original question?

**Comment:** It is a good predictive model, but not an excellent interpretive model.

## Approach 2: Linear Regression

### Fit a linear regression model

Fit a linear regression model. What's the error?


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubW9kZWwyIDwtIGxtKG5fbWFsZSB+IHdpZHRoLCBkYXRhPWNyYWIpXG5nZ3Bsb3QoY3JhYiwgYWVzKHdpZHRoLCBuX21hbGUpKSArXG4gICAgZ2VvbV9wb2ludChhbHBoYT0wLjI1KSArXG4gICAgZ2VvbV9zbW9vdGgobWV0aG9kPVwibG1cIiwgc2U9RkFMU0UpXG5gYGAifQ== -->

```r
model2 <- lm(n_male ~ width, data=crab)
ggplot(crab, aes(width, n_male)) +
    geom_point(alpha=0.25) +
    geom_smooth(method="lm", se=FALSE)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJjb25kaXRpb25zIjpbXSwiaGVpZ2h0Ijo0MzIuNjMyOSwic2l6ZV9iZWhhdmlvciI6MCwid2lkdGgiOjcwMH0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucmVzaWQyIDwtIGNyYWIkbl9tYWxlIC0gcHJlZGljdChtb2RlbDIpXG4oZXJyb3IyIDwtIG1lYW4ocmVzaWQyXjIpKVxuYGBgIn0= -->

```r
resid2 <- crab$n_male - predict(model2)
(error2 <- mean(resid2^2))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIDguNzE2MjUyXG4ifQ== -->

```
[1] 8.716252
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


How well does this model answer our original question? Do you see a potential problem with this model? Are any assumptions of linear regression not true? Brainstorm ideas for how to deal with the problems.

## New approaches

Let's talk about an alternative approach called _Generalized Linear Models_ (GLM). Topics:

- Appropriate transformation: on Y? On E(Y|X)? Link function definitions.
- Interpretation of parameters under log and logit links.
- Fitting the model function: Is LS "valid"? Can we do better? 
    - The two types of parametric assumptions, their risk, and their value.
    - Review of MLE?
    - Nomenclature: Poisson regression; Binomial/Bernoulli/Logistic regression.

## Approach 3: Link Function

Fit a GLM. Plot using `ggplot2`, making use of the `method.args` argument of `geom_smooth()`. What's the error?


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuKGVycm9yMyA8LSBtZWFuKHJlc2lkM14yKSlcblxuYGBgIn0= -->

```r
(error3 <- mean(resid3^2))

```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIDguODg2MzA0XG4ifQ== -->

```
[1] 8.886304
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Bonus: generate some data under the fitted model. How does it compare?

## Approach 4: Scientifically motivated model function?

There's probably none here, but if there was, what then?

<!-- rnb-text-end -->

