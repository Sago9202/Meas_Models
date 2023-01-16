Session 3: Factor Analysis
================
Laura Eberlein, Santiago Gómez-Echeverry & Dimitris Pavlopoulos
2023-01-16

- <a href="#factor-analysis" id="toc-factor-analysis">Factor Analysis</a>
- <a href="#example---spss-anxiety"
  id="toc-example---spss-anxiety">Example - SPSS Anxiety</a>
- <a href="#correlation-matrix" id="toc-correlation-matrix">Correlation
  matrix</a>

Before diving into the core of the lecture, remember that you should
always start your R session by arranging the work space.

``` r
rm(list = ls()) # Clean the environment 
library(lavaan)
library(psych)
library(haven) # To import the data from SPSS
library(memisc) # To make a fast description of the data
library(corrplot) 
options(digits = 3) # We only want to see three numbers after the decimal point
```

# Factor Analysis

Let us start our factor analyses with the simplest example possible: a
one factor model. This model would imply that the items that we observe
can be expressed as:

$$
  X_{mi} = \mu_{m} + \lambda_{m}\theta_{i} + \epsilon_{mi}
$$

Upon close inspection you will notice that this model is quite similar
to the regression that we saw in the previous session. In fact, factor
analysis is equivalent to a linear regression with unobserved
predictor(s). However, since we are dealing with an unobserved variable,
which we call factor, and since now we are using a different sub-index
we will use a different notation. In this case we will have that:

- $X_{mi}$: Score of person $i$ on item $j$.
- $\mu_{m}$: Intercept of the item $m$. This is the value of the item if
  the factor takes the value of zero, and usually matches the mean item
  score.
- $\lambda_{m}$: Factor loading of item $j$; this term quantifies the
  extent to which the observed variable relates to a given factor.
- $\theta_{i}$: Score of the person $i$ in the unobserved factor. Notice
  that as we said, we are using Greek terms to refer to unobserved
  elements in our equations.
- $\epsilon_{mi}$: Residual variance of the observed item $X_{m}$ for
  individual $i$. In other words, this term shows the part of $X_{mi}$
  that is not explained by the common factor $\theta_{i}$.

In addition to the main equation, it is also good to think about the
variances. We can express the variance of the observed items as the sum
between the shared variance due to the common unobserved factor
(commonality), and the unique variance of each item (uniqueness). The
latter contains two parts that we cannot truly untangle: the
item-specific variance and the measurement error. We can express the
ideas expressed in this paragraph with the following equation:

$$
  \sigma^{2}_{X_{m}} = \lambda^{2}_{m}\sigma^{2}_{\theta}+\sigma^{2}_{\varepsilon_{m}}
$$ Or equivalently

$$
  Var(X_{m}) = \lambda_{m}^{2}Var(\theta) + Var(\epsilon_{m})
$$

It is good to keep in mind that we assume in our model that once
controlled for the unobserved factor, there shouldn’t be any
relationship between our indicators.

On the other hand, just as in regression analysis, we have to estimate
the intercepts, the slopes and the residuals of the equation. However,
there is are some additional unknowns in this model and all of them stem
from the unobserved factor. Given the latter we must make an
identification assumption to be able to run our model. The most frequent
options for identification are:

- $\sigma^{2}_{\theta}$: Factor variance set equal to unity.
- $\lambda_{1}=1$: First loading set equal to 1 (marker variable)
- $\mu_{\theta} = 0$: Factor mean set equal to zero.

# Example - SPSS Anxiety

In this practical we will explore data on the anxiety that social
science students experience when faced with a statistics course (much
like this). You can see a bit more about this data in here. Now, let’s
load the data, check how many observations we have and check the first
cases.

``` r
setwd("C:/Users/Startklar/OneDrive - Vrije Universiteit Amsterdam/Measurement Models in Quantitative Research/3 - Practicals/Week 2 - Factor Analysis")

anxiety <- read_sav("SAQ8.sav")
dim(anxiety) # We have 2,571 obs. with 8 variables
```

    ## [1] 2571    8

