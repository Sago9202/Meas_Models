Session 5: Logistic Regression
================
Laura Eberlein, Santiago Gómez-Echeverry & Dimitris Pavlopoulos
2023-01-19

**Required packages**

We start by loading the required packages:

``` r
library(foreign) 
library(texreg) 
```

    ## Version:  1.38.6
    ## Date:     2022-04-06
    ## Author:   Philip Leifeld (University of Essex)
    ## 
    ## Consider submitting praise using the praise or praise_interactive functions.
    ## Please cite the JSS article in your publications -- see citation("texreg").

``` r
library(lmtest)
```

    ## Loading required package: zoo

    ## 
    ## Attaching package: 'zoo'

    ## The following objects are masked from 'package:base':
    ## 
    ##     as.Date, as.Date.numeric

``` r
library(sandwich)
```

If you still have objects from previous sessions in your environment,
let’s clear the environment:

``` r
rm(list = ls())
```

**Loading data**

We will be using some data from a post-referendum survey among people
living in Switzerland. The survey was carried out right after the vote
on an initiative whether to ban military assault rifles in private
households or not. If you would like to get some more background you may
consult the Wikipedia article on the referendum, here
(<https://en.wikipedia.org/wiki/2011_Swiss_gun_control_initiative>).

You can load the data from GitHub by running the following code:

``` r
swiss <- read.dta("https://raw.githubusercontent.com/UCLSPP/datasets/master/data/SwissData2011.dta")
```

We will use the following variables for the analysis:

| Variable   | Description                                                                                         |
|:-----------|:----------------------------------------------------------------------------------------------------|
| VoteYes    | 1 if someone votes yes, 0 if someone voted no                                                       |
| age        | Age in years                                                                                        |
| LeftRight  | Left-Right self placement where low values indicate that a respondent is more to the political left |
| university | Binary indicator (dummy) whether respondent has a university degree(1) or not (0)                   |
| german     | Binary indicator (dummy) whether respondent’s mother tongue is German (1) or not (0)                |
| urban      | Binary indicator (dummy) whether respondent lives in a city (1) or not (0)                          |

Now take a look at the first few observations to see what the data set
looks like:

``` r
head(swiss)
```

    ##   VoteYes participation male age LeftRight GovTrust ReligFreq university
    ## 1       1             1    1  49         4        1         1          0
    ## 2       1             1    1  31         3        1         2          0
    ## 3      NA             1    1  26         5        1         1          0
    ## 4       1             1    1  59         3        0        NA          1
    ## 5       0             1    1  64         5        1        NA          0
    ## 6       0             1    1  83         5       -1         1          0
    ##   cantonnr party income german suburb urban married cars urbanization
    ## 1        1     5      4      1      0     1       1    0         90.7
    ## 2        1     3      7      1      0     1       0    1         90.7
    ## 3        1    NA      9      1      0     1       0    2         90.7
    ## 4        1    NA      4      1      0     1       0    1         90.7
    ## 5        1    NA      3      1      1     0       0    0         90.7
    ## 6        1     4      3      1      0     1       1    0         90.7
    ##   nodenomination old_voter
    ## 1          0.132         0
    ## 2          0.132         0
    ## 3          0.132         0
    ## 4          0.132         0
    ## 5          0.132         1
    ## 6          0.132         1

We will also check for missing values and delete rows with missings on
our variables of interest:

``` r
# check for NA's 
table(is.na(swiss$VoteYes))
```

    ## 
    ## FALSE  TRUE 
    ##  1013   490

``` r
table(is.na(swiss$LeftRight))
```

    ## 
    ## FALSE  TRUE 
    ##  1290   213

``` r
table(is.na(swiss$age))
```

    ## 
    ## FALSE 
    ##  1503

``` r
table(is.na(swiss$university))
```

    ## 
    ## FALSE  TRUE 
    ##  1497     6

``` r
table(is.na(swiss$german))
```

    ## 
    ## FALSE 
    ##  1503

``` r
table(is.na(swiss$urban))
```

    ## 
    ## FALSE 
    ##  1503

``` r
# Delete rows with missing information on our variables of interest, and save them in a new dataset "swiss1"
swiss1 <- swiss[!is.na(swiss$VoteYes),]
swiss1 <- swiss1[!is.na(swiss1$LeftRight),] 
swiss1 <- swiss1[!is.na(swiss1$university),] 
```

Before moving on to the new model, we can illustrate some of the
shortcomings of the linear regression model when working with binary
outcome variables.

Let’s run a linear regression (here, a linear probability model) where
“VoteYes” is our dependent variable, and “LeftRight” is our independent
variable.

``` r
linear_mod <- lm(VoteYes ~ LeftRight, data = swiss1)
screenreg(linear_mod)
```

    ## 
    ## =======================
    ##              Model 1   
    ## -----------------------
    ## (Intercept)    1.19 ***
    ##               (0.04)   
    ## LeftRight     -0.14 ***
    ##               (0.01)   
    ## -----------------------
    ## R^2            0.29    
    ## Adj. R^2       0.28    
    ## Num. obs.    901       
    ## =======================
    ## *** p < 0.001; ** p < 0.01; * p < 0.05

The model shows that there is a significant bivariate relationship
between the position in the political spectrum and voting yes in the
referendum. Specifically, the model suggests that increasing LeftRight
by one unit (moving one unit to the Right) decreases the probability
that the respondent will vote yes in the referendum by 14 percentage
points on average.

As we discussed in the lecture, however, the linear probability model
can lead to some odd conclusions with regard to fitted values. Let’s
plot the two variables above, and include the estimated regression line.

Here, we use the **jitter()** function to offset the observations on the
x-axis a little bit. This helps us to better see the amount of
observations that we have at each level of ideology. Furthermore,
instead of plotting dots, we plot vertical bars for the same reason.

``` r
plot(
  x = jitter(swiss1$LeftRight,1),
  y = swiss1$VoteYes,
  pch = "|", bty = "n",
  col = rgb(green = 100, blue = 100, red = 100, alpha = 100, maxColorValue = 255),
  xlab = "Left-Right Self Placement", ylab = "vote yes (1 = yes, 0 = no)",
  ylim = c(-.5, 1.5),
  xlim = c(0, 10),
  main = "Voting Yes on Assault Rifle Ban by Ideology"
  )
abline(lm(VoteYes ~ LeftRight, data = swiss1), lwd = 3)
```

![](Script_L5_files/figure-gfm/plot%201-1.png)<!-- -->

As we can see from the plot, because the functional form of the linear
probability model is linear, the estimated relationship suggests that
respondents with a value of 9 on the Left-Right Self-Placement scale
have a negative probability of voting yes, and respondents with a value
less than about 2 have a probability of voting yes that is greater than
1.This illustrates (one of) the problem(s) using linear regression to
model a binary outcome. It is entirely possible to have a fitted
regression which gives predicted values for some individuals which are
outside of the (0,1) range or probabilities.

**Exercise 1**: Create a plot where “VoteYes” is our dependent variable,
and “age” is our independent variable. Add a regression line (from a
linear probability model) to the plots.

Solution:

``` r
plot(
  x = jitter(swiss1$age,1),
  y = swiss1$VoteYes,
  pch = "|", bty = "n",
  col = rgb(green = 100, blue = 100, red = 100, alpha = 100, maxColorValue = 255),
  xlab = "age", ylab = "vote yes (1 = yes, 0 = no)",
  main = "Voting Yes on Assault Rifle Ban by Age"
  )
abline( lm(VoteYes ~ age, data = swiss1), lwd = 3  )
```

![](Script_L5_files/figure-gfm/plot%202-1.png)<!-- -->

**\Logistic Regression Model**

We use the generalized linear model function *glm()* to estimate a
logistic regression. The syntax is very similar to the lm regression
function that we are already familiar with, but there is an additional
argument that we need to specify (the family argument) in order to tell
R that we would like to estimate a logistic regression model. To see the
description of the glm function, you can use the help function of R:

``` r
?glm
```

    ## starting httpd help server ... done

We tell glm() that we have a binary dependent variable and want to use
the logistic link function using the family = binomial(link = “logit”)
argument. Now, we estimate a model which includes age and LeftRight as
predictors, and VoteYes as the dependent variable:

``` r
m1 <- glm(VoteYes ~ age + LeftRight, data = swiss1, family = binomial(link="logit"))
library(texreg)
screenreg(m1)
```

    ## 
    ## ===========================
    ##                 Model 1    
    ## ---------------------------
    ## (Intercept)        5.01 ***
    ##                   (0.42)   
    ## age               -0.02 ***
    ##                   (0.01)   
    ## LeftRight         -0.81 ***
    ##                   (0.06)   
    ## ---------------------------
    ## AIC              934.45    
    ## BIC              948.86    
    ## Log Likelihood  -464.22    
    ## Deviance         928.45    
    ## Num. obs.        901       
    ## ===========================
    ## *** p < 0.001; ** p < 0.01; * p < 0.05

Interpreting the output of a logistic regression model is less
straightforward than for the linear model, because the coefficients no
longer describe the effect of a unit change in X on Y. Instead, the
direct interpretation of the coefficient is: a one unit change in X is
associated with a $\hat{\beta}$ change in the log-odds of Y, holding
constant other variables. Here, the coefficient on age is equal to
-0.02, implying that the log-odds of voting yes decrease by 0.02 for a
one-unit increase of age, holding constant LeftRight.

**Odds-ratios**

Differences in the log-odds, however, are difficult to interpret
substantively. There are two main approaches to describing the
substantive relationships that emerge from a logistic regression
model: 1) odds-ratios, and 2) predicted probabilities.

