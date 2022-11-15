# Setting up

The idea of this practical is to go through the basics of multiple
regression analysis, which you should know from previous courses.

Before diving into the core of the lecture, remember that you should
always start your R session by arranging the workspace

    # Clean the environment 
    rm(list = ls())

    # Setting the working directory
    setwd("C:/Users/Startklar/OneDrive - Vrije Universiteit Amsterdam/Measurement Models in Quantitative Research/3 - Practicals/Meas_Models")

    # Installing  and loading the required packages
    library(ggplot2)
    library(visreg)
    library(MASS)

# Regression

Now, we can go back to the main topic. The main idea behind regression
is that a dependent variable (DV) can be modeled as a combination of a
single or multiple independent variables(IV). For example, we could
model a variable *Y*<sub>*i*</sub> as the weighted sum of *k*
independent variables, denoted by *X*<sub>*i*</sub>, and an error term
*ε*<sub>*i*</sub>. Note that in this notation *i* refers to an
individual. Thus, we have:

## Assumptions

### 1 - Normality of *y*<sub>*i*</sub> - and hence of *ε*<sub>*i*</sub>

### 2 - Exogeneity - *E*(*ε*<sub>*i*</sub>|*x*<sub>*i*</sub>) = 0

# Example - Birth weight

    data(birthwt, package = "MASS")

     # Let's check what this data has
    head(birthwt)

    ##    low age lwt race smoke ptl ht ui ftv  bwt
    ## 85   0  19 182    2     0   0  0  1   0 2523
    ## 86   0  33 155    3     0   0  0  0   3 2551
    ## 87   0  20 105    1     1   0  0  0   1 2557
    ## 88   0  21 108    1     1   0  0  1   2 2594
    ## 89   0  18 107    1     1   0  0  1   0 2600
    ## 91   0  21 124    3     0   0  0  0   0 2622

    ?birthwt

## Simple regression - Continuous IV

Our goal with this data will be to estimate children weight at birth. To
do so, we can first just employ age as an IV and see our results.
Beforehand though, let us see a scatter with these two variables

![](Script_L2_files/figure-markdown_strict/simpreg_cont_plots-1.png)![](Script_L2_files/figure-markdown_strict/simpreg_cont_plots-2.png)![](Script_L2_files/figure-markdown_strict/simpreg_cont_plots-3.png)

    ## 
    ## Call:
    ## lm(formula = bwt ~ age, data = birthwt)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -2294.78  -517.63    10.51   530.80  1774.92 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  2655.74     238.86   11.12   <2e-16 ***
    ## age            12.43      10.02    1.24    0.216    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 728.2 on 187 degrees of freedom
    ## Multiple R-squared:  0.008157,   Adjusted R-squared:  0.002853 
    ## F-statistic: 1.538 on 1 and 187 DF,  p-value: 0.2165

## Simple regression - Dummy IV

The interpretation of the regression results vary considerably when we
are dealing with IV’s that are dummies. We can see this by regressing
the birth weight against the dummy variables that indicates whether the
mother smoked (0 = Didn’t Smoke, 1 = Smoked).You’ll frequently encounter
dummy variables since they are a common way of representing the
presence/absence of a trait.

    ## 
    ## Call:
    ## lm(formula = bwt ~ smoke, data = birthwt)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -2062.9  -475.9    34.3   545.1  1934.3 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  3055.70      66.93  45.653  < 2e-16 ***
    ## smoke        -283.78     106.97  -2.653  0.00867 ** 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 717.8 on 187 degrees of freedom
    ## Multiple R-squared:  0.03627,    Adjusted R-squared:  0.03112 
    ## F-statistic: 7.038 on 1 and 187 DF,  p-value: 0.008667