``` r
head(anxiety)
```

    ## # A tibble: 6 × 8
    ##   q01                q02         q03     q04     q05     q06     q07     q08    
    ##   <dbl+lbl>          <dbl+lbl>   <dbl+l> <dbl+l> <dbl+l> <dbl+l> <dbl+l> <dbl+l>
    ## 1 2 [Agree]          1 [Strongl… 4 [Dis… 2 [Agr… 2 [Agr… 2 [Agr… 3 [Nei… 1 [Str…
    ## 2 1 [Strongly agree] 1 [Strongl… 4 [Dis… 3 [Nei… 2 [Agr… 2 [Agr… 2 [Agr… 2 [Agr…
    ## 3 2 [Agree]          3 [Neither] 2 [Agr… 2 [Agr… 4 [Dis… 1 [Str… 2 [Agr… 2 [Agr…
    ## 4 3 [Neither]        1 [Strongl… 1 [Str… 4 [Dis… 3 [Nei… 3 [Nei… 4 [Dis… 2 [Agr…
    ## 5 2 [Agree]          1 [Strongl… 3 [Nei… 2 [Agr… 2 [Agr… 3 [Nei… 3 [Nei… 2 [Agr…
    ## 6 2 [Agree]          1 [Strongl… 3 [Nei… 2 [Agr… 4 [Dis… 4 [Dis… 4 [Dis… 2 [Agr…

As we see, luckily this data has some labels so we can easily see what
the variables are about and what are the response categories. Let’s
check which items we have and let us get some descriptive statistics.

``` r
# Labels of the variables
description(anxiety)
```

    ## 
    ##  q01 'Statistics makes me cry'                                              
    ##  q02 'My friends will think I'm stupid for not being able to cope with SPSS'
    ##  q03 'Standard deviations excite me'                                        
    ##  q04 'I dream that Pearson is attacking me with correlation coefficients'   
    ##  q05 'I don't understand statistics'                                        
    ##  q06 'I have little experience of computers'                                
    ##  q07 'All computers hate me'                                                
    ##  q08 'I have never been good at mathematics'

``` r
# Descriptive Statistics
describe(anxiety)
```

    ##     vars    n mean   sd median trimmed  mad min max range skew kurtosis   se
    ## q01    1 2571 2.37 0.83      2    2.34 0.00   1   5     4 0.65     0.61 0.02
    ## q02    2 2571 1.62 0.85      1    1.46 0.00   1   5     4 1.49     2.04 0.02
    ## q03    3 2571 2.59 1.08      3    2.57 1.48   1   5     4 0.09    -0.78 0.02
    ## q04    4 2571 2.79 0.95      3    2.74 1.48   1   5     4 0.39    -0.29 0.02
    ## q05    5 2571 2.72 0.96      3    2.68 1.48   1   5     4 0.46    -0.44 0.02
    ## q06    6 2571 2.23 1.12      2    2.09 1.48   1   5     4 0.93     0.15 0.02
    ## q07    7 2571 2.92 1.10      3    2.89 1.48   1   5     4 0.20    -0.85 0.02
    ## q08    8 2571 2.24 0.87      2    2.15 0.00   1   5     4 1.05     1.48 0.02

Now that we know what the data contains, let us start with our analyses.

# Correlation matrix

EFA and CFA, like many other models that are embedded in Structural
Equation Modeling (SEM) mainly require the correlation matrix to work
with. Remember that the optimization method by which these models is
achieved is by minimizing the difference between the observed
correlation matrix and the one that is implied by the model. Thus, let’s
see this matrix with a bit more detail

``` r
# Covariance matrix
cov_mat <- cov(anxiety)
cov_mat
```

    ##         q01     q02    q03     q04    q05     q06    q07     q08
    ## q01  0.6856 -0.0696 -0.300  0.3423  0.321  0.2014  0.279  0.2390
    ## q02 -0.0696  0.7243  0.291 -0.0903 -0.098 -0.0709 -0.149 -0.0369
    ## q03 -0.2997  0.2913  1.156 -0.3880 -0.322 -0.2735 -0.453 -0.2426
    ## q04  0.3423 -0.0903 -0.388  0.8997  0.367  0.2961  0.427  0.2892
    ## q05  0.3215 -0.0980 -0.322  0.3666  0.931  0.2787  0.361  0.2261
    ## q06  0.2014 -0.0709 -0.273  0.2961  0.279  1.2589  0.635  0.2182
    ## q07  0.2787 -0.1493 -0.453  0.4273  0.361  0.6352  1.215  0.2862
    ## q08  0.2390 -0.0369 -0.243  0.2892  0.226  0.2182  0.286  0.7614