The odds ratio (OR) is a measure of how strongly an event is associated with exposure. 
The odds ratio is a ratio of two sets of odds: the odds of the event occurring in an exposed group versus the odds of the event occurring in a non-exposed group.

Converting log-odds differences to odds-ratios is very straightforward.
As the log function is the inverse of the exponential function, we can
simply take the exponent of the coefficient associated with age:

``` r
exp(coef(m1)[["age"]])
```

    ## [1] 0.980796

And we can do the same for the coefficient associated with LeftRight:

``` r
exp(coef(m1)[["LeftRight"]])
```

    ## [1] 0.4444553

We can then interpret the odds-ratios as follows:

- Increasing age by one year, holding constant all other variables,
  multiplies the odds of voting yes in the referendum by 0.98, i.e., the
  odds decrease by 2%.
- In general, when X increases by one unit, the odds of the outcome Y=1
  are multiplied by $exp(\hat{\beta})$, holding other factors constant.

**Question 1.** So, What is the effect of a one-unit increase in age on
VoteYes?

Voting yes on the ban becomes less likely with increasing age. For each
additional year the odds ratio of voting yes decease by 2%.

**Question 2.** What is the effect of a one-unit increase in LeftRight
on VoteYes?

Conservatives are less likely to vote in favor of the ban. The odds
ratio of voting for the assault rifle ban decreases by 56% when we move
1 unit into the conservative direction of the ideology measure.