``` r
# Correlation matrix
cor_mat <- cor(anxiety)
cor_mat
```

    ##         q01     q02    q03    q04    q05     q06    q07     q08
    ## q01  1.0000 -0.0987 -0.337  0.436  0.402  0.2167  0.305  0.3307
    ## q02 -0.0987  1.0000  0.318 -0.112 -0.119 -0.0742 -0.159 -0.0496
    ## q03 -0.3366  0.3184  1.000 -0.380 -0.310 -0.2267 -0.382 -0.2586
    ## q04  0.4359 -0.1119 -0.380  1.000  0.401  0.2782  0.409  0.3494
    ## q05  0.4024 -0.1193 -0.310  0.401  1.000  0.2575  0.339  0.2686
    ## q06  0.2167 -0.0742 -0.227  0.278  0.257  1.0000  0.514  0.2228
    ## q07  0.3054 -0.1592 -0.382  0.409  0.339  0.5136  1.000  0.2975
    ## q08  0.3307 -0.0496 -0.259  0.349  0.269  0.2228  0.297  1.0000

``` r
# Correlation Plot
corrplot(cor_mat)
```

![](Script_L3_files/figure-gfm/cov%20and%20corr-1.png)<!-- -->

Great! Now we know how is the relationship between our variables. Still,
we haven’t tested if this relationship is statistically significant.
Remember that this is relevant since we want our variables to be
strongly related to conduct a factor analysis. To do these significance
test, let us perform some indexing (as we saw in the first class), and a
very simple loop.

``` r
# Remember subsetting?
anxiety[,which(colnames(anxiety)==c("q01", "q02"))]
```

    ## # A tibble: 2,571 × 2
    ##    q01                q02               
    ##    <dbl+lbl>          <dbl+lbl>         
    ##  1 2 [Agree]          1 [Strongly agree]
    ##  2 1 [Strongly agree] 1 [Strongly agree]
    ##  3 2 [Agree]          3 [Neither]       
    ##  4 3 [Neither]        1 [Strongly agree]
    ##  5 2 [Agree]          1 [Strongly agree]
    ##  6 2 [Agree]          1 [Strongly agree]
    ##  7 2 [Agree]          3 [Neither]       
    ##  8 2 [Agree]          2 [Agree]         
    ##  9 3 [Neither]        3 [Neither]       
    ## 10 2 [Agree]          4 [Disagree]      
    ## # … with 2,561 more rows

``` r
anxiety[,c(1,2)]
```

    ## # A tibble: 2,571 × 2
    ##    q01                q02               
    ##    <dbl+lbl>          <dbl+lbl>         
    ##  1 2 [Agree]          1 [Strongly agree]
    ##  2 1 [Strongly agree] 1 [Strongly agree]
    ##  3 2 [Agree]          3 [Neither]       
    ##  4 3 [Neither]        1 [Strongly agree]
    ##  5 2 [Agree]          1 [Strongly agree]
    ##  6 2 [Agree]          1 [Strongly agree]
    ##  7 2 [Agree]          3 [Neither]       
    ##  8 2 [Agree]          2 [Agree]         
    ##  9 3 [Neither]        3 [Neither]       
    ## 10 2 [Agree]          4 [Disagree]      
    ## # … with 2,561 more rows

``` r
anxiety <- as.matrix(anxiety)

for (i in 1:3){
  for (j in 1:3){
   if (i!=j){
    print(paste0("Test Q", i,",Q", j))
    print(cor.test(anxiety[,i], anxiety[,j]))  
   }
   if (i==j){
   }
 }
}
```

    ## [1] "Test Q1,Q2"
    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  anxiety[, i] and anxiety[, j]
    ## t = -5, df = 2569, p-value = 5e-07
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.1369 -0.0603
    ## sample estimates:
    ##     cor 
    ## -0.0987 
    ## 
    ## [1] "Test Q1,Q3"
    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  anxiety[, i] and anxiety[, j]
    ## t = -18, df = 2569, p-value <2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.370 -0.302
    ## sample estimates:
    ##    cor 
    ## -0.337 
    ## 
    ## [1] "Test Q2,Q1"
    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  anxiety[, i] and anxiety[, j]
    ## t = -5, df = 2569, p-value = 5e-07
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.1369 -0.0603
    ## sample estimates:
    ##     cor 
    ## -0.0987 
    ## 
    ## [1] "Test Q2,Q3"
    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  anxiety[, i] and anxiety[, j]
    ## t = 17, df = 2569, p-value <2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.283 0.353
    ## sample estimates:
    ##   cor 
    ## 0.318 
    ## 
    ## [1] "Test Q3,Q1"
    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  anxiety[, i] and anxiety[, j]
    ## t = -18, df = 2569, p-value <2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.370 -0.302
    ## sample estimates:
    ##    cor 
    ## -0.337 
    ## 
    ## [1] "Test Q3,Q2"
    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  anxiety[, i] and anxiety[, j]
    ## t = 17, df = 2569, p-value <2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.283 0.353
    ## sample estimates:
    ##   cor 
    ## 0.318