*Predicted probabilities*

Thinking in terms of odds may not be much better than thinking in terms
of log-odds, and so often the most useful discussion of the substantive
effect sizes is in terms of predicted probabilities.

We can use the **predict()** function to calculate fitted values for the
logistic regression model, just as we did for the linear model. Here,
however, we need to take into account the fact that we model the
log-odds that Y=1, rather than the probability that Y=1. The predict()
function will therefore, by default, give us predictions for Y on the
log-odds scale. To get predictions on the probability scale, we need to
add an additional argument to predict(): we set the type argument to
type = “response”.

For example, if we would like to calculate the predicted probability of
a yes vote for someone who is 55 years old and scores 7 on the
left-right scale (so very conservative), we could use:

``` r
# predicted probability of yes-vote for age 55 and left-right 7
pp <- predict(m1, newdata = data.frame(age = 55, LeftRight = 7), type = "response")
pp
```

    ##         1 
    ## 0.1507965

This tells us that the probability of a respondent with these covariate
values voting yes in the referendum (e.g., voting to ban assault rifle,
Y=1) is 0.15, based on this model.

**Exercise**: What is the effect on the probability of a “yes” vote of
moving from a left-right self placement of 5 to a self placement of 6
for an individual who is 44 years old?

``` r
# predicted probability of yes-vote for left-right 5 and age 44
s1 <- predict(m1, newdata = data.frame(age = 44, LeftRight = 5), type = "response")
s1
```

    ##         1 
    ## 0.5266603

``` r
# predicted probability of yes-vote for left-right 6 and age 44
s2 <- predict(m1, newdata = data.frame(age = 44, LeftRight = 6), type = "response")
s2
```

    ##         1 
    ## 0.3308898

``` r
# first differences
s1 - s2
```

    ##         1 
    ## 0.1957705

The probability of voting in favour decreases by 20 percentage points
from 53% to 33%. Assuming a threshold of 0.5, we would predict that the
44 years old respondent who is at 5 on the ideology scale would vote for
the ban. The respondent who is of the same age but at 6 on the ideology
scale would vote against the ban.

As discussed in lecture, the logistic model implies a non-linear
relationship between the X variables and the outcome. To see this more
clearly, we can calculate the predicted probability of voting yes across
the range of the age variable for individuals who have a left-right self
placement of 5.

``` r
# age range
s3 <- predict(m1, newdata = data.frame(age = seq(min(swiss1$age), max(swiss1$age), length.out = 100),
                                       LeftRight = 5), type = "response" )
```

``` r
max(s3)
```

    ## [1] 0.6481467

``` r
min(s3)
```

    ## [1] 0.3258398

We predict that the probability of voting for the ban decreases with age
for a respondent with centrist ideology (left-right = 5) from 65% to
33%. This is a substantial effect.

We can do the same across the range of the LeftRight variable for
individuals with an age of 50.

``` r
# left-right range
s4 <- predict(m1, newdata = data.frame(age = 50,
                                       LeftRight = seq(min(swiss1$LeftRight, na.rm = TRUE), 
                                                       max(swiss1$LeftRight, na.rm = TRUE),
                                                       length.out = 100)), type = "response" )

plot(
  x= jitter(swiss1$LeftRight[swiss1$age==50],1),
  y = swiss1$VoteYes[swiss1$age==50],
  pch = "|", bty = "n",
  col = rgb(green = 100, blue = 100, red = 100, alpha = 150, maxColorValue = 255),
  xlab = "Left-Right Self Placement", 
  ylab = "Predicted Probability of Yes-Vote",
  main = "Effect of Ideology for Fifty Year Olds"
  )
abline(h=.5, lty = "dotted", lwd = 3)
text(x = 8, y= .50, pos = 3, "cutoff pi = .5")
lines(x = seq(min(swiss1$LeftRight, na.rm = TRUE), 
              max(swiss1$LeftRight, na.rm = TRUE),
              length.out = 100),
      y = s4, lwd = 3)
```

![](Script_L5_files/figure-gfm/range%20left-right-1.png)<!-- -->

``` r
max(s4)
```

    ## [1] 0.9827904

``` r
min(s4)
```

    ## [1] 0.03721116

We predict that the probability of voting for the ban decreases the more
conservative the respondent. For a 50 year old respondent, who is on the
extreme left of the ideology scale, we predict a 98% probability of
voting yes. The predicted probability of voting in favour decreases
rapidly the more conservative the respondent, to 4% at the extreme right
of the scale.

**Exercise** Include the independent variables (1) university, (2)
german, and (3) urban in the model.

We suspect that university-educated respondents are generally more
liberal and more supportive of gun control specifically. University
classes, particularly those in statistics, teach that gun laws are
beneficial to society as a whole because freely available guns do not
prevent crime but are potentially harmful. In addition, we control for
the cultural language gap in Switzerland, where German-speaking areas
are potentially more conservative and more supportive of liberal gun
laws. We control for urbanization because we suspect that rural areas
are more status quo oriented, while urban areas favor stricter gun
regulation.

``` r
m2 <- glm(VoteYes ~ age + LeftRight + university + german + urban, data = swiss1, family = binomial(link="logit"))
screenreg(list(m1, m2)) # show model 1 and model 2
```

    ## 
    ## ========================================
    ##                 Model 1      Model 2    
    ## ----------------------------------------
    ## (Intercept)        5.01 ***     4.64 ***
    ##                   (0.42)       (0.44)   
    ## age               -0.02 ***    -0.02 ***
    ##                   (0.01)       (0.01)   
    ## LeftRight         -0.81 ***    -0.80 ***
    ##                   (0.06)       (0.06)   
    ## university                      0.67 ***
    ##                                (0.19)   
    ## german                         -0.12    
    ##                                (0.17)   
    ## urban                           0.42 *  
    ##                                (0.18)   
    ## ----------------------------------------
    ## AIC              934.45       917.79    
    ## BIC              948.86       946.61    
    ## Log Likelihood  -464.22      -452.90    
    ## Deviance         928.45       905.79    
    ## Num. obs.        901          901       
    ## ========================================
    ## *** p < 0.001; ** p < 0.01; * p < 0.05

The effect of german in our new model is not statistically significant.
As expected, university educated respondents are more in favour of the
assault rifle regulation. Similarly, the more urban the canton, the
respondent lives in, the more likely the respondent is to be in favour
of the regulation.

Comparing our two models, we conclude that none of the new variables
were confounding the effects of age and ideology. The effects of age and
ideology are substantially unchanged.

We illustrate the effect of higher education and urbanisation in a plot.
We vary urbanization from its minimum to its maximum. We plot two lines
one for respondents with higher education and one for respondents
without university education. We will keep constant age, LeftRight, and
german and the appropriate measures of central tendency.