Keep in mind that loops can very helpful to perform repetitive
processes, and they are at the core of any programming languages. In the
case of *R*, there are also some additional functions that perform
diverse sorts of loops for some particular situations. For those who are
more interested on this, you can check the function *apply* and its
variations.

We saw that we shall also perform other tests to confirm that we can
perform a factor analysis. Among these, we had the Kaiser-Meyer-Olkin
criterion and the Barlett’s test:

``` r
# Kaiser Meyer Olkin
KMO(anxiety)
```

    ## Kaiser-Meyer-Olkin factor adequacy
    ## Call: KMO(r = anxiety)
    ## Overall MSA =  0.82
    ## MSA for each item = 
    ##  q01  q02  q03  q04  q05  q06  q07  q08 
    ## 0.84 0.68 0.82 0.85 0.87 0.75 0.78 0.88

``` r
# Barlett's test
cortest.bartlett(anxiety)
```

    ## $chisq
    ## [1] 4157
    ## 
    ## $p.value
    ## [1] 0
    ## 
    ## $df
    ## [1] 28

According to this results, we do have a strong justification for
conducting a Factor Analysis. Now that we have checked the assumptions,
we can proceed with the EFA.

Keep in mind that to perform this analysis we will use the *efa()*
function embedded in the *lavaan* package. However, you could
alternatively use other functions such as *fa()*. Notice that the
arguments of this function include: the data, the name of the observed
variables, the number of factors, the rotation, and the maximization
method employed to deal with the missing values.

``` r
fit_1 <- efa(data = anxiety, 
             ov.names = paste0("q0",1:8),
             nfactor = 1:4,
             rotation = "geomin",
             missing = "fiml")

# The result we have is a list
class(fit_1)
```

    ## [1] "efaList" "list"

Remember that the whole idea of the rotation is that we can easily
interpret the obstained factors and factor loadings and that we define a
relationship between the factors (orthogonal between oblique). The
results from all the different analyses are within this list and we can
access them simply by indexing, and use them to perform further
procedures. Let us for instance, explore the results of the model with
three factors first. We can go further and see the factor loadings from
all the different model specifications or ask R to give us a detailed
summary of the results of a specific model.

``` r
# How do we interpret this?
fit_1[[3]]
```

    ## 
    ##         f1      f2      f3 
    ## q01          0.789*      .*
    ## q02  0.530*                
    ## q03  0.489* -0.371*        
    ## q04          0.662*        
    ## q05          0.587*        
    ## q06                  0.636*
    ## q07                  0.842*
    ## q08          0.498*

``` r
fit_1$loadings
```

    ## $nf1
    ##         f1
    ## q01  0.586
    ## q02 -0.233
    ## q03 -0.570
    ## q04  0.667
    ## q05  0.574
    ## q06  0.494
    ## q07  0.650
    ## q08  0.486
    ## 
    ## $nf2
    ##         f1     f2
    ## q01  0.728 -0.123
    ## q02 -0.176 -0.063
    ## q03 -0.483 -0.109
    ## q04  0.662  0.028
    ## q05  0.591 -0.001
    ## q06  0.103  0.481
    ## q07 -0.003  0.944
    ## q08  0.475  0.025
    ## 
    ## $nf3
    ##         f1     f2     f3
    ## q01  0.003  0.789 -0.185
    ## q02  0.530  0.002  0.014
    ## q03  0.489 -0.371 -0.005
    ## q04 -0.021  0.662  0.014
    ## q05 -0.017  0.587 -0.009
    ## q06  0.089  0.008  0.636
    ## q07 -0.018 -0.003  0.842
    ## q08  0.049  0.498  0.027
    ## 
    ## $nf4
    ##         f1     f2     f3     f4
    ## q01 -0.004  0.694  0.058 -0.143
    ## q02  0.498  0.003 -0.085 -0.005
    ## q03  0.488 -0.451  0.004  0.000
    ## q04 -0.016  0.671 -0.004  0.015
    ## q05  0.002  0.007  0.831  0.007
    ## q06  0.071 -0.005  0.035  0.601
    ## q07 -0.022  0.010 -0.008  0.856
    ## q08  0.058  0.585 -0.089  0.010