``` r
# newdata with no university degree
X1 <- data.frame(
  age = mean(swiss1$age),
  LeftRight = mean(swiss1$LeftRight, na.rm = TRUE),
  university = 0,
  german = median(swiss1$german),
  urban = seq(min(swiss1$urban), max(swiss1$urban),length.out = 100)
)

# newdata with university degree
X2 <- data.frame(
  age = mean(swiss1$age),
  LeftRight = mean(swiss1$LeftRight, na.rm = TRUE),
  university = 1,
  german = median(swiss1$german),
  urban = seq(min(swiss1$urban), max(swiss1$urban),length.out = 100)
)


# no university degree
X1$pp <- predict(m2, newdata = X1, type = "response")

# university degree
X2$pp <- predict(m2, newdata = X2, type = "response")


# plot
plot(
  x = X1$urban,
  y = X1$pp,
  type = "l",
  ylim = c(0,1),
  main = "Effects of Urbanisation and Higher Education on Yes-Vote",
  xlab = "Share of citizens in canton living in urban areas",
  ylab = "Predicted Probability of Yes-Vote",
  lwd = 3,
  frame.plot = FALSE
  )
abline(h=.5, lty = "dotted", lwd = 3)
text(x = .8, y= .50, pos = 1, "cutoff pi = .5")

# add university education
lines(X2$urban, X2$pp, lwd = 3, col = 2)
```

![](Script_L5_files/figure-gfm/ex%202-1.png)<!-- -->

``` r
# no university degree predictions
range(X1$pp)
```

    ## [1] 0.4324099 0.5367935

``` r
# university degree predictions
range(X2$pp)
```

    ## [1] 0.5989590 0.6943628

We show the effects of urbanization and higher education for a centrist
respondent with mean age (49), from the German speaking part of
Switzerland. An average respondent such as this without a university
degree living in the most rural part of Switzerland is predicted to vote
yes with 44% probability. The same respondent with higher education is
predicted to vote yes with probability 60%. At the other extreme end of
urbanization the predicted probability of a yes-vote for a respondent
without higher education is 54%. The respondent with a university degree
is predicted to vote yes with 70% probability.

**Likelihood-ratio test**

Our first model m1 included age and ideology as predictors. In our
second model, we also included university, german and urban. Let’s
compare the models in a table again.

``` r
screenreg(list(m1,m2))
```

    ## 
    ## ========================================
    ##                 Model 1      Model 2    
    ## ----------------------------------------
    ## (Intercept)        5.01 ***     4.64 ***
    ##                   (0.42)       (0.44)   
    ## age               -0.02 ***    -0.02 ***
    ##                   (0.01)       (0.01)   
    ## LeftRight         -0.81 ***    -0.80 ***
    ##                   (0.06)       (0.06)   
    ## university                      0.67 ***
    ##                                (0.19)   
    ## german                         -0.12    
    ##                                (0.17)   
    ## urban                           0.42 *  
    ##                                (0.18)   
    ## ----------------------------------------
    ## AIC              934.45       917.79    
    ## BIC              948.86       946.61    
    ## Log Likelihood  -464.22      -452.90    
    ## Deviance         928.45       905.79    
    ## Num. obs.        901          901       
    ## ========================================
    ## *** p < 0.001; ** p < 0.01; * p < 0.05

As you can see, the log-likelihood in m2 is larger than the
log-likelihood in m1. That means that the same is true for the
likelihoods. The likelihood is a relative measure. We do not know
whether any particular value is large or small but we can compare the
likelihoods between two nested models. We want to test now whether the
increase in the likelihood could be due too chance (sampling
variability). To do this, we apply the likelihood ratio test.

In R, you need to load the **library(lmtest)** to carry out the test.
The actual test is done by using the lrtest() function which stands for
likelihood-ratio test. We will do this now. The null hypothesis is that
m2 is not an improvement on m1 but that they are similar models,
i.e. both explain the world equally well. We can reject that null if the
p value is small. Here, we require it to be less than 0.05.

``` r
lrtest(m1,m2)
```

    ## Likelihood ratio test
    ## 
    ## Model 1: VoteYes ~ age + LeftRight
    ## Model 2: VoteYes ~ age + LeftRight + university + german + urban
    ##   #Df  LogLik Df  Chisq Pr(>Chisq)    
    ## 1   3 -464.22                         
    ## 2   6 -452.90  3 22.656  4.763e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Our p value is smaller than 0.05. We reject the null hypothesis.