``` r
# Let's explore the result with two factors
summary(fit_1[[2]], nd = 3L, cutoff = 0.3, dot.cutoff = 0.05)
```

    ## lavaan 0.6.13 ended normally after 1 iteration
    ## 
    ##   Estimator                                         ML
    ##   Optimization method                           NLMINB
    ##   Number of model parameters                        31
    ## 
    ##   Rotation method                       GEOMIN OBLIQUE
    ##   Geomin epsilon                                 0.001
    ##   Rotation algorithm (rstarts)                GPA (30)
    ##   Standardized metric                             TRUE
    ##   Row weights                                     None
    ## 
    ##   Number of observations                          2571
    ##   Number of missing patterns                         1
    ## 
    ## Model Test User Model:
    ##                                                       
    ##   Test statistic                               199.069
    ##   Degrees of freedom                                13
    ##   P-value (Chi-square)                           0.000
    ## 
    ## Standardized loadings: (* = significant at 1% level)
    ## 
    ##         f1      f2       unique.var   communalities
    ## q01  0.728*      .*           0.565           0.435
    ## q02      .*      .            0.951           0.049
    ## q03 -0.483*      .*           0.690           0.310
    ## q04  0.662*                   0.538           0.462
    ## q05  0.591*                   0.651           0.349
    ## q06      .   0.481*           0.697           0.303
    ## q07          0.944*           0.112           0.888
    ## q08  0.475*                   0.759           0.241
    ## 
    ##                               f1    f2 total
    ## Sum of sq (obliq) loadings 1.850 1.187  3.04
    ## Proportion of total        0.609 0.391  1.00
    ## Proportion var             0.231 0.148  0.38
    ## Cumulative var             0.231 0.380  0.38
    ## 
    ## Factor correlations: (* = significant at 1% level)
    ## 
    ##        f1      f2 
    ## f1  1.000         
    ## f2  0.614*  1.000

``` r
# We will get the eigen values
ev <- eigen(cor_mat)
ev$values
```

    ## [1] 3.057 1.067 0.958 0.736 0.622 0.571 0.543 0.446

``` r
# Automatic one
scree(cor_mat, pc = FALSE)
```

![](Script_L3_files/figure-gfm/number%20of%20factors-1.png)<!-- -->

``` r
# With parallel analysis
fa.parallel(anxiety, fa = "fa")
```

![](Script_L3_files/figure-gfm/number%20of%20factors-2.png)<!-- -->

    ## Parallel analysis suggests that the number of factors =  3  and the number of components =  NA

In the first part of code just presented we see the different eigen
values, which represent the the variance that each additional factor
brings to the table when included. These values are closely linked to
the ones that we see in the screeplot, although they are not exactly the
same, since the latter represent the share over the total variance of
each additional factor.

Let us think about this calmly with the numbers we see as an example.
The first eigenvalue is 3.057, and the second eigenvalue is 1.067. That
means that the share of the variance that the second factor is
1.067/(3.057+1.067) = 0.259. Thus, if we were to keep this logic, each
additional factor that we contrast is going to be measured against the
total variance given by the remaining factors and the factor itself
(e.g., for the third factor it would be 0.958/(3.057+1.067+0.958)) which
will inevitably lead to a constantly decreasing screeplot.

As we see, it is not completely clear how many factor we should select
in this case. We do know however that: (i) the Kaiser-Guttman rule
suggest a unique factor, (ii) the parallel analysis suggest to keep
three factors, and (iii) there is a ‘knee’ at the two factors mark
suggesting that this is a sensible choice. All things considered, we
will go with 2 factor model in this case. How would you interpret these
factors? What can wee see in here? (Hint: Check the summary of the model
that is above and think on the factor loadings that we estimated).

Furthermore, we can inspect some of the fit measures to evaluate if the
model that we are selecting is the most adequate for our data. To do
this we can also use some loops.

``` r
# Remember loops?
Fit <- matrix(data = NA, nrow = 4, ncol = 4) 

for (i in 1:4){
  Fit[,i] <- fitMeasures(fit_1[[i]], fit.measures = c("chisq","rmsea", "tli", "cfi"))
}

Fit
```

    ##         [,1]     [,2]    [,3] [,4]
    ## [1,] 554.191 199.0691 13.8449 1.39
    ## [2,]   0.102   0.0746  0.0195 0.00
    ## [3,]   0.819   0.9031  0.9934 1.00
    ## [4,]   0.871   0.9550  0.9983 1.00

We are seeing some weird coefficients in the last column. Why do you
think that this is? Should we trust these numbers to assess the quality
of our model?

Finally, let’s think about the correlations between our variables. As we
mentioned before, the observed indicators are assumed to be only related
through the latent factor, which would imply that:

$$
  Cov(x_{i}, x_{i}) = \lambda_{j}\lambda_{i}
$$ This might not happen in practice, which would be an indicative of
poor model fit. Let us check if this occurs.

``` r
# The correlations according to the model (without considering the main diagonal)
fit_1$loadings$nf2[,1]%o%fit_1$loadings$nf2[,1]
```

    ##          q01       q02      q03     q04      q05       q06       q07      q08
    ## q01  0.52978 -0.128368 -0.35147  0.4818  0.43051  0.074955 -1.87e-03  0.34574
    ## q02 -0.12837  0.031104  0.08516 -0.1168 -0.10431 -0.018162  4.53e-04 -0.08377
    ## q03 -0.35147  0.085163  0.23318 -0.3197 -0.28561 -0.049727  1.24e-03 -0.22937
    ## q04  0.48184 -0.116753 -0.31967  0.4382  0.39155  0.068173 -1.70e-03  0.31445
    ## q05  0.43051 -0.104314 -0.28561  0.3916  0.34983  0.060910 -1.52e-03  0.28095
    ## q06  0.07496 -0.018162 -0.04973  0.0682  0.06091  0.010605 -2.64e-04  0.04892
    ## q07 -0.00187  0.000453  0.00124 -0.0017 -0.00152 -0.000264  6.58e-06 -0.00122
    ## q08  0.34574 -0.083774 -0.22937  0.3145  0.28095  0.048916 -1.22e-03  0.22563

``` r
# The observed correlation
cor_mat
```

    ##         q01     q02    q03    q04    q05     q06    q07     q08
    ## q01  1.0000 -0.0987 -0.337  0.436  0.402  0.2167  0.305  0.3307
    ## q02 -0.0987  1.0000  0.318 -0.112 -0.119 -0.0742 -0.159 -0.0496
    ## q03 -0.3366  0.3184  1.000 -0.380 -0.310 -0.2267 -0.382 -0.2586
    ## q04  0.4359 -0.1119 -0.380  1.000  0.401  0.2782  0.409  0.3494
    ## q05  0.4024 -0.1193 -0.310  0.401  1.000  0.2575  0.339  0.2686
    ## q06  0.2167 -0.0742 -0.227  0.278  0.257  1.0000  0.514  0.2228
    ## q07  0.3054 -0.1592 -0.382  0.409  0.339  0.5136  1.000  0.2975
    ## q08  0.3307 -0.0496 -0.259  0.349  0.269  0.2228  0.297  1.0000

Finally, we can retrieve our latent variables and store them in the data
set. This is a common practice when you want to employ the factors in
aurther analyses

``` r
fit_2 <- fa(anxiety, nfactors = 2)
fa_scores <- factor.scores(anxiety, fit_2)
anxiety <- cbind(anxiety, fa_scores$scores)
head(anxiety)
```

    ##      q01 q02 q03 q04 q05 q06 q07 q08    MR1     MR2
    ## [1,]   2   1   4   2   2   2   3   1 -0.761  1.1315
    ## [2,]   1   1   4   3   2   2   2   2 -1.061  0.1252
    ## [3,]   2   3   2   2   4   1   2   2 -0.535 -0.7299
    ## [4,]   3   1   1   4   3   3   4   2  1.245 -0.0366
    ## [5,]   2   1   3   2   2   3   3   2 -0.427  0.7868
    ## [6,]   2   1   3   2   4   4   4   2  0.394  1.2561
