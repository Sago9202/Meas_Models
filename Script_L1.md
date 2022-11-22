Intro_to_R
================
Laura Eberlein, Santiago Gómez-Echeverry & Dimitris Pavlopoulos
2022-10-31

## Introduction

Let’s go through some of the basics of R. We always use objects and
functions in R.

Data types concern the different types that single values in data can
have. The most basic data types in R are:

- numeric (numbers)
- character (text, sometimes also called ‘strings’)
- factor (categorical data)

– Factors are variables in R which take on a limited number of different
values, and are employed to refer to categorical variables.

- logical (True or False)

``` r
# (i) Numeric

x <- 20
x = 20 # There are different way of assigning objects
x
```

    ## [1] 20

``` r
y <- 37

# We can use R as a calculator
x-y
```

    ## [1] -17

``` r
x+y
```

    ## [1] 57

``` r
x*y;x/y # You can use the semi-colon to get several functions in a line
```

    ## [1] 740

    ## [1] 0.5405405

``` r
res <- x+y # We can store the outcome in a new object

# (ii) Characters

chr <- "Some random text"
chr
```

    ## [1] "Some random text"

``` r
xt <- "20"
xt
```

    ## [1] "20"

``` r
#sum(xt,y) # There is an error message here; xt is not a number but a character
?sum() # We can check the documentation of each function in R to know a bit more about it.
```

    ## starting httpd help server ... done

``` r
# (iii) Factor

# 
f <- as.factor(c(1:10))
f
```

    ##  [1] 1  2  3  4  5  6  7  8  9  10
    ## Levels: 1 2 3 4 5 6 7 8 9 10

``` r
f <- as.factor(seq(from = 1, to = 10, by = 1)) # This is an equivalent 
mean(f) # Factors, though they seem like typical numbers, they are not meant to make standard algebra
```

    ## Warning in mean.default(f): argument is not numeric or logical: returning NA

    ## [1] NA

``` r
# (iv) Logicals

# The results of conditioning or indexing
L <- c(TRUE, FALSE)
test <- ifelse(x<30,TRUE, FALSE)
test
```

    ## [1] TRUE

## Data Structures

``` r
# (i) Vectors
age <- c(27, 21, 30, 32)
age
```

    ## [1] 27 21 30 32

``` r
class(age)
```

    ## [1] "numeric"

``` r
master <- c("Sociology", "Psychology", "Economics", "Political Science")
class(master)
```

    ## [1] "character"

``` r
prstats <-c(FALSE, TRUE, TRUE, FALSE)
class(prstats)
```

    ## [1] "logical"

``` r
# (ii) Matrices

mat1 <- matrix(data = seq(from =1, to = 10, by = 2), nrow = 5, ncol = 5)
mat1
```

    ##      [,1] [,2] [,3] [,4] [,5]
    ## [1,]    1    1    1    1    1
    ## [2,]    3    3    3    3    3
    ## [3,]    5    5    5    5    5
    ## [4,]    7    7    7    7    7
    ## [5,]    9    9    9    9    9

``` r
mat1[1,1] # To check a specif cell
```

    ## [1] 1

``` r
mat1[1,]
```

    ## [1] 1 1 1 1 1

``` r
# We can also use this to manipulate the content

mat1[1,1] <- 1
mat1[1,]
```

    ## [1] 1 1 1 1 1

``` r
# (iii) Data frames

dat <- data.frame(age =age, 
                  master = master, 
                  prstats = prstats, 
                  score = 6:9,
                  gender = c("Male", "Female", "Male", "Female") )  # You can either write c(6,7,8,9) or 6:9
dat
```

    ##   age            master prstats score gender
    ## 1  27         Sociology   FALSE     6   Male
    ## 2  21        Psychology    TRUE     7 Female
    ## 3  30         Economics    TRUE     8   Male
    ## 4  32 Political Science   FALSE     9 Female

``` r
dat$age # To check the vector
```

    ## [1] 27 21 30 32

``` r
# We can subset the data frame 
dat[,c(1,4)] # Selecting only columns 1 and 4
```

    ##   age score
    ## 1  27     6
    ## 2  21     7
    ## 3  30     8
    ## 4  32     9

``` r
dat[,-2] # Select all columns but the second one
```

    ##   age prstats score gender
    ## 1  27   FALSE     6   Male
    ## 2  21    TRUE     7 Female
    ## 3  30    TRUE     8   Male
    ## 4  32   FALSE     9 Female

``` r
# We can further do it with conditions
dat[dat$score>6,] # These are the people that passed the course
```

    ##   age            master prstats score gender
    ## 2  21        Psychology    TRUE     7 Female
    ## 3  30         Economics    TRUE     8   Male
    ## 4  32 Political Science   FALSE     9 Female

``` r
# And use these conditions to create new variables
dat$pass <- dat$score>6
dat
```

    ##   age            master prstats score gender  pass
    ## 1  27         Sociology   FALSE     6   Male FALSE
    ## 2  21        Psychology    TRUE     7 Female  TRUE
    ## 3  30         Economics    TRUE     8   Male  TRUE
    ## 4  32 Political Science   FALSE     9 Female  TRUE

``` r
# Should we include dim (?)
```

## Setting up R

    ## [1] "C:/Users/Startklar/OneDrive - Vrije Universiteit Amsterdam/Measurement Models in Quantitative Research/3 - Practicals/Week 1 - Introduction"

    ## [1] 18060   513

    ## # A tibble: 6 × 513
    ##   name     essro…¹ edition prodd…²  idno cntry    pweight dweight nwspol netus…³
    ##   <chr>      <dbl> <chr>   <chr>   <dbl> <chr+lb>   <dbl>   <dbl> <dbl+> <dbl+l>
    ## 1 ESS10e0…      10 1.3     4.10.2… 10002 BG [Bul…   0.218   1.03   80    1 [Nev…
    ## 2 ESS10e0…      10 1.3     4.10.2… 10006 BG [Bul…   0.218   0.879  63    5 [Eve…
    ## 3 ESS10e0…      10 1.3     4.10.2… 10009 BG [Bul…   0.218   1.01  390    5 [Eve…
    ## 4 ESS10e0…      10 1.3     4.10.2… 10024 BG [Bul…   0.218   0.955  60    5 [Eve…
    ## 5 ESS10e0…      10 1.3     4.10.2… 10027 BG [Bul…   0.218   0.841 120    5 [Eve…
    ## 6 ESS10e0…      10 1.3     4.10.2… 10048 BG [Bul…   0.218   0.946  60    5 [Eve…
    ## # … with 503 more variables: netustm <dbl+lbl>, ppltrst <dbl+lbl>,
    ## #   pplfair <dbl+lbl>, pplhlp <dbl+lbl>, polintr <dbl+lbl>, psppsgva <dbl+lbl>,
    ## #   actrolga <dbl+lbl>, psppipla <dbl+lbl>, cptppola <dbl+lbl>,
    ## #   trstprl <dbl+lbl>, trstlgl <dbl+lbl>, trstplc <dbl+lbl>, trstplt <dbl+lbl>,
    ## #   trstprt <dbl+lbl>, trstep <dbl+lbl>, trstun <dbl+lbl>, trstsci <dbl+lbl>,
    ## #   vote <dbl+lbl>, prtvtebg <dbl+lbl>, prtvtbhr <dbl+lbl>, prtvtecz <dbl+lbl>,
    ## #   prtvthee <dbl+lbl>, prtvtefi <dbl+lbl>, prtvtefr <dbl+lbl>, …

    ##      name              essround    edition            proddate        
    ##  Length:18060       Min.   :10   Length:18060       Length:18060      
    ##  Class :character   1st Qu.:10   Class :character   Class :character  
    ##  Mode  :character   Median :10   Mode  :character   Mode  :character  
    ##                     Mean   :10                                        
    ##                     3rd Qu.:10                                        
    ##                     Max.   :10                                        
    ##                                                                       
    ##       idno          cntry              pweight           dweight       
    ##  Min.   :10002   Length:18060       Min.   :0.07209   Min.   :0.05643  
    ##  1st Qu.:14493   Class :character   1st Qu.:0.21743   1st Qu.:0.94829  
    ##  Median :18879   Mode  :character   Median :0.29632   Median :1.00000  
    ##  Mean   :18932                      Mean   :0.53663   Mean   :1.00003  
    ##  3rd Qu.:23417                      3rd Qu.:0.36276   3rd Qu.:1.03208  
    ##  Max.   :27932                      Max.   :2.81741   Max.   :4.00726  
    ##                                                                        
    ##      nwspol           netusoft        netustm          ppltrst     
    ##  Min.   :   0.00   Min.   :1.000   Min.   :   0.0   Min.   : 0.00  
    ##  1st Qu.:  30.00   1st Qu.:3.000   1st Qu.:  90.0   1st Qu.: 3.00  
    ##  Median :  60.00   Median :5.000   Median : 180.0   Median : 5.00  
    ##  Mean   :  78.56   Mean   :3.958   Mean   : 219.2   Mean   : 4.83  
    ##  3rd Qu.:  90.00   3rd Qu.:5.000   3rd Qu.: 300.0   3rd Qu.: 7.00  
    ##  Max.   :1200.00   Max.   :5.000   Max.   :1440.0   Max.   :10.00  
    ##  NA's   :435       NA's   :27      NA's   :5467     NA's   :71     
    ##     pplfair           pplhlp          polintr        psppsgva    
    ##  Min.   : 0.000   Min.   : 0.000   Min.   :1.00   Min.   :1.000  
    ##  1st Qu.: 4.000   1st Qu.: 3.000   1st Qu.:2.00   1st Qu.:1.000  
    ##  Median : 5.000   Median : 5.000   Median :3.00   Median :2.000  
    ##  Mean   : 5.387   Mean   : 4.792   Mean   :2.78   Mean   :2.128  
    ##  3rd Qu.: 7.000   3rd Qu.: 7.000   3rd Qu.:3.00   3rd Qu.:3.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :4.00   Max.   :5.000  
    ##  NA's   :131      NA's   :80       NA's   :42     NA's   :432    
    ##     actrolga        psppipla        cptppola        trstprl      
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   : 0.000  
    ##  1st Qu.:1.000   1st Qu.:1.000   1st Qu.:1.000   1st Qu.: 2.000  
    ##  Median :2.000   Median :2.000   Median :2.000   Median : 4.000  
    ##  Mean   :1.912   Mean   :2.001   Mean   :1.862   Mean   : 4.138  
    ##  3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:2.000   3rd Qu.: 6.000  
    ##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :10.000  
    ##  NA's   :349     NA's   :352     NA's   :485     NA's   :306     
    ##     trstlgl          trstplc          trstplt          trstprt      
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 3.000   1st Qu.: 5.000   1st Qu.: 1.000   1st Qu.: 1.000  
    ##  Median : 5.000   Median : 7.000   Median : 3.000   Median : 3.000  
    ##  Mean   : 4.856   Mean   : 6.134   Mean   : 3.449   Mean   : 3.381  
    ##  3rd Qu.: 7.000   3rd Qu.: 8.000   3rd Qu.: 5.000   3rd Qu.: 5.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :295      NA's   :150      NA's   :211      NA's   :266     
    ##      trstep           trstun          trstsci            vote      
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   :1.000  
    ##  1st Qu.: 3.000   1st Qu.: 3.000   1st Qu.: 5.000   1st Qu.:1.000  
    ##  Median : 5.000   Median : 5.000   Median : 7.000   Median :1.000  
    ##  Mean   : 4.636   Mean   : 5.046   Mean   : 6.793   Mean   :1.391  
    ##  3rd Qu.: 7.000   3rd Qu.: 7.000   3rd Qu.: 9.000   3rd Qu.:2.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :3.000  
    ##  NA's   :859      NA's   :1456     NA's   :6215     NA's   :184    
    ##     prtvtebg         prtvtbhr         prtvtecz         prtvthee     
    ##  Min.   : 1.000   Min.   : 1.000   Min.   : 1.000   Min.   : 1.000  
    ##  1st Qu.: 1.000   1st Qu.: 1.000   1st Qu.: 3.750   1st Qu.: 1.000  
    ##  Median : 3.000   Median : 2.000   Median : 4.000   Median : 2.000  
    ##  Mean   : 3.593   Mean   : 2.691   Mean   : 4.752   Mean   : 3.341  
    ##  3rd Qu.: 5.000   3rd Qu.: 4.000   3rd Qu.: 7.000   3rd Qu.: 4.000  
    ##  Max.   :12.000   Max.   :10.000   Max.   :10.000   Max.   :16.000  
    ##  NA's   :16595    NA's   :17294    NA's   :16688    NA's   :17111   
    ##     prtvtefi         prtvtefr        prtvtghu         prtvclt1     
    ##  Min.   : 1.000   Min.   : 1.00   Min.   : 1.000   Min.   : 1.000  
    ##  1st Qu.: 2.000   1st Qu.: 6.00   1st Qu.: 3.000   1st Qu.: 5.000  
    ##  Median : 5.000   Median : 7.00   Median : 3.000   Median : 9.000  
    ##  Mean   : 8.722   Mean   : 7.37   Mean   : 3.771   Mean   : 9.607  
    ##  3rd Qu.:17.000   3rd Qu.: 9.00   3rd Qu.: 4.000   3rd Qu.:13.000  
    ##  Max.   :22.000   Max.   :14.00   Max.   :55.000   Max.   :17.000  
    ##  NA's   :16948    NA's   :17186   NA's   :17026    NA's   :17221   
    ##     prtvclt2         prtvclt3         prtvtfsi         prtvtesk    
    ##  Min.   : 1.000   Min.   : 5.000   Min.   : 1.000   Min.   :1.000  
    ##  1st Qu.: 5.000   1st Qu.: 6.000   1st Qu.: 3.000   1st Qu.:1.000  
    ##  Median :11.000   Median : 9.000   Median : 6.000   Median :2.000  
    ##  Mean   : 9.889   Mean   : 9.545   Mean   : 5.594   Mean   :3.338  
    ##  3rd Qu.:15.250   3rd Qu.:12.500   3rd Qu.: 8.000   3rd Qu.:6.000  
    ##  Max.   :18.000   Max.   :17.000   Max.   :12.000   Max.   :8.000  
    ##  NA's   :18042    NA's   :18049    NA's   :17457    NA's   :17154  
    ##     contplt         donprty          badge          sgnptit     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :2.000   Median :2.000   Median :2.000   Median :2.000  
    ##  Mean   :1.882   Mean   :1.966   Mean   :1.952   Mean   :1.839  
    ##  3rd Qu.:2.000   3rd Qu.:2.000   3rd Qu.:2.000   3rd Qu.:2.000  
    ##  Max.   :2.000   Max.   :2.000   Max.   :2.000   Max.   :2.000  
    ##  NA's   :163     NA's   :202     NA's   :177     NA's   :152    
    ##     pbldmna          bctprd         pstplonl       volunfp         clsprty     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.00   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.00   1st Qu.:2.000   1st Qu.:1.000  
    ##  Median :2.000   Median :2.000   Median :2.00   Median :2.000   Median :2.000  
    ##  Mean   :1.949   Mean   :1.875   Mean   :1.87   Mean   :1.872   Mean   :1.585  
    ##  3rd Qu.:2.000   3rd Qu.:2.000   3rd Qu.:2.00   3rd Qu.:2.000   3rd Qu.:2.000  
    ##  Max.   :2.000   Max.   :2.000   Max.   :2.00   Max.   :2.000   Max.   :2.000  
    ##  NA's   :160     NA's   :216     NA's   :194    NA's   :154     NA's   :436    
    ##     prtclebg         prtclbhr        prtclecz         prtclhee     
    ##  Min.   : 1.000   Min.   : 1.00   Min.   : 1.000   Min.   : 1.000  
    ##  1st Qu.: 1.000   1st Qu.: 5.00   1st Qu.: 4.000   1st Qu.: 2.000  
    ##  Median : 2.000   Median : 9.00   Median : 4.000   Median : 2.000  
    ##  Mean   : 3.377   Mean   :10.65   Mean   : 5.003   Mean   : 4.003  
    ##  3rd Qu.: 5.000   3rd Qu.:18.00   3rd Qu.: 7.000   3rd Qu.: 6.000  
    ##  Max.   :12.000   Max.   :20.00   Max.   :10.000   Max.   :19.000  
    ##  NA's   :16868    NA's   :17514   NA's   :17327    NA's   :17454   
    ##     prtclffi         prtclffr         prtclhhu         prtclclt     
    ##  Min.   : 1.000   Min.   : 1.000   Min.   : 1.000   Min.   : 1.000  
    ##  1st Qu.: 3.000   1st Qu.: 5.000   1st Qu.: 3.000   1st Qu.: 2.000  
    ##  Median : 5.000   Median : 7.000   Median : 3.000   Median : 3.000  
    ##  Mean   : 9.102   Mean   : 6.982   Mean   : 4.105   Mean   : 4.479  
    ##  3rd Qu.:17.000   3rd Qu.: 9.000   3rd Qu.: 4.000   3rd Qu.: 5.000  
    ##  Max.   :24.000   Max.   :12.000   Max.   :55.000   Max.   :65.000  
    ##  NA's   :17134    NA's   :17289    NA's   :17400    NA's   :17563   
    ##     prtclfsi         prtclesk        prtdgcl         lrscale      
    ##  Min.   : 1.000   Min.   :1.000   Min.   :1.000   Min.   : 0.000  
    ##  1st Qu.: 3.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.: 4.000  
    ##  Median : 6.000   Median :4.000   Median :2.000   Median : 5.000  
    ##  Mean   : 5.811   Mean   :4.235   Mean   :2.002   Mean   : 5.391  
    ##  3rd Qu.: 8.000   3rd Qu.:6.000   3rd Qu.:2.000   3rd Qu.: 7.000  
    ##  Max.   :12.000   Max.   :8.000   Max.   :4.000   Max.   :10.000  
    ##  NA's   :17711    NA's   :17617   NA's   :11360   NA's   :2308    
    ##     stflife           stfeco           stfgov          stfdem      
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.00   Min.   : 0.000  
    ##  1st Qu.: 6.000   1st Qu.: 3.000   1st Qu.: 2.00   1st Qu.: 3.000  
    ##  Median : 7.000   Median : 5.000   Median : 4.00   Median : 5.000  
    ##  Mean   : 6.961   Mean   : 4.655   Mean   : 4.29   Mean   : 4.907  
    ##  3rd Qu.: 8.000   3rd Qu.: 7.000   3rd Qu.: 6.00   3rd Qu.: 7.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.00   Max.   :10.000  
    ##  NA's   :157      NA's   :419      NA's   :420     NA's   :462     
    ##      stfedu          stfhlth          gincdif         freehms     
    ##  Min.   : 0.000   Min.   : 0.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.: 4.000   1st Qu.: 3.000   1st Qu.:1.000   1st Qu.:1.000  
    ##  Median : 6.000   Median : 6.000   Median :2.000   Median :2.000  
    ##  Mean   : 5.609   Mean   : 5.457   Mean   :2.089   Mean   :2.418  
    ##  3rd Qu.: 8.000   3rd Qu.: 8.000   3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :5.000   Max.   :5.000  
    ##  NA's   :859      NA's   :144      NA's   :288     NA's   :492    
    ##     hmsfmlsh        hmsacld          euftf           lrnobed     
    ##  Min.   :1.000   Min.   :1.000   Min.   : 0.000   Min.   :1.000  
    ##  1st Qu.:3.000   1st Qu.:2.000   1st Qu.: 4.000   1st Qu.:2.000  
    ##  Median :4.000   Median :3.000   Median : 5.000   Median :2.000  
    ##  Mean   :3.561   Mean   :3.236   Mean   : 5.452   Mean   :2.369  
    ##  3rd Qu.:5.000   3rd Qu.:4.000   3rd Qu.: 7.000   3rd Qu.:3.000  
    ##  Max.   :5.000   Max.   :5.000   Max.   :10.000   Max.   :5.000  
    ##  NA's   :881     NA's   :687     NA's   :1188     NA's   :194    
    ##     loylead         imsmetn         imdfetn         impcntr       imbgeco      
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.0   Min.   : 0.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.0   1st Qu.: 3.000  
    ##  Median :3.000   Median :2.000   Median :3.000   Median :3.0   Median : 5.000  
    ##  Mean   :3.027   Mean   :2.206   Mean   :2.616   Mean   :2.7   Mean   : 4.886  
    ##  3rd Qu.:4.000   3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:3.0   3rd Qu.: 7.000  
    ##  Max.   :5.000   Max.   :4.000   Max.   :4.000   Max.   :4.0   Max.   :10.000  
    ##  NA's   :599     NA's   :438     NA's   :429     NA's   :462   NA's   :593     
    ##     imueclt          imwbcnt           happy           sclmeet     
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   :1.000  
    ##  1st Qu.: 3.000   1st Qu.: 3.000   1st Qu.: 6.000   1st Qu.:3.000  
    ##  Median : 5.000   Median : 5.000   Median : 8.000   Median :5.000  
    ##  Mean   : 5.027   Mean   : 4.701   Mean   : 7.139   Mean   :4.559  
    ##  3rd Qu.: 7.000   3rd Qu.: 6.000   3rd Qu.: 9.000   3rd Qu.:6.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :7.000  
    ##  NA's   :545      NA's   :636      NA's   :46       NA's   :97     
    ##     inprdsc          sclact          crmvct         aesfdrk     
    ##  Min.   :0.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:1.000  
    ##  Median :2.000   Median :3.000   Median :2.000   Median :2.000  
    ##  Mean   :2.328   Mean   :2.694   Mean   :1.898   Mean   :1.938  
    ##  3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:2.000   3rd Qu.:2.000  
    ##  Max.   :6.000   Max.   :5.000   Max.   :2.000   Max.   :4.000  
    ##  NA's   :392     NA's   :328     NA's   :82      NA's   :187    
    ##      health         hlthhmp         atchctr          atcherp      
    ##  Min.   :1.000   Min.   :1.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.: 7.000   1st Qu.: 5.000  
    ##  Median :2.000   Median :3.000   Median : 9.000   Median : 6.000  
    ##  Mean   :2.246   Mean   :2.644   Mean   : 8.127   Mean   : 6.128  
    ##  3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:10.000   3rd Qu.: 8.000  
    ##  Max.   :5.000   Max.   :3.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :24      NA's   :71      NA's   :109      NA's   :249     
    ##      rlgblg          rlgdnm         rlgdnafi         rlgdnhu     
    ##  Min.   :1.000   Min.   :1.000   Min.   : 1.000   Min.   :110.0  
    ##  1st Qu.:1.000   1st Qu.:1.000   1st Qu.: 1.000   1st Qu.:110.0  
    ##  Median :1.000   Median :1.000   Median : 1.000   Median :110.0  
    ##  Mean   :1.429   Mean   :1.926   Mean   : 1.311   Mean   :152.1  
    ##  3rd Qu.:2.000   3rd Qu.:3.000   3rd Qu.: 1.000   3rd Qu.:120.0  
    ##  Max.   :2.000   Max.   :8.000   Max.   :14.000   Max.   :998.0  
    ##  NA's   :164     NA's   :7911    NA's   :17281    NA's   :16941  
    ##     rlgdnlt         rlgdnbsk         rlgblge         rlgdnme     
    ##  Min.   :1.000   Min.   : 1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.: 4.000   1st Qu.:2.000   1st Qu.:1.000  
    ##  Median :1.000   Median : 9.000   Median :2.000   Median :1.000  
    ##  Mean   :1.118   Mean   : 6.828   Mean   :1.876   Mean   :1.611  
    ##  3rd Qu.:1.000   3rd Qu.: 9.000   3rd Qu.:2.000   3rd Qu.:2.000  
    ##  Max.   :8.000   Max.   :14.000   Max.   :2.000   Max.   :8.000  
    ##  NA's   :16798   NA's   :17007    NA's   :10342   NA's   :17111  
    ##     rlgdeafi         rlgdehu         rlgdelt         rlgdebsk    
    ##  Min.   : 1.000   Min.   :110.0   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.: 1.000   1st Qu.:110.0   1st Qu.:1.000   1st Qu.:2.000  
    ##  Median : 1.000   Median :110.0   Median :1.000   Median :9.000  
    ##  Mean   : 1.354   Mean   :175.5   Mean   :1.193   Mean   :6.543  
    ##  3rd Qu.: 1.000   3rd Qu.:257.5   3rd Qu.:1.000   3rd Qu.:9.000  
    ##  Max.   :13.000   Max.   :998.0   Max.   :7.000   Max.   :9.000  
    ##  NA's   :17814    NA's   :18004   NA's   :17977   NA's   :18014  
    ##      rlgdgr          rlgatnd           pray          dscrgrp     
    ##  Min.   : 0.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.: 1.000   1st Qu.:5.000   1st Qu.:3.000   1st Qu.:2.000  
    ##  Median : 5.000   Median :6.000   Median :6.000   Median :2.000  
    ##  Mean   : 4.368   Mean   :5.606   Mean   :5.061   Mean   :1.926  
    ##  3rd Qu.: 7.000   3rd Qu.:7.000   3rd Qu.:7.000   3rd Qu.:2.000  
    ##  Max.   :10.000   Max.   :7.000   Max.   :7.000   Max.   :2.000  
    ##  NA's   :247      NA's   :155     NA's   :416     NA's   :269    
    ##     dscrrce           dscrntn            dscrrlg            dscrlng        
    ##  Min.   :0.00000   Min.   :0.000000   Min.   :0.000000   Min.   :0.000000  
    ##  1st Qu.:0.00000   1st Qu.:0.000000   1st Qu.:0.000000   1st Qu.:0.000000  
    ##  Median :0.00000   Median :0.000000   Median :0.000000   Median :0.000000  
    ##  Mean   :0.01301   Mean   :0.006589   Mean   :0.007309   Mean   :0.006589  
    ##  3rd Qu.:0.00000   3rd Qu.:0.000000   3rd Qu.:0.000000   3rd Qu.:0.000000  
    ##  Max.   :1.00000   Max.   :1.000000   Max.   :1.000000   Max.   :1.000000  
    ##                                                                            
    ##     dscretn            dscrage          dscrgnd            dscrsex        
    ##  Min.   :0.000000   Min.   :0.0000   Min.   :0.000000   Min.   :0.000000  
    ##  1st Qu.:0.000000   1st Qu.:0.0000   1st Qu.:0.000000   1st Qu.:0.000000  
    ##  Median :0.000000   Median :0.0000   Median :0.000000   Median :0.000000  
    ##  Mean   :0.008693   Mean   :0.0129   Mean   :0.009967   Mean   :0.004983  
    ##  3rd Qu.:0.000000   3rd Qu.:0.0000   3rd Qu.:0.000000   3rd Qu.:0.000000  
    ##  Max.   :1.000000   Max.   :1.0000   Max.   :1.000000   Max.   :1.000000  
    ##                                                                           
    ##     dscrdsb           dscroth          dscrdk            dscrref         
    ##  Min.   :0.00000   Min.   :0.000   Min.   :0.000000   Min.   :0.0000000  
    ##  1st Qu.:0.00000   1st Qu.:0.000   1st Qu.:0.000000   1st Qu.:0.0000000  
    ##  Median :0.00000   Median :0.000   Median :0.000000   Median :0.0000000  
    ##  Mean   :0.00825   Mean   :0.017   Mean   :0.001107   Mean   :0.0006645  
    ##  3rd Qu.:0.00000   3rd Qu.:0.000   3rd Qu.:0.000000   3rd Qu.:0.0000000  
    ##  Max.   :1.00000   Max.   :1.000   Max.   :1.000000   Max.   :1.0000000  
    ##                                                                          
    ##     dscrnap          dscrna            ctzcntr         brncntr     
    ##  Min.   :0.000   Min.   :0.000000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.:0.000000   1st Qu.:1.000   1st Qu.:1.000  
    ##  Median :1.000   Median :0.000000   Median :1.000   Median :1.000  
    ##  Mean   :0.924   Mean   :0.003211   Mean   :1.034   Mean   :1.055  
    ##  3rd Qu.:1.000   3rd Qu.:0.000000   3rd Qu.:1.000   3rd Qu.:1.000  
    ##  Max.   :1.000   Max.   :1.000000   Max.   :2.000   Max.   :2.000  
    ##                                     NA's   :30      NA's   :15     
    ##    cntbrthd            livecnta       lnghom1            lnghom2         
    ##  Length:18060       Min.   :1937    Length:18060       Length:18060      
    ##  Class :character   1st Qu.:1971    Class :character   Class :character  
    ##  Mode  :character   Median :1985    Mode  :character   Mode  :character  
    ##                     Mean   :1985                                         
    ##                     3rd Qu.:2001                                         
    ##                     Max.   :2021                                         
    ##                     NA's   :17084                                        
    ##     feethngr        facntr        fbrncntc             mocntr     
    ##  Min.   :1.00   Min.   :1.000   Length:18060       Min.   :1.000  
    ##  1st Qu.:1.00   1st Qu.:1.000   Class :character   1st Qu.:1.000  
    ##  Median :1.00   Median :1.000   Mode  :character   Median :1.000  
    ##  Mean   :1.08   Mean   :1.097                      Mean   :1.086  
    ##  3rd Qu.:1.00   3rd Qu.:1.000                      3rd Qu.:1.000  
    ##  Max.   :2.00   Max.   :2.000                      Max.   :2.000  
    ##  NA's   :141    NA's   :114                        NA's   :55     
    ##    mbrncntc            ccnthum         ccrdprs          wrclmch   
    ##  Length:18060       Min.   : 1.00   Min.   : 0.000   Min.   :1.0  
    ##  Class :character   1st Qu.: 3.00   1st Qu.: 4.000   1st Qu.:3.0  
    ##  Mode  :character   Median : 3.00   Median : 6.000   Median :3.0  
    ##                     Mean   : 4.02   Mean   : 5.715   Mean   :3.2  
    ##                     3rd Qu.: 4.00   3rd Qu.: 8.000   3rd Qu.:4.0  
    ##                     Max.   :55.00   Max.   :10.000   Max.   :5.0  
    ##                     NA's   :355     NA's   :594      NA's   :337  
    ##     admrclc         testic34         testic35         testic36     
    ##  Min.   :1.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:1.000   1st Qu.: 4.000   1st Qu.: 2.000   1st Qu.: 3.000  
    ##  Median :2.000   Median : 6.000   Median : 4.000   Median : 5.000  
    ##  Mean   :1.998   Mean   : 5.719   Mean   : 4.035   Mean   : 4.798  
    ##  3rd Qu.:3.000   3rd Qu.: 7.000   3rd Qu.: 6.000   3rd Qu.: 6.000  
    ##  Max.   :3.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :197     NA's   :12294    NA's   :12268    NA's   :12315   
    ##     testic37        testic38        testic39        testic40    
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :0.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:3.000  
    ##  Median :3.000   Median :2.000   Median :2.000   Median :4.000  
    ##  Mean   :2.668   Mean   :2.176   Mean   :2.445   Mean   :3.506  
    ##  3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:5.000  
    ##  Max.   :4.000   Max.   :4.000   Max.   :4.000   Max.   :6.000  
    ##  NA's   :12354   NA's   :12331   NA's   :12404   NA's   :12346  
    ##     testic41        testic42        vteurmmb         vteubcmb    
    ##  Min.   :0.000   Min.   :0.000   Min.   : 1.000   Min.   : NA    
    ##  1st Qu.:1.000   1st Qu.:2.000   1st Qu.: 1.000   1st Qu.: NA    
    ##  Median :2.000   Median :3.000   Median : 1.000   Median : NA    
    ##  Mean   :2.426   Mean   :2.954   Mean   : 5.514   Mean   :NaN    
    ##  3rd Qu.:3.000   3rd Qu.:4.000   3rd Qu.: 1.000   3rd Qu.: NA    
    ##  Max.   :6.000   Max.   :6.000   Max.   :65.000   Max.   : NA    
    ##  NA's   :12324   NA's   :12377   NA's   :2326     NA's   :18060  
    ##     fairelc          dfprtal          medcrgv         rghmgpr      
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.00   Min.   : 0.000  
    ##  1st Qu.: 8.000   1st Qu.: 7.000   1st Qu.: 7.00   1st Qu.: 6.000  
    ##  Median :10.000   Median : 8.000   Median : 9.00   Median : 8.000  
    ##  Mean   : 8.916   Mean   : 8.039   Mean   : 8.39   Mean   : 7.784  
    ##  3rd Qu.:10.000   3rd Qu.:10.000   3rd Qu.:10.00   3rd Qu.:10.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.00   Max.   :10.000  
    ##  NA's   :258      NA's   :608      NA's   :323     NA's   :391     
    ##     votedir          cttresa          gptpelc          gvctzpv      
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 7.000   1st Qu.: 9.000   1st Qu.: 8.000   1st Qu.: 8.000  
    ##  Median : 8.000   Median :10.000   Median : 9.000   Median : 9.000  
    ##  Mean   : 8.065   Mean   : 9.057   Mean   : 8.407   Mean   : 8.456  
    ##  3rd Qu.:10.000   3rd Qu.:10.000   3rd Qu.:10.000   3rd Qu.:10.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :489      NA's   :218      NA's   :490      NA's   :254     
    ##     grdfinc           viepol          wpestop           keydec      
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 7.000   1st Qu.: 6.000   1st Qu.: 7.000   1st Qu.: 7.000  
    ##  Median : 9.000   Median : 8.000   Median : 8.000   Median : 8.000  
    ##  Mean   : 8.061   Mean   : 7.744   Mean   : 8.031   Mean   : 7.881  
    ##  3rd Qu.:10.000   3rd Qu.:10.000   3rd Qu.:10.000   3rd Qu.:10.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :345      NA's   :624      NA's   :460      NA's   :626     
    ##     fairelcc         dfprtalc         medcrgvc         rghmgprc     
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 4.000   1st Qu.: 3.000   1st Qu.: 4.000   1st Qu.: 5.000  
    ##  Median : 7.000   Median : 5.000   Median : 7.000   Median : 7.000  
    ##  Mean   : 6.381   Mean   : 5.247   Mean   : 6.158   Mean   : 6.551  
    ##  3rd Qu.: 9.000   3rd Qu.: 7.000   3rd Qu.: 9.000   3rd Qu.: 8.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :613      NA's   :867      NA's   :428      NA's   :677     
    ##     votedirc         cttresac         gptpelcc         gvctzpvc     
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 2.000   1st Qu.: 2.000   1st Qu.: 2.000   1st Qu.: 2.000  
    ##  Median : 5.000   Median : 5.000   Median : 5.000   Median : 4.000  
    ##  Mean   : 4.578   Mean   : 4.614   Mean   : 4.802   Mean   : 4.005  
    ##  3rd Qu.: 7.000   3rd Qu.: 7.000   3rd Qu.: 7.000   3rd Qu.: 6.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :715      NA's   :579      NA's   :898      NA's   :323     
    ##     grdfincc         viepolc          wpestopc         keydecc      
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 2.000   1st Qu.: 1.000   1st Qu.: 2.000   1st Qu.: 4.000  
    ##  Median : 4.000   Median : 3.000   Median : 4.000   Median : 5.000  
    ##  Mean   : 4.082   Mean   : 3.633   Mean   : 4.247   Mean   : 5.406  
    ##  3rd Qu.: 6.000   3rd Qu.: 5.000   3rd Qu.: 6.000   3rd Qu.: 8.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :582      NA's   :671      NA's   :691      NA's   :1093    
    ##      chpldm         chpldmi          chpldmc          stpldmi      
    ##  Min.   :1.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:1.000   1st Qu.: 7.000   1st Qu.: 2.000   1st Qu.: 6.000  
    ##  Median :1.000   Median : 8.000   Median : 4.000   Median : 7.000  
    ##  Mean   :1.924   Mean   : 7.981   Mean   : 4.014   Mean   : 6.968  
    ##  3rd Qu.:2.000   3rd Qu.:10.000   3rd Qu.: 6.000   3rd Qu.: 8.000  
    ##  Max.   :5.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :616     NA's   :6923     NA's   :3717     NA's   :15218   
    ##     stpldmc           admit           showcv     impdema         impdemb     
    ##  Min.   : 0.000   Min.   :1.000   Min.   :1   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.: 5.000   1st Qu.:2.000   1st Qu.:1   1st Qu.:1.000   1st Qu.:2.000  
    ##  Median : 7.000   Median :3.000   Median :1   Median :3.000   Median :3.000  
    ##  Mean   : 6.194   Mean   :2.995   Mean   :1   Mean   :2.619   Mean   :2.987  
    ##  3rd Qu.: 8.000   3rd Qu.:4.000   3rd Qu.:1   3rd Qu.:4.000   3rd Qu.:4.000  
    ##  Max.   :10.000   Max.   :5.000   Max.   :1   Max.   :5.000   Max.   :5.000  
    ##  NA's   :15239                                NA's   :14509   NA's   :14517  
    ##     impdemc         impdemd         impdeme         implvdm      
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   : 0.000  
    ##  1st Qu.:2.000   1st Qu.:1.000   1st Qu.:2.000   1st Qu.: 7.000  
    ##  Median :3.000   Median :3.000   Median :3.000   Median : 9.000  
    ##  Mean   :2.992   Mean   :2.862   Mean   :3.044   Mean   : 8.385  
    ##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:5.000   3rd Qu.:10.000  
    ##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :10.000  
    ##  NA's   :14625   NA's   :14536   NA's   :14535   NA's   :277     
    ##     accalaw           hhmmb             gndr           gndr2      
    ##  Min.   : 0.000   Min.   : 1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.: 0.000   1st Qu.: 2.000   1st Qu.:1.000   1st Qu.:1.000  
    ##  Median : 3.000   Median : 2.000   Median :2.000   Median :1.000  
    ##  Mean   : 3.549   Mean   : 2.494   Mean   :1.551   Mean   :1.463  
    ##  3rd Qu.: 6.000   3rd Qu.: 3.000   3rd Qu.:2.000   3rd Qu.:2.000  
    ##  Max.   :10.000   Max.   :13.000   Max.   :2.000   Max.   :2.000  
    ##  NA's   :755      NA's   :53                       NA's   :4538   
    ##      gndr3           gndr4           gndr5           gndr6      
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.:1.000   1st Qu.:1.000   1st Qu.:1.000  
    ##  Median :2.000   Median :2.000   Median :2.000   Median :1.000  
    ##  Mean   :1.534   Mean   :1.507   Mean   :1.514   Mean   :1.472  
    ##  3rd Qu.:2.000   3rd Qu.:2.000   3rd Qu.:2.000   3rd Qu.:2.000  
    ##  Max.   :2.000   Max.   :2.000   Max.   :2.000   Max.   :2.000  
    ##  NA's   :10720   NA's   :14105   NA's   :16720   NA's   :17615  
    ##      gndr7           gndr8           gndr9           gndr10     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.00   
    ##  1st Qu.:1.000   1st Qu.:1.000   1st Qu.:1.000   1st Qu.:1.00   
    ##  Median :2.000   Median :2.000   Median :1.000   Median :2.00   
    ##  Mean   :1.543   Mean   :1.509   Mean   :1.414   Mean   :1.65   
    ##  3rd Qu.:2.000   3rd Qu.:2.000   3rd Qu.:2.000   3rd Qu.:2.00   
    ##  Max.   :2.000   Max.   :2.000   Max.   :2.000   Max.   :2.00   
    ##  NA's   :17920   NA's   :18003   NA's   :18031   NA's   :18040  
    ##      gndr11          gndr12          gndr13          yrbrn           agea      
    ##  Min.   :1.0     Min.   :1       Min.   : NA     Min.   :1931   Min.   :15.00  
    ##  1st Qu.:2.0     1st Qu.:1       1st Qu.: NA     1st Qu.:1955   1st Qu.:36.00  
    ##  Median :2.0     Median :1       Median : NA     Median :1969   Median :51.00  
    ##  Mean   :1.8     Mean   :1       Mean   :NaN     Mean   :1970   Mean   :50.89  
    ##  3rd Qu.:2.0     3rd Qu.:1       3rd Qu.: NA     3rd Qu.:1985   3rd Qu.:66.00  
    ##  Max.   :2.0     Max.   :1       Max.   : NA     Max.   :2006   Max.   :90.00  
    ##  NA's   :18055   NA's   :18059   NA's   :18060   NA's   :120    NA's   :120    
    ##      yrbrn2         yrbrn3          yrbrn4          yrbrn5          yrbrn6     
    ##  Min.   :1931   Min.   :1931    Min.   :1931    Min.   :1933    Min.   :1931   
    ##  1st Qu.:1957   1st Qu.:1977    1st Qu.:1998    1st Qu.:2001    1st Qu.:2003   
    ##  Median :1970   Median :2000    Median :2006    Median :2009    Median :2010   
    ##  Mean   :1969   Mean   :1994    Mean   :2003    Mean   :2005    Mean   :2007   
    ##  3rd Qu.:1981   3rd Qu.:2009    3rd Qu.:2013    3rd Qu.:2015    3rd Qu.:2016   
    ##  Max.   :2021   Max.   :2021    Max.   :2021    Max.   :2021    Max.   :2021   
    ##  NA's   :4822   NA's   :10924   NA's   :14218   NA's   :16773   NA's   :17635  
    ##      yrbrn7          yrbrn8          yrbrn9         yrbrn10     
    ##  Min.   :1935    Min.   :1954    Min.   :1951    Min.   :1986   
    ##  1st Qu.:2003    1st Qu.:2002    1st Qu.:2002    1st Qu.:2002   
    ##  Median :2011    Median :2010    Median :2012    Median :2012   
    ##  Mean   :2005    Mean   :2007    Mean   :2008    Mean   :2009   
    ##  3rd Qu.:2016    3rd Qu.:2015    3rd Qu.:2017    3rd Qu.:2018   
    ##  Max.   :2021    Max.   :2020    Max.   :2020    Max.   :2020   
    ##  NA's   :17927   NA's   :18007   NA's   :18034   NA's   :18041  
    ##     yrbrn11         yrbrn12         yrbrn13         rshipa2     
    ##  Min.   :1990    Min.   :2018    Min.   : NA     Min.   :1.000  
    ##  1st Qu.:2004    1st Qu.:2018    1st Qu.: NA     1st Qu.:1.000  
    ##  Median :2015    Median :2018    Median : NA     Median :1.000  
    ##  Mean   :2010    Mean   :2018    Mean   :NaN     Mean   :1.568  
    ##  3rd Qu.:2019    3rd Qu.:2018    3rd Qu.: NA     3rd Qu.:2.000  
    ##  Max.   :2021    Max.   :2018    Max.   : NA     Max.   :6.000  
    ##  NA's   :18055   NA's   :18059   NA's   :18060   NA's   :4602   
    ##     rshipa3         rshipa4         rshipa5         rshipa6     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :2.000   Median :2.000   Median :2.000   Median :3.000  
    ##  Mean   :2.391   Mean   :2.636   Mean   :2.992   Mean   :3.304  
    ##  3rd Qu.:3.000   3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:5.000  
    ##  Max.   :6.000   Max.   :6.000   Max.   :6.000   Max.   :6.000  
    ##  NA's   :10776   NA's   :14135   NA's   :16741   NA's   :17623  
    ##     rshipa7         rshipa8         rshipa9         rshipa10    
    ##  Min.   :2.000   Min.   :1.000   Min.   :2.000   Min.   :1.00   
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:4.000   1st Qu.:4.00   
    ##  Median :4.000   Median :4.000   Median :4.500   Median :5.00   
    ##  Mean   :3.743   Mean   :3.907   Mean   :4.107   Mean   :4.25   
    ##  3rd Qu.:5.000   3rd Qu.:5.000   3rd Qu.:5.000   3rd Qu.:5.00   
    ##  Max.   :6.000   Max.   :6.000   Max.   :6.000   Max.   :5.00   
    ##  NA's   :17924   NA's   :18006   NA's   :18032   NA's   :18040  
    ##     rshipa11        rshipa12        rshipa13        acchome      
    ##  Min.   :2.0     Min.   :5       Min.   : NA     Min.   :0.0000  
    ##  1st Qu.:2.0     1st Qu.:5       1st Qu.: NA     1st Qu.:1.0000  
    ##  Median :4.0     Median :5       Median : NA     Median :1.0000  
    ##  Mean   :3.4     Mean   :5       Mean   :NaN     Mean   :0.8405  
    ##  3rd Qu.:4.0     3rd Qu.:5       3rd Qu.: NA     3rd Qu.:1.0000  
    ##  Max.   :5.0     Max.   :5       Max.   : NA     Max.   :1.0000  
    ##  NA's   :18055   NA's   :18059   NA's   :18060                   
    ##      accwrk          accmove           accoth          accnone     
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.0000   Min.   :0.000  
    ##  1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.000  
    ##  Median :0.0000   Median :1.0000   Median :0.0000   Median :0.000  
    ##  Mean   :0.4396   Mean   :0.5055   Mean   :0.4404   Mean   :0.123  
    ##  3rd Qu.:1.0000   3rd Qu.:1.0000   3rd Qu.:1.0000   3rd Qu.:0.000  
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :1.0000   Max.   :1.000  
    ##                                                                    
    ##      accref             accdk              accna             fampref     
    ##  Min.   :0.000000   Min.   :0.000000   Min.   :0.000000   Min.   :1.000  
    ##  1st Qu.:0.000000   1st Qu.:0.000000   1st Qu.:0.000000   1st Qu.:1.000  
    ##  Median :0.000000   Median :0.000000   Median :0.000000   Median :3.000  
    ##  Mean   :0.002049   Mean   :0.003655   Mean   :0.001495   Mean   :2.965  
    ##  3rd Qu.:0.000000   3rd Qu.:0.000000   3rd Qu.:0.000000   3rd Qu.:4.000  
    ##  Max.   :1.000000   Max.   :1.000000   Max.   :1.000000   Max.   :5.000  
    ##                                                           NA's   :239    
    ##     famadvs          fampdf         mcclose          mcinter      
    ##  Min.   :1.000   Min.   :1.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:2.000   1st Qu.:1.000   1st Qu.: 5.000   1st Qu.: 4.000  
    ##  Median :3.000   Median :3.000   Median : 7.000   Median : 6.000  
    ##  Mean   :3.024   Mean   :3.051   Mean   : 6.588   Mean   : 5.795  
    ##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.: 9.000   3rd Qu.: 8.000  
    ##  Max.   :5.000   Max.   :5.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :173     NA's   :183     NA's   :730      NA's   :1063    
    ##     mccoord           mcpriv          mcmsinf          chldo12      
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 7.000   1st Qu.: 5.000   1st Qu.: 5.000   1st Qu.: 0.000  
    ##  Median : 8.000   Median : 6.000   Median : 7.000   Median : 1.000  
    ##  Mean   : 7.671   Mean   : 6.018   Mean   : 6.777   Mean   : 1.129  
    ##  3rd Qu.: 9.000   3rd Qu.: 8.000   3rd Qu.: 9.000   3rd Qu.: 2.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :35.000  
    ##  NA's   :802      NA's   :846      NA's   :951      NA's   :303     
    ##     gndro12a        gndro12b         ageo12         hhlio12     
    ##  Min.   :1.00    Min.   :1.000   Min.   :12.00   Min.   :1.000  
    ##  1st Qu.:1.00    1st Qu.:1.000   1st Qu.:22.00   1st Qu.:1.000  
    ##  Median :1.00    Median :1.000   Median :33.00   Median :2.000  
    ##  Mean   :1.46    Mean   :1.473   Mean   :33.53   Mean   :1.679  
    ##  3rd Qu.:2.00    3rd Qu.:2.000   3rd Qu.:44.00   3rd Qu.:2.000  
    ##  Max.   :2.00    Max.   :2.000   Max.   :90.00   Max.   :2.000  
    ##  NA's   :11260   NA's   :14745   NA's   :8152    NA's   :7912   
    ##     closeo12        ttmino12         speako12        scrno12     
    ##  Min.   :1.000   Min.   :   0.0   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.:  15.0   1st Qu.:1.000   1st Qu.:5.000  
    ##  Median :2.000   Median :  40.0   Median :3.000   Median :7.000  
    ##  Mean   :1.853   Mean   : 150.8   Mean   :3.066   Mean   :5.848  
    ##  3rd Qu.:2.000   3rd Qu.: 120.0   3rd Qu.:4.000   3rd Qu.:7.000  
    ##  Max.   :5.000   Max.   :4800.0   Max.   :7.000   Max.   :7.000  
    ##  NA's   :9143    NA's   :11463    NA's   :7926    NA's   :7945   
    ##     phoneo12         como12         c19spo12         c19mco12    
    ##  Min.   :1.000   Min.   :1.000   Min.   : 1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:3.000   1st Qu.: 3.000   1st Qu.:3.000  
    ##  Median :3.000   Median :5.000   Median : 3.000   Median :3.000  
    ##  Mean   :3.309   Mean   :4.745   Mean   : 3.593   Mean   :2.906  
    ##  3rd Qu.:4.000   3rd Qu.:7.000   3rd Qu.: 3.000   3rd Qu.:3.000  
    ##  Max.   :7.000   Max.   :7.000   Max.   :55.000   Max.   :5.000  
    ##  NA's   :7940    NA's   :7939    NA's   :7994     NA's   :8161   
    ##      livpnt         pntmofa          agepnt          hhlipnt     
    ##  Min.   :1.000   Min.   :1.000   Min.   : 32.00   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.:1.000   1st Qu.: 56.00   1st Qu.:2.000  
    ##  Median :2.000   Median :1.000   Median : 66.00   Median :2.000  
    ##  Mean   :2.558   Mean   :1.416   Mean   : 65.69   Mean   :1.762  
    ##  3rd Qu.:4.000   3rd Qu.:2.000   3rd Qu.: 75.00   3rd Qu.:2.000  
    ##  Max.   :4.000   Max.   :2.000   Max.   :101.00   Max.   :2.000  
    ##  NA's   :208     NA's   :11774   NA's   :8436     NA's   :8195   
    ##     closepnt        ttminpnt          speakpnt       scrnpnt     
    ##  Min.   :1.000   Min.   :   0.00   Min.   :1.00   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.:  15.00   1st Qu.:2.00   1st Qu.:6.000  
    ##  Median :2.000   Median :  30.00   Median :3.00   Median :7.000  
    ##  Mean   :2.099   Mean   :  95.51   Mean   :3.24   Mean   :6.122  
    ##  3rd Qu.:3.000   3rd Qu.:  90.00   3rd Qu.:4.00   3rd Qu.:7.000  
    ##  Max.   :5.000   Max.   :4320.00   Max.   :7.00   Max.   :7.000  
    ##  NA's   :9549    NA's   :10726     NA's   :8204   NA's   :8222   
    ##     phonepnt         compnt         c19sppnt         c19mcpnt    
    ##  Min.   :1.000   Min.   :1.000   Min.   : 1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:3.000   1st Qu.: 3.000   1st Qu.:3.000  
    ##  Median :3.000   Median :6.000   Median : 3.000   Median :3.000  
    ##  Mean   :3.557   Mean   :5.144   Mean   : 3.531   Mean   :2.898  
    ##  3rd Qu.:4.000   3rd Qu.:7.000   3rd Qu.: 3.000   3rd Qu.:3.000  
    ##  Max.   :7.000   Max.   :7.000   Max.   :55.000   Max.   :5.000  
    ##  NA's   :8226    NA's   :8238    NA's   :8278     NA's   :8411   
    ##     stfmjob          trdawrk         jbprtfp         pfmfdjba   
    ##  Min.   : 0.000   Min.   :1.000   Min.   :1.000   Min.   :1.00  
    ##  1st Qu.: 7.000   1st Qu.:3.000   1st Qu.:2.000   1st Qu.:1.00  
    ##  Median : 8.000   Median :3.000   Median :3.000   Median :2.00  
    ##  Mean   : 7.511   Mean   :3.007   Mean   :3.033   Mean   :2.27  
    ##  3rd Qu.: 9.000   3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:3.00  
    ##  Max.   :10.000   Max.   :5.000   Max.   :6.000   Max.   :5.00  
    ##  NA's   :8149     NA's   :8120    NA's   :8167    NA's   :9203  
    ##     dcsfwrka        wrkhome         c19whome        c19wplch    
    ##  Min.   :1.000   Min.   :1.000   Min.   : 1.00   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.:3.000   1st Qu.: 3.00   1st Qu.:1.000  
    ##  Median :2.000   Median :6.000   Median :55.00   Median :1.000  
    ##  Mean   :1.765   Mean   :4.809   Mean   :29.52   Mean   :1.473  
    ##  3rd Qu.:2.000   3rd Qu.:6.000   3rd Qu.:55.00   3rd Qu.:2.000  
    ##  Max.   :3.000   Max.   :6.000   Max.   :55.00   Max.   :3.000  
    ##  NA's   :8133    NA's   :8142    NA's   :8265    NA's   :15900  
    ##     wrklong         wrkresp         c19whacc        mansupp     
    ##  Min.   : 1.00   Min.   :1.000   Min.   : 1.00   Min.   : 0.00  
    ##  1st Qu.: 3.00   1st Qu.:3.000   1st Qu.: 3.00   1st Qu.: 6.00  
    ##  Median : 5.00   Median :5.000   Median : 5.00   Median : 8.00  
    ##  Mean   :13.21   Mean   :4.153   Mean   :27.79   Mean   :14.52  
    ##  3rd Qu.: 6.00   3rd Qu.:6.000   3rd Qu.:55.00   3rd Qu.:10.00  
    ##  Max.   :55.00   Max.   :6.000   Max.   :55.00   Max.   :55.00  
    ##  NA's   :8360    NA's   :10147   NA's   :10132   NA's   :8292   
    ##      manhlp         manwrkpl         manspeak        manscrn     
    ##  Min.   :1.000   Min.   : 1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.: 1.000   1st Qu.:1.000   1st Qu.:5.000  
    ##  Median :2.000   Median : 2.000   Median :3.000   Median :7.000  
    ##  Mean   :1.692   Mean   : 2.882   Mean   :2.954   Mean   :5.954  
    ##  3rd Qu.:2.000   3rd Qu.: 3.000   3rd Qu.:4.000   3rd Qu.:7.000  
    ##  Max.   :4.000   Max.   :44.000   Max.   :7.000   Max.   :7.000  
    ##  NA's   :9775    NA's   :9747     NA's   :9759    NA's   :9754   
    ##     manphone         mancom         teamfeel       wrkextra    
    ##  Min.   :1.000   Min.   :1.000   Min.   : 0.0   Min.   : 0.00  
    ##  1st Qu.:3.000   1st Qu.:3.000   1st Qu.: 8.0   1st Qu.: 2.00  
    ##  Median :4.000   Median :5.000   Median :10.0   Median : 5.00  
    ##  Mean   :4.416   Mean   :4.773   Mean   :16.5   Mean   : 4.99  
    ##  3rd Qu.:6.000   3rd Qu.:7.000   3rd Qu.:10.0   3rd Qu.: 8.00  
    ##  Max.   :7.000   Max.   :7.000   Max.   :55.0   Max.   :10.00  
    ##  NA's   :9781    NA's   :9767    NA's   :8132   NA's   :10062  
    ##     colprop           colhlp        colspeak        colscrn     
    ##  Min.   : 1.000   Min.   :1.00   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.: 1.000   1st Qu.:1.00   1st Qu.:1.000   1st Qu.:5.000  
    ##  Median : 3.000   Median :1.00   Median :1.000   Median :7.000  
    ##  Mean   : 9.201   Mean   :1.57   Mean   :2.092   Mean   :5.902  
    ##  3rd Qu.: 6.000   3rd Qu.:2.00   3rd Qu.:3.000   3rd Qu.:7.000  
    ##  Max.   :55.000   Max.   :4.00   Max.   :7.000   Max.   :7.000  
    ##  NA's   :8173     NA's   :9423   NA's   :9393    NA's   :9403   
    ##     colphone         colcom        c19spwrk         c19mcwrk     
    ##  Min.   :1.000   Min.   :1.00   Min.   : 1.000   Min.   : 1.000  
    ##  1st Qu.:3.000   1st Qu.:3.00   1st Qu.: 3.000   1st Qu.: 3.000  
    ##  Median :4.000   Median :4.00   Median : 3.000   Median : 3.000  
    ##  Mean   :4.065   Mean   :4.53   Mean   : 4.083   Mean   : 7.559  
    ##  3rd Qu.:6.000   3rd Qu.:7.00   3rd Qu.: 3.000   3rd Qu.: 3.000  
    ##  Max.   :7.000   Max.   :7.00   Max.   :55.000   Max.   :55.000  
    ##  NA's   :9445    NA's   :9444   NA's   :9495     NA's   :9490    
    ##     mcwrkhom         ipcrtiv         imprich         ipeqopt     
    ##  Min.   : 0.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.: 1.000   1st Qu.:2.000   1st Qu.:3.000   1st Qu.:1.000  
    ##  Median : 6.000   Median :3.000   Median :4.000   Median :2.000  
    ##  Mean   : 5.459   Mean   :2.711   Mean   :4.018   Mean   :2.172  
    ##  3rd Qu.: 9.000   3rd Qu.:3.000   3rd Qu.:5.000   3rd Qu.:3.000  
    ##  Max.   :10.000   Max.   :6.000   Max.   :6.000   Max.   :6.000  
    ##  NA's   :10851    NA's   :282     NA's   :260     NA's   :272    
    ##     ipshabt         impsafe         impdiff         ipfrule     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:1.000   1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :3.000   Median :2.000   Median :3.000   Median :3.000  
    ##  Mean   :3.208   Mean   :2.312   Mean   :2.998   Mean   :3.195  
    ##  3rd Qu.:4.000   3rd Qu.:3.000   3rd Qu.:4.000   3rd Qu.:4.000  
    ##  Max.   :6.000   Max.   :6.000   Max.   :6.000   Max.   :6.000  
    ##  NA's   :307     NA's   :221     NA's   :282     NA's   :357    
    ##     ipudrst         ipmodst         ipgdtim         impfree     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:1.000  
    ##  Median :2.000   Median :3.000   Median :3.000   Median :2.000  
    ##  Mean   :2.501   Mean   :2.745   Mean   :2.855   Mean   :2.309  
    ##  3rd Qu.:3.000   3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:3.000  
    ##  Max.   :6.000   Max.   :6.000   Max.   :6.000   Max.   :6.000  
    ##  NA's   :324     NA's   :311     NA's   :288     NA's   :246    
    ##     iphlppl         ipsuces         ipstrgv         ipadvnt     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:1.000   1st Qu.:3.000  
    ##  Median :2.000   Median :3.000   Median :2.000   Median :4.000  
    ##  Mean   :2.318   Mean   :3.176   Mean   :2.297   Mean   :3.815  
    ##  3rd Qu.:3.000   3rd Qu.:4.000   3rd Qu.:3.000   3rd Qu.:5.000  
    ##  Max.   :6.000   Max.   :6.000   Max.   :6.000   Max.   :6.000  
    ##  NA's   :246     NA's   :335     NA's   :335     NA's   :293    
    ##     ipbhprp         iprspot         iplylfr          impenv     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:1.000   1st Qu.:1.000  
    ##  Median :2.000   Median :3.000   Median :2.000   Median :2.000  
    ##  Mean   :2.648   Mean   :3.218   Mean   :2.112   Mean   :2.203  
    ##  3rd Qu.:3.000   3rd Qu.:4.000   3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :6.000   Max.   :6.000   Max.   :6.000   Max.   :6.000  
    ##  NA's   :306     NA's   :383     NA's   :245     NA's   :256    
    ##     imptrad          impfun         testii1         testii2     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :3.000   Median :3.000   Median :3.000   Median :2.000  
    ##  Mean   :2.774   Mean   :3.067   Mean   :2.587   Mean   :2.174  
    ##  3rd Qu.:4.000   3rd Qu.:4.000   3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :6.000   Max.   :6.000   Max.   :4.000   Max.   :4.000  
    ##  NA's   :238     NA's   :260     NA's   :12242   NA's   :12230  
    ##     testii3         testii4         testii5         testii6     
    ##  Min.   :1.000   Min.   :0.000   Min.   :0.000   Min.   :0.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :2.000   Median :4.000   Median :3.000   Median :3.000  
    ##  Mean   :2.417   Mean   :3.411   Mean   :2.525   Mean   :2.992  
    ##  3rd Qu.:3.000   3rd Qu.:5.000   3rd Qu.:3.000   3rd Qu.:4.000  
    ##  Max.   :4.000   Max.   :6.000   Max.   :6.000   Max.   :6.000  
    ##  NA's   :12297   NA's   :12283   NA's   :12264   NA's   :12322  
    ##     testii7          testii8          testii9         secgrdec    
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.00   Min.   :1.000  
    ##  1st Qu.: 4.000   1st Qu.: 2.000   1st Qu.: 3.00   1st Qu.:2.000  
    ##  Median : 6.000   Median : 4.000   Median : 5.00   Median :3.000  
    ##  Mean   : 5.609   Mean   : 4.082   Mean   : 4.78   Mean   :2.995  
    ##  3rd Qu.: 7.000   3rd Qu.: 6.000   3rd Qu.: 6.00   3rd Qu.:4.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.00   Max.   :5.000  
    ##  NA's   :12269    NA's   :12268    NA's   :12302   NA's   :3224   
    ##     scidecpb         admc19         panpriph         panmonpb     
    ##  Min.   :1.000   Min.   :1.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:2.000   1st Qu.:1.000   1st Qu.: 2.000   1st Qu.: 5.000  
    ##  Median :3.000   Median :1.000   Median : 4.000   Median : 6.000  
    ##  Mean   :3.093   Mean   :1.498   Mean   : 3.711   Mean   : 6.113  
    ##  3rd Qu.:4.000   3rd Qu.:2.000   3rd Qu.: 5.000   3rd Qu.: 8.000  
    ##  Max.   :5.000   Max.   :2.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :3007    NA's   :1977    NA's   :10144    NA's   :10223   
    ##     govpriph         govmonpb         panfolru         panclobo     
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 2.000   1st Qu.: 5.000   1st Qu.: 3.000   1st Qu.: 5.000  
    ##  Median : 4.000   Median : 7.000   Median : 5.000   Median : 7.000  
    ##  Mean   : 3.851   Mean   : 6.756   Mean   : 5.017   Mean   : 6.248  
    ##  3rd Qu.: 5.000   3rd Qu.: 9.000   3rd Qu.: 7.000   3rd Qu.: 9.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :10228    NA's   :10284    NA's   :2245     NA's   :2536    
    ##     panresmo         gvhanc19         gvjobc19         gveldc19     
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 2.000   1st Qu.: 3.000   1st Qu.: 2.000   1st Qu.: 3.000  
    ##  Median : 5.000   Median : 5.000   Median : 5.000   Median : 5.000  
    ##  Mean   : 4.989   Mean   : 5.054   Mean   : 4.384   Mean   : 4.657  
    ##  3rd Qu.: 7.000   3rd Qu.: 7.000   3rd Qu.: 6.000   3rd Qu.: 7.000  
    ##  Max.   :10.000   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :2418     NA's   :2595     NA's   :3294     NA's   :4072    
    ##     gvfamc19        hscopc19         gvbalc19         gvimpc19     
    ##  Min.   : 0.00   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 3.00   1st Qu.: 4.000   1st Qu.: 5.000   1st Qu.: 3.000  
    ##  Median : 5.00   Median : 6.000   Median : 5.000   Median : 5.000  
    ##  Mean   : 4.67   Mean   : 5.951   Mean   : 5.302   Mean   : 4.957  
    ##  3rd Qu.: 7.00   3rd Qu.: 8.000   3rd Qu.: 6.000   3rd Qu.: 7.000  
    ##  Max.   :10.00   Max.   :10.000   Max.   :10.000   Max.   :10.000  
    ##  NA's   :3603    NA's   :2372     NA's   :2974     NA's   :2394    
    ##     gvconc19        respc19         reshhc19        hapljc19      
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :0.00000  
    ##  1st Qu.:2.000   1st Qu.:3.000   1st Qu.:3.000   1st Qu.:0.00000  
    ##  Median :3.000   Median :3.000   Median :3.000   Median :0.00000  
    ##  Mean   :3.042   Mean   :2.645   Mean   :2.889   Mean   :0.01982  
    ##  3rd Qu.:4.000   3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:0.00000  
    ##  Max.   :5.000   Max.   :3.000   Max.   :4.000   Max.   :1.00000  
    ##  NA's   :3115    NA's   :2336    NA's   :2254                     
    ##     hapirc19          hapwrc19          hapfuc19          hapfoc19      
    ##  Min.   :0.00000   Min.   :0.00000   Min.   :0.00000   Min.   :0.00000  
    ##  1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000  
    ##  Median :0.00000   Median :0.00000   Median :0.00000   Median :0.00000  
    ##  Mean   :0.07636   Mean   :0.04945   Mean   :0.05692   Mean   :0.02868  
    ##  3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000  
    ##  Max.   :1.00000   Max.   :1.00000   Max.   :1.00000   Max.   :1.00000  
    ##                                                                         
    ##     hapnoc19         hapnwc19          hapnpc19        haprec19      
    ##  Min.   :0.0000   Min.   :0.00000   Min.   :0.000   Min.   :0.00000  
    ##  1st Qu.:0.0000   1st Qu.:0.00000   1st Qu.:0.000   1st Qu.:0.00000  
    ##  Median :0.0000   Median :0.00000   Median :0.000   Median :0.00000  
    ##  Mean   :0.4587   Mean   :0.09291   Mean   :0.171   Mean   :0.00515  
    ##  3rd Qu.:1.0000   3rd Qu.:0.00000   3rd Qu.:0.000   3rd Qu.:0.00000  
    ##  Max.   :1.0000   Max.   :1.00000   Max.   :1.000   Max.   :1.00000  
    ##                                                                      
    ##     hapdkc19           hapnac19         icvacc19       getavc19   
    ##  Min.   :0.000000   Min.   :0.0000   Min.   :1.00   Min.   :1.00  
    ##  1st Qu.:0.000000   1st Qu.:0.0000   1st Qu.:1.00   1st Qu.:2.00  
    ##  Median :0.000000   Median :0.0000   Median :1.00   Median :2.00  
    ##  Mean   :0.003544   Mean   :0.1002   Mean   :1.07   Mean   :2.18  
    ##  3rd Qu.:0.000000   3rd Qu.:0.0000   3rd Qu.:1.00   3rd Qu.:3.00  
    ##  Max.   :1.000000   Max.   :1.0000   Max.   :2.00   Max.   :3.00  
    ##                                      NA's   :9373   NA's   :3409  
    ##     getnvc19         vdcond         vdovexre         vdtype     
    ##  Min.   :1.000   Min.   :1.000   Min.   : 0.00   Min.   :1.000  
    ##  1st Qu.:1.000   1st Qu.:1.000   1st Qu.: 7.00   1st Qu.:1.000  
    ##  Median :1.000   Median :1.000   Median : 8.00   Median :1.000  
    ##  Mean   :1.457   Mean   :1.254   Mean   : 7.92   Mean   :1.544  
    ##  3rd Qu.:2.000   3rd Qu.:1.000   3rd Qu.:10.00   3rd Qu.:3.000  
    ##  Max.   :2.000   Max.   :3.000   Max.   :10.00   Max.   :4.000  
    ##  NA's   :17522   NA's   :17      NA's   :172     NA's   :17433  
    ##     vdtpsvre           vdtpitre          vdtpscre           vdtpaure       
    ##  Min.   :0.000000   Min.   :0.00000   Min.   :0.000000   Min.   :0.000000  
    ##  1st Qu.:0.000000   1st Qu.:0.00000   1st Qu.:0.000000   1st Qu.:0.000000  
    ##  Median :0.000000   Median :0.00000   Median :0.000000   Median :0.000000  
    ##  Mean   :0.004042   Mean   :0.00371   Mean   :0.001273   Mean   :0.003931  
    ##  3rd Qu.:0.000000   3rd Qu.:0.00000   3rd Qu.:0.000000   3rd Qu.:0.000000  
    ##  Max.   :1.000000   Max.   :1.00000   Max.   :1.000000   Max.   :1.000000  
    ##                                                                            
    ##     vdtpvire           vdtpoire            vdtpntre          vdtpapre     
    ##  Min.   :0.000000   Min.   :0.0000000   Min.   :0.00000   Min.   :0.0000  
    ##  1st Qu.:0.000000   1st Qu.:0.0000000   1st Qu.:0.00000   1st Qu.:1.0000  
    ##  Median :0.000000   Median :0.0000000   Median :0.00000   Median :1.0000  
    ##  Mean   :0.001107   Mean   :0.0008306   Mean   :0.02348   Mean   :0.9643  
    ##  3rd Qu.:0.000000   3rd Qu.:0.0000000   3rd Qu.:0.00000   3rd Qu.:1.0000  
    ##  Max.   :1.000000   Max.   :1.0000000   Max.   :1.00000   Max.   :1.0000  
    ##                                                                           
    ##     vdtprere    vdtpdkre           vdtpnare       
    ##  Min.   :0   Min.   :0.00e+00   Min.   :0.000000  
    ##  1st Qu.:0   1st Qu.:0.00e+00   1st Qu.:0.000000  
    ##  Median :0   Median :0.00e+00   Median :0.000000  
    ##  Mean   :0   Mean   :5.54e-05   Mean   :0.001218  
    ##  3rd Qu.:0   3rd Qu.:0.00e+00   3rd Qu.:0.000000  
    ##  Max.   :0   Max.   :1.00e+00   Max.   :1.000000  
    ##                                                   
    ##      inwds                            ainws                       
    ##  Min.   :2020-09-18 10:18:44.00   Min.   :2020-09-18 10:20:04.00  
    ##  1st Qu.:2021-07-18 17:45:35.25   1st Qu.:2021-07-18 17:53:00.00  
    ##  Median :2021-08-18 15:08:21.00   Median :2021-08-18 15:53:26.00  
    ##  Mean   :2021-08-15 20:06:36.00   Mean   :2021-08-15 21:56:47.91  
    ##  3rd Qu.:2021-09-25 23:28:36.25   3rd Qu.:2021-09-26 10:07:25.50  
    ##  Max.   :2022-01-13 11:02:25.00   Max.   :2022-01-13 11:03:35.00  
    ##                                   NA's   :1                       
    ##      ainwe                            binwe                       
    ##  Min.   :2020-09-18 10:25:21.00   Min.   :2020-09-18 10:35:57.00  
    ##  1st Qu.:2021-07-18 17:54:00.00   1st Qu.:2021-07-18 18:13:58.50  
    ##  Median :2021-08-18 15:37:24.00   Median :2021-08-18 16:23:41.00  
    ##  Mean   :2021-08-15 23:53:38.34   Mean   :2021-08-16 01:16:27.64  
    ##  3rd Qu.:2021-09-26 10:45:38.00   3rd Qu.:2021-09-26 11:37:26.25  
    ##  Max.   :2022-01-13 11:05:18.00   Max.   :2022-01-13 11:14:24.00  
    ##  NA's   :23                       NA's   :2                       
    ##      cinwe                            dinwe                       
    ##  Min.   :2020-09-18 10:44:27.00   Min.   :2020-09-18 10:51:22.00  
    ##  1st Qu.:2021-07-18 18:28:00.00   1st Qu.:2021-07-17 17:19:04.50  
    ##  Median :2021-08-18 16:25:00.00   Median :2021-08-15 09:29:30.00  
    ##  Mean   :2021-08-16 01:15:20.55   Mean   :2021-08-14 07:13:19.07  
    ##  3rd Qu.:2021-09-26 11:32:28.00   3rd Qu.:2021-09-23 09:52:07.50  
    ##  Max.   :2022-01-13 11:20:10.00   Max.   :2022-01-13 11:27:50.00  
    ##  NA's   :7                        NA's   :830                     
    ##      finwe                            ginwe                       
    ##  Min.   :2020-09-18 11:01:21.00   Min.   :2020-09-18 11:07:19.00  
    ##  1st Qu.:2021-07-17 13:39:10.00   1st Qu.:2021-07-17 17:15:27.50  
    ##  Median :2021-08-14 11:39:00.00   Median :2021-08-15 13:26:22.00  
    ##  Mean   :2021-08-13 17:28:32.46   Mean   :2021-08-14 00:46:46.97  
    ##  3rd Qu.:2021-09-22 14:03:13.00   3rd Qu.:2021-09-23 10:53:51.75  
    ##  Max.   :2022-01-13 11:36:14.00   Max.   :2022-01-13 11:46:02.00  
    ##  NA's   :943                      NA's   :1188                    
    ##      hinwe                            iinwe                       
    ##  Min.   :2020-09-18 11:11:36.00   Min.   :2020-09-18 11:12:25.00  
    ##  1st Qu.:2021-07-18 20:44:00.00   1st Qu.:2021-07-18 10:55:46.00  
    ##  Median :2021-08-18 18:08:06.00   Median :2021-08-16 19:45:00.00  
    ##  Mean   :2021-08-16 06:39:15.91   Mean   :2021-08-14 12:56:08.73  
    ##  3rd Qu.:2021-09-26 12:02:27.00   3rd Qu.:2021-09-23 20:33:46.00  
    ##  Max.   :2022-01-13 11:49:38.00   Max.   :2022-01-17 18:42:13.00  
    ##  NA's   :35                       NA's   :1035                    
    ##      kinwe                            vinwe                       
    ##  Min.   :2021-05-05 10:40:51.00   Min.   :2021-01-01 09:00:17.00  
    ##  1st Qu.:2021-07-16 15:31:44.75   1st Qu.:2021-07-19 15:46:02.25  
    ##  Median :2021-08-08 14:58:30.50   Median :2021-08-14 17:23:41.50  
    ##  Mean   :2021-08-16 03:17:41.25   Mean   :2021-08-23 12:05:11.23  
    ##  3rd Qu.:2021-09-08 19:00:55.50   3rd Qu.:2021-09-20 13:12:45.00  
    ##  Max.   :2021-12-31 13:09:00.00   Max.   :2021-12-31 20:44:20.00  
    ##  NA's   :4236                     NA's   :2636                    
    ##      inwde                            jinws                       
    ##  Min.   :2020-09-18 11:21:51.00   Min.   :2020-09-18 11:21:51.00  
    ##  1st Qu.:2021-07-18 20:51:00.00   1st Qu.:2021-07-18 14:02:07.00  
    ##  Median :2021-08-18 19:02:56.50   Median :2021-08-17 08:16:57.00  
    ##  Mean   :2021-08-16 05:42:38.50   Mean   :2021-08-14 23:57:56.72  
    ##  3rd Qu.:2021-09-26 13:26:13.50   3rd Qu.:2021-09-23 19:12:45.00  
    ##  Max.   :2022-01-17 14:44:55.00   Max.   :2022-01-18 15:48:46.00  
    ##  NA's   :6                        NA's   :383                     
    ##      jinwe                            inwtm          domain         
    ##  Min.   :2020-09-18 11:22:51.00   Min.   :  5.0   Length:18060      
    ##  1st Qu.:2021-07-18 14:51:41.00   1st Qu.: 40.0   Class :character  
    ##  Median :2021-08-17 10:20:32.00   Median : 49.0   Mode  :character  
    ##  Mean   :2021-08-15 00:39:28.56   Mean   : 52.3                     
    ##  3rd Qu.:2021-09-23 20:34:49.00   3rd Qu.: 60.0                     
    ##  Max.   :2022-01-18 15:52:36.00   Max.   :759.0                     
    ##  NA's   :393                      NA's   :242                       
    ##      prob              stratum            psu          rshpsts     
    ##  Length:18060       Min.   :   1.0   Min.   :   1   Min.   : 1.00  
    ##  Class :character   1st Qu.: 119.0   1st Qu.: 886   1st Qu.: 1.00  
    ##  Mode  :character   Median : 940.0   Median :4314   Median : 3.00  
    ##                     Mean   : 646.9   Mean   :3738   Mean   :29.94  
    ##                     3rd Qu.:1075.0   3rd Qu.:5722   3rd Qu.:66.00  
    ##                     Max.   :1178.0   Max.   :7534   Max.   :99.00  
    ##                                                                    
    ##     lvgptnea        dvrcdeva         marsts         maritalb     
    ##  Min.   :1.000   Min.   :1.000   Min.   : 1.00   Min.   : 1.000  
    ##  1st Qu.:1.000   1st Qu.:2.000   1st Qu.: 5.00   1st Qu.: 1.000  
    ##  Median :2.000   Median :2.000   Median : 6.00   Median : 3.000  
    ##  Mean   :2.239   Mean   :1.878   Mean   :32.86   Mean   : 3.771  
    ##  3rd Qu.:2.000   3rd Qu.:2.000   3rd Qu.:66.00   3rd Qu.: 6.000  
    ##  Max.   :9.000   Max.   :9.000   Max.   :99.00   Max.   :99.000  
    ##                                                                  
    ##     chldhhe        domicil         edulvlb           eisced      
    ##  Min.   :1.00   Min.   :1.000   Min.   :   0.0   Min.   : 1.000  
    ##  1st Qu.:1.00   1st Qu.:1.000   1st Qu.: 313.0   1st Qu.: 3.000  
    ##  Median :2.00   Median :3.000   Median : 323.0   Median : 4.000  
    ##  Mean   :2.96   Mean   :2.803   Mean   : 443.7   Mean   : 4.633  
    ##  3rd Qu.:6.00   3rd Qu.:4.000   3rd Qu.: 610.0   3rd Qu.: 6.000  
    ##  Max.   :9.00   Max.   :9.000   Max.   :9999.0   Max.   :99.000  
    ##                                                                  
    ##     edlvebg           edlvehr           edlvdcz           edlvdee      
    ##  Min.   :   1.00   Min.   :   1.00   Min.   :   2.00   Min.   : 113.0  
    ##  1st Qu.:   7.00   1st Qu.:   5.00   1st Qu.:   4.00   1st Qu.: 313.0  
    ##  Median :   9.00   Median :   6.00   Median :   6.00   Median : 423.0  
    ##  Mean   :  10.94   Mean   :  25.17   Mean   :  31.56   Mean   : 458.5  
    ##  3rd Qu.:  12.00   3rd Qu.:   7.00   3rd Qu.:   8.00   3rd Qu.: 620.0  
    ##  Max.   :5555.00   Max.   :7777.00   Max.   :8888.00   Max.   :7777.0  
    ##  NA's   :15342     NA's   :16468     NA's   :15584     NA's   :16518   
    ##     edlvdfi           edlvdfr           edlvdahu          edlvdlt      
    ##  Min.   :   1.00   Min.   :   1.00   Min.   :   1.00   Min.   :   0.0  
    ##  1st Qu.:   5.00   1st Qu.:   7.00   1st Qu.:   4.00   1st Qu.:   7.0  
    ##  Median :   7.00   Median :  10.00   Median :   6.00   Median :  10.0  
    ##  Mean   :  12.69   Mean   :  42.83   Mean   :  52.67   Mean   :  92.8  
    ##  3rd Qu.:  10.00   3rd Qu.:  16.00   3rd Qu.:   7.00   3rd Qu.:  13.0  
    ##  Max.   :8888.00   Max.   :7777.00   Max.   :9999.00   Max.   :8888.0  
    ##  NA's   :16483     NA's   :16083     NA's   :16211     NA's   :16401   
    ##     edlvesi           edlvdsk           eduyrs          pdwrk       
    ##  Min.   :   0.00   Min.   :   1.0   Min.   : 0.00   Min.   :0.0000  
    ##  1st Qu.:   3.00   1st Qu.:   6.0   1st Qu.:11.00   1st Qu.:0.0000  
    ##  Median :   4.00   Median :   7.0   Median :12.00   Median :1.0000  
    ##  Mean   :  41.91   Mean   : 171.1   Mean   :14.45   Mean   :0.5356  
    ##  3rd Qu.:   6.00   3rd Qu.:   9.0   3rd Qu.:16.00   3rd Qu.:1.0000  
    ##  Max.   :9999.00   Max.   :9999.0   Max.   :99.00   Max.   :1.0000  
    ##  NA's   :16808     NA's   :16642                                    
    ##      edctn             uempla            uempli            dsbld        
    ##  Min.   :0.00000   Min.   :0.00000   Min.   :0.00000   Min.   :0.00000  
    ##  1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000  
    ##  Median :0.00000   Median :0.00000   Median :0.00000   Median :0.00000  
    ##  Mean   :0.07813   Mean   :0.03599   Mean   :0.02032   Mean   :0.02447  
    ##  3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000  
    ##  Max.   :1.00000   Max.   :1.00000   Max.   :1.00000   Max.   :1.00000  
    ##                                                                         
    ##       rtrd           cmsrv           hswrk             dngoth       
    ##  Min.   :0.000   Min.   :0e+00   Min.   :0.00000   Min.   :0.00000  
    ##  1st Qu.:0.000   1st Qu.:0e+00   1st Qu.:0.00000   1st Qu.:0.00000  
    ##  Median :0.000   Median :0e+00   Median :0.00000   Median :0.00000  
    ##  Mean   :0.297   Mean   :9e-04   Mean   :0.07785   Mean   :0.01124  
    ##  3rd Qu.:1.000   3rd Qu.:0e+00   3rd Qu.:0.00000   3rd Qu.:0.00000  
    ##  Max.   :1.000   Max.   :1e+00   Max.   :1.00000   Max.   :1.00000  
    ##                  NA's   :1592                                       
    ##      dngref             dngdk               dngna            mainact     
    ##  Min.   :0.000000   Min.   :0.0000000   Min.   :0.00000   Min.   : 1.00  
    ##  1st Qu.:0.000000   1st Qu.:0.0000000   1st Qu.:0.00000   1st Qu.:66.00  
    ##  Median :0.000000   Median :0.0000000   Median :0.00000   Median :66.00  
    ##  Mean   :0.002547   Mean   :0.0001661   Mean   :0.00144   Mean   :61.16  
    ##  3rd Qu.:0.000000   3rd Qu.:0.0000000   3rd Qu.:0.00000   3rd Qu.:66.00  
    ##  Max.   :1.000000   Max.   :1.0000000   Max.   :1.00000   Max.   :99.00  
    ##                                                                          
    ##     mnactic          crpdwk         pdjobev         pdjobyr        emplrel     
    ##  Min.   : 1.00   Min.   :1.000   Min.   :1.000   Min.   :1915   Min.   :1.000  
    ##  1st Qu.: 1.00   1st Qu.:2.000   1st Qu.:1.000   1st Qu.:2018   1st Qu.:1.000  
    ##  Median : 1.00   Median :6.000   Median :6.000   Median :6666   Median :1.000  
    ##  Mean   : 3.43   Mean   :4.158   Mean   :3.875   Mean   :5106   Mean   :1.563  
    ##  3rd Qu.: 6.00   3rd Qu.:6.000   3rd Qu.:6.000   3rd Qu.:6666   3rd Qu.:1.000  
    ##  Max.   :99.00   Max.   :9.000   Max.   :9.000   Max.   :9999   Max.   :9.000  
    ##                                                                                
    ##      emplno         wrkctra          estsz           jbspv          njbspv     
    ##  Min.   :    0   Min.   :1.000   Min.   :1.000   Min.   :1.00   Min.   :    0  
    ##  1st Qu.:66666   1st Qu.:1.000   1st Qu.:1.000   1st Qu.:2.00   1st Qu.:66666  
    ##  Median :66666   Median :1.000   Median :3.000   Median :2.00   Median :66666  
    ##  Mean   :61007   Mean   :2.077   Mean   :2.951   Mean   :2.15   Mean   :52968  
    ##  3rd Qu.:66666   3rd Qu.:2.000   3rd Qu.:4.000   3rd Qu.:2.00   3rd Qu.:66666  
    ##  Max.   :99999   Max.   :9.000   Max.   :9.000   Max.   :9.00   Max.   :99999  
    ##                                                                                
    ##     wkdcorga        iorgact           wkhct           wkhtot          nacer2   
    ##  Min.   : 0.00   Min.   : 0.000   Min.   :  0.0   Min.   :  0.0   Min.   :  1  
    ##  1st Qu.: 2.00   1st Qu.: 0.000   1st Qu.: 40.0   1st Qu.: 40.0   1st Qu.: 41  
    ##  Median : 7.00   Median : 4.000   Median : 40.0   Median : 40.0   Median : 56  
    ##  Mean   :11.18   Mean   : 9.846   Mean   :165.4   Mean   :157.5   Mean   :140  
    ##  3rd Qu.:10.00   3rd Qu.: 8.000   3rd Qu.: 48.0   3rd Qu.: 50.0   3rd Qu.: 85  
    ##  Max.   :99.00   Max.   :99.000   Max.   :999.0   Max.   :999.0   Max.   :999  
    ##                                                                                
    ##     tporgwk          isco08         wrkac6m          uemp3m     
    ##  Min.   : 1.00   Min.   :    0   Min.   :1.000   Min.   :1.000  
    ##  1st Qu.: 3.00   1st Qu.: 3131   1st Qu.:2.000   1st Qu.:1.000  
    ##  Median : 4.00   Median : 5223   Median :2.000   Median :2.000  
    ##  Mean   : 9.11   Mean   :12729   Mean   :2.314   Mean   :1.778  
    ##  3rd Qu.: 4.00   3rd Qu.: 8322   3rd Qu.:2.000   3rd Qu.:2.000  
    ##  Max.   :99.00   Max.   :99999   Max.   :9.000   Max.   :9.000  
    ##                                                                 
    ##     uemp12m         uemp5yr          mbtru          hincsrca     
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   : 1.000  
    ##  1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.000   1st Qu.: 1.000  
    ##  Median :6.000   Median :6.000   Median :3.000   Median : 1.000  
    ##  Mean   :4.792   Mean   :4.786   Mean   :2.596   Mean   : 3.141  
    ##  3rd Qu.:6.000   3rd Qu.:6.000   3rd Qu.:3.000   3rd Qu.: 4.000  
    ##  Max.   :9.000   Max.   :9.000   Max.   :9.000   Max.   :99.000  
    ##                                                                  
    ##     hinctnta        hincfel         edulvlpb       eiscedp        edlvpebg    
    ##  Min.   : 1.00   Min.   :1.000   Min.   :   0   Min.   : 1.0   Min.   :   1   
    ##  1st Qu.: 4.00   1st Qu.:2.000   1st Qu.: 323   1st Qu.: 4.0   1st Qu.:   8   
    ##  Median : 6.00   Median :2.000   Median : 720   Median : 7.0   Median :  13   
    ##  Mean   :19.32   Mean   :2.144   Mean   :3249   Mean   :32.3   Mean   :3003   
    ##  3rd Qu.:10.00   3rd Qu.:3.000   3rd Qu.:6666   3rd Qu.:66.0   3rd Qu.:6666   
    ##  Max.   :99.00   Max.   :9.000   Max.   :9999   Max.   :99.0   Max.   :8888   
    ##                                                                NA's   :15342  
    ##     edlvpehr        edlvpdcz        edlvpdee        edlvpdfi    
    ##  Min.   :   1    Min.   :   1    Min.   : 113    Min.   :   1   
    ##  1st Qu.:   6    1st Qu.:   6    1st Qu.: 423    1st Qu.:   5   
    ##  Median :  11    Median :6666    Median : 720    Median :  12   
    ##  Mean   :2997    Mean   :3453    Mean   :3445    Mean   :2682   
    ##  3rd Qu.:6666    3rd Qu.:6666    3rd Qu.:6666    3rd Qu.:6666   
    ##  Max.   :9999    Max.   :8888    Max.   :9999    Max.   :8888   
    ##  NA's   :16468   NA's   :15584   NA's   :16518   NA's   :16483  
    ##     edlvpdfr       edlvpdahu        edlvpdlt        edlvpesi    
    ##  Min.   :   1    Min.   :   2    Min.   :   0    Min.   :   1   
    ##  1st Qu.:   9    1st Qu.:   4    1st Qu.:  10    1st Qu.:   4   
    ##  Median :  20    Median :  10    Median :6666    Median :   7   
    ##  Mean   :2809    Mean   :2829    Mean   :3454    Mean   :2529   
    ##  3rd Qu.:6666    3rd Qu.:6666    3rd Qu.:6666    3rd Qu.:6666   
    ##  Max.   :8888    Max.   :9999    Max.   :8888    Max.   :8888   
    ##  NA's   :16083   NA's   :16211   NA's   :16401   NA's   :16808  
    ##     edlvpdsk         pdwrkp           edctnp            uemplap       
    ##  Min.   :   1    Min.   :0.0000   Min.   :0.000000   Min.   :0.00000  
    ##  1st Qu.:   7    1st Qu.:0.0000   1st Qu.:0.000000   1st Qu.:0.00000  
    ##  Median :  16    Median :0.0000   Median :0.000000   Median :0.00000  
    ##  Mean   :3020    Mean   :0.3508   Mean   :0.007586   Mean   :0.01462  
    ##  3rd Qu.:6666    3rd Qu.:1.0000   3rd Qu.:0.000000   3rd Qu.:0.00000  
    ##  Max.   :8888    Max.   :1.0000   Max.   :1.000000   Max.   :1.00000  
    ##  NA's   :16642                                                        
    ##     uemplip             dsbldp             rtrdp            cmsrvp     
    ##  Min.   :0.000000   Min.   :0.000000   Min.   :0.0000   Min.   :0e+00  
    ##  1st Qu.:0.000000   1st Qu.:0.000000   1st Qu.:0.0000   1st Qu.:0e+00  
    ##  Median :0.000000   Median :0.000000   Median :0.0000   Median :0e+00  
    ##  Mean   :0.007032   Mean   :0.008472   Mean   :0.1506   Mean   :2e-04  
    ##  3rd Qu.:0.000000   3rd Qu.:0.000000   3rd Qu.:0.0000   3rd Qu.:0e+00  
    ##  Max.   :1.000000   Max.   :1.000000   Max.   :1.0000   Max.   :1e+00  
    ##                                                         NA's   :1592   
    ##      hswrkp           dngothp             dngdkp             dngnapp      
    ##  Min.   :0.00000   Min.   :0.000000   Min.   :0.0000000   Min.   :0.0000  
    ##  1st Qu.:0.00000   1st Qu.:0.000000   1st Qu.:0.0000000   1st Qu.:0.0000  
    ##  Median :0.00000   Median :0.000000   Median :0.0000000   Median :0.0000  
    ##  Mean   :0.04103   Mean   :0.005925   Mean   :0.0006645   Mean   :0.4397  
    ##  3rd Qu.:0.00000   3rd Qu.:0.000000   3rd Qu.:0.0000000   3rd Qu.:1.0000  
    ##  Max.   :1.00000   Max.   :1.000000   Max.   :1.0000000   Max.   :1.0000  
    ##                                                                           
    ##     dngrefp             dngnap             mnactp         crpdwkp     
    ##  Min.   :0.000000   Min.   :0.000000   Min.   : 1.00   Min.   :1.000  
    ##  1st Qu.:0.000000   1st Qu.:0.000000   1st Qu.:66.00   1st Qu.:6.000  
    ##  Median :0.000000   Median :0.000000   Median :66.00   Median :6.000  
    ##  Mean   :0.002159   Mean   :0.003931   Mean   :64.21   Mean   :5.181  
    ##  3rd Qu.:0.000000   3rd Qu.:0.000000   3rd Qu.:66.00   3rd Qu.:6.000  
    ##  Max.   :1.000000   Max.   :1.000000   Max.   :99.00   Max.   :9.000  
    ##                                                                       
    ##     isco08p         emprelp         wkhtotp         edulvlfb       eiscedf     
    ##  Min.   :    0   Min.   :1.000   Min.   :  0.0   Min.   :   0   Min.   : 1.00  
    ##  1st Qu.: 7131   1st Qu.:1.000   1st Qu.: 42.0   1st Qu.: 213   1st Qu.: 2.00  
    ##  Median :66666   Median :6.000   Median :666.0   Median : 321   Median : 3.00  
    ##  Mean   :46216   Mean   :4.273   Mean   :468.9   Mean   :1002   Mean   :10.07  
    ##  3rd Qu.:66666   3rd Qu.:6.000   3rd Qu.:666.0   3rd Qu.: 421   3rd Qu.: 5.00  
    ##  Max.   :99999   Max.   :9.000   Max.   :999.0   Max.   :9999   Max.   :99.00  
    ##                                                                                
    ##     edlvfebg         edlvfehr         edlvfdcz         edlvfdee    
    ##  Min.   :   1.0   Min.   :   1.0   Min.   :   1.0   Min.   :   0   
    ##  1st Qu.:   4.0   1st Qu.:   3.0   1st Qu.:   4.0   1st Qu.: 213   
    ##  Median :   7.0   Median :   5.0   Median :   5.0   Median : 321   
    ##  Mean   : 436.1   Mean   : 410.8   Mean   : 577.4   Mean   :1118   
    ##  3rd Qu.:   9.0   3rd Qu.:   6.0   3rd Qu.:   8.0   3rd Qu.: 610   
    ##  Max.   :8888.0   Max.   :8888.0   Max.   :8888.0   Max.   :8888   
    ##  NA's   :15342    NA's   :16468    NA's   :15584    NA's   :16518  
    ##     edlvfdfi         edlvfdfr       edlvfdahu         edlvfdlt    
    ##  Min.   :   1.0   Min.   :   1    Min.   :   1.0   Min.   :   0   
    ##  1st Qu.:   2.0   1st Qu.:   3    1st Qu.:   3.0   1st Qu.:   2   
    ##  Median :   5.0   Median :   7    Median :   4.0   Median :   7   
    ##  Mean   : 459.7   Mean   :1411    Mean   : 365.8   Mean   :1547   
    ##  3rd Qu.:   8.0   3rd Qu.:  19    3rd Qu.:   4.0   3rd Qu.:  13   
    ##  Max.   :8888.0   Max.   :8888    Max.   :9999.0   Max.   :8888   
    ##  NA's   :16483    NA's   :16083   NA's   :16211    NA's   :16401  
    ##     edlvfesi         edlvfdsk         emprf14         occf14b     
    ##  Min.   :   0.0   Min.   :   1.0   Min.   :1.000   Min.   : 1.00  
    ##  1st Qu.:   2.0   1st Qu.:   6.0   1st Qu.:1.000   1st Qu.: 5.00  
    ##  Median :   3.0   Median :   6.0   Median :1.000   Median : 7.00  
    ##  Mean   : 453.2   Mean   : 793.4   Mean   :1.625   Mean   :15.27  
    ##  3rd Qu.:   4.0   3rd Qu.:   7.0   3rd Qu.:1.000   3rd Qu.: 9.00  
    ##  Max.   :9999.0   Max.   :8888.0   Max.   :9.000   Max.   :99.00  
    ##  NA's   :16808    NA's   :16642                                   
    ##     edulvlmb         eiscedm          edlvmebg         edlvmehr     
    ##  Min.   :   0.0   Min.   : 1.000   Min.   :   1.0   Min.   :   1.0  
    ##  1st Qu.: 213.0   1st Qu.: 2.000   1st Qu.:   4.0   1st Qu.:   3.0  
    ##  Median : 321.0   Median : 3.000   Median :   7.0   Median :   4.0  
    ##  Mean   : 723.1   Mean   : 7.347   Mean   : 343.8   Mean   : 258.3  
    ##  3rd Qu.: 323.0   3rd Qu.: 4.000   3rd Qu.:   9.0   3rd Qu.:   6.0  
    ##  Max.   :9999.0   Max.   :99.000   Max.   :8888.0   Max.   :8888.0  
    ##                                    NA's   :15342    NA's   :16468   
    ##     edlvmdcz         edlvmdee         edlvmdfi         edlvmdfr    
    ##  Min.   :   1.0   Min.   :   0.0   Min.   :   1.0   Min.   :   1   
    ##  1st Qu.:   4.0   1st Qu.: 213.0   1st Qu.:   2.0   1st Qu.:   3   
    ##  Median :   5.0   Median : 313.0   Median :   5.0   Median :   7   
    ##  Mean   : 293.4   Mean   : 587.4   Mean   : 306.1   Mean   :1066   
    ##  3rd Qu.:   7.0   3rd Qu.: 520.0   3rd Qu.:   8.0   3rd Qu.:  14   
    ##  Max.   :8888.0   Max.   :8888.0   Max.   :8888.0   Max.   :8888   
    ##  NA's   :15584    NA's   :16518    NA's   :16483    NA's   :16083  
    ##    edlvmdahu         edlvmdlt         edlvmesi         edlvmdsk     
    ##  Min.   :   1.0   Min.   :   0.0   Min.   :   0.0   Min.   :   1.0  
    ##  1st Qu.:   3.0   1st Qu.:   1.0   1st Qu.:   2.0   1st Qu.:   4.0  
    ##  Median :   4.0   Median :   7.0   Median :   3.0   Median :   6.0  
    ##  Mean   : 207.9   Mean   : 801.1   Mean   : 220.6   Mean   : 659.1  
    ##  3rd Qu.:   6.0   3rd Qu.:  12.0   3rd Qu.:   4.0   3rd Qu.:   7.0  
    ##  Max.   :9999.0   Max.   :8888.0   Max.   :9999.0   Max.   :8888.0  
    ##  NA's   :16211    NA's   :16401    NA's   :16808    NA's   :16642   
    ##     emprm14         occm14b         atncrse         anctry1      
    ##  Min.   :1.000   Min.   : 1.00   Min.   :1.000   Min.   : 10000  
    ##  1st Qu.:1.000   1st Qu.: 4.00   1st Qu.:2.000   1st Qu.: 14030  
    ##  Median :1.000   Median : 7.00   Median :2.000   Median : 15020  
    ##  Mean   :1.697   Mean   :21.49   Mean   :1.835   Mean   : 17952  
    ##  3rd Qu.:3.000   3rd Qu.:66.00   3rd Qu.:2.000   3rd Qu.: 15040  
    ##  Max.   :9.000   Max.   :99.00   Max.   :9.000   Max.   :999999  
    ##                                                                  
    ##     anctry2          regunit         region         
    ##  Min.   : 11000   Min.   :2.000   Length:18060      
    ##  1st Qu.:555555   1st Qu.:3.000   Class :character  
    ##  Median :555555   Median :3.000   Mode  :character  
    ##  Mean   :573172   Mean   :2.891                     
    ##  3rd Qu.:555555   3rd Qu.:3.000                     
    ##  Max.   :999999   Max.   :3.000                     
    ## 

    ##   [1] "name"      "essround"  "edition"   "proddate"  "idno"      "cntry"    
    ##   [7] "pweight"   "dweight"   "nwspol"    "netusoft"  "netustm"   "ppltrst"  
    ##  [13] "pplfair"   "pplhlp"    "polintr"   "psppsgva"  "actrolga"  "psppipla" 
    ##  [19] "cptppola"  "trstprl"   "trstlgl"   "trstplc"   "trstplt"   "trstprt"  
    ##  [25] "trstep"    "trstun"    "trstsci"   "vote"      "prtvtebg"  "prtvtbhr" 
    ##  [31] "prtvtecz"  "prtvthee"  "prtvtefi"  "prtvtefr"  "prtvtghu"  "prtvclt1" 
    ##  [37] "prtvclt2"  "prtvclt3"  "prtvtfsi"  "prtvtesk"  "contplt"   "donprty"  
    ##  [43] "badge"     "sgnptit"   "pbldmna"   "bctprd"    "pstplonl"  "volunfp"  
    ##  [49] "clsprty"   "prtclebg"  "prtclbhr"  "prtclecz"  "prtclhee"  "prtclffi" 
    ##  [55] "prtclffr"  "prtclhhu"  "prtclclt"  "prtclfsi"  "prtclesk"  "prtdgcl"  
    ##  [61] "lrscale"   "stflife"   "stfeco"    "stfgov"    "stfdem"    "stfedu"   
    ##  [67] "stfhlth"   "gincdif"   "freehms"   "hmsfmlsh"  "hmsacld"   "euftf"    
    ##  [73] "lrnobed"   "loylead"   "imsmetn"   "imdfetn"   "impcntr"   "imbgeco"  
    ##  [79] "imueclt"   "imwbcnt"   "happy"     "sclmeet"   "inprdsc"   "sclact"   
    ##  [85] "crmvct"    "aesfdrk"   "health"    "hlthhmp"   "atchctr"   "atcherp"  
    ##  [91] "rlgblg"    "rlgdnm"    "rlgdnafi"  "rlgdnhu"   "rlgdnlt"   "rlgdnbsk" 
    ##  [97] "rlgblge"   "rlgdnme"   "rlgdeafi"  "rlgdehu"   "rlgdelt"   "rlgdebsk" 
    ## [103] "rlgdgr"    "rlgatnd"   "pray"      "dscrgrp"   "dscrrce"   "dscrntn"  
    ## [109] "dscrrlg"   "dscrlng"   "dscretn"   "dscrage"   "dscrgnd"   "dscrsex"  
    ## [115] "dscrdsb"   "dscroth"   "dscrdk"    "dscrref"   "dscrnap"   "dscrna"   
    ## [121] "ctzcntr"   "brncntr"   "cntbrthd"  "livecnta"  "lnghom1"   "lnghom2"  
    ## [127] "feethngr"  "facntr"    "fbrncntc"  "mocntr"    "mbrncntc"  "ccnthum"  
    ## [133] "ccrdprs"   "wrclmch"   "admrclc"   "testic34"  "testic35"  "testic36" 
    ## [139] "testic37"  "testic38"  "testic39"  "testic40"  "testic41"  "testic42" 
    ## [145] "vteurmmb"  "vteubcmb"  "fairelc"   "dfprtal"   "medcrgv"   "rghmgpr"  
    ## [151] "votedir"   "cttresa"   "gptpelc"   "gvctzpv"   "grdfinc"   "viepol"   
    ## [157] "wpestop"   "keydec"    "fairelcc"  "dfprtalc"  "medcrgvc"  "rghmgprc" 
    ## [163] "votedirc"  "cttresac"  "gptpelcc"  "gvctzpvc"  "grdfincc"  "viepolc"  
    ## [169] "wpestopc"  "keydecc"   "chpldm"    "chpldmi"   "chpldmc"   "stpldmi"  
    ## [175] "stpldmc"   "admit"     "showcv"    "impdema"   "impdemb"   "impdemc"  
    ## [181] "impdemd"   "impdeme"   "implvdm"   "accalaw"   "hhmmb"     "gndr"     
    ## [187] "gndr2"     "gndr3"     "gndr4"     "gndr5"     "gndr6"     "gndr7"    
    ## [193] "gndr8"     "gndr9"     "gndr10"    "gndr11"    "gndr12"    "gndr13"   
    ## [199] "yrbrn"     "agea"      "yrbrn2"    "yrbrn3"    "yrbrn4"    "yrbrn5"   
    ## [205] "yrbrn6"    "yrbrn7"    "yrbrn8"    "yrbrn9"    "yrbrn10"   "yrbrn11"  
    ## [211] "yrbrn12"   "yrbrn13"   "rshipa2"   "rshipa3"   "rshipa4"   "rshipa5"  
    ## [217] "rshipa6"   "rshipa7"   "rshipa8"   "rshipa9"   "rshipa10"  "rshipa11" 
    ## [223] "rshipa12"  "rshipa13"  "acchome"   "accwrk"    "accmove"   "accoth"   
    ## [229] "accnone"   "accref"    "accdk"     "accna"     "fampref"   "famadvs"  
    ## [235] "fampdf"    "mcclose"   "mcinter"   "mccoord"   "mcpriv"    "mcmsinf"  
    ## [241] "chldo12"   "gndro12a"  "gndro12b"  "ageo12"    "hhlio12"   "closeo12" 
    ## [247] "ttmino12"  "speako12"  "scrno12"   "phoneo12"  "como12"    "c19spo12" 
    ## [253] "c19mco12"  "livpnt"    "pntmofa"   "agepnt"    "hhlipnt"   "closepnt" 
    ## [259] "ttminpnt"  "speakpnt"  "scrnpnt"   "phonepnt"  "compnt"    "c19sppnt" 
    ## [265] "c19mcpnt"  "stfmjob"   "trdawrk"   "jbprtfp"   "pfmfdjba"  "dcsfwrka" 
    ## [271] "wrkhome"   "c19whome"  "c19wplch"  "wrklong"   "wrkresp"   "c19whacc" 
    ## [277] "mansupp"   "manhlp"    "manwrkpl"  "manspeak"  "manscrn"   "manphone" 
    ## [283] "mancom"    "teamfeel"  "wrkextra"  "colprop"   "colhlp"    "colspeak" 
    ## [289] "colscrn"   "colphone"  "colcom"    "c19spwrk"  "c19mcwrk"  "mcwrkhom" 
    ## [295] "ipcrtiv"   "imprich"   "ipeqopt"   "ipshabt"   "impsafe"   "impdiff"  
    ## [301] "ipfrule"   "ipudrst"   "ipmodst"   "ipgdtim"   "impfree"   "iphlppl"  
    ## [307] "ipsuces"   "ipstrgv"   "ipadvnt"   "ipbhprp"   "iprspot"   "iplylfr"  
    ## [313] "impenv"    "imptrad"   "impfun"    "testii1"   "testii2"   "testii3"  
    ## [319] "testii4"   "testii5"   "testii6"   "testii7"   "testii8"   "testii9"  
    ## [325] "secgrdec"  "scidecpb"  "admc19"    "panpriph"  "panmonpb"  "govpriph" 
    ## [331] "govmonpb"  "panfolru"  "panclobo"  "panresmo"  "gvhanc19"  "gvjobc19" 
    ## [337] "gveldc19"  "gvfamc19"  "hscopc19"  "gvbalc19"  "gvimpc19"  "gvconc19" 
    ## [343] "respc19"   "reshhc19"  "hapljc19"  "hapirc19"  "hapwrc19"  "hapfuc19" 
    ## [349] "hapfoc19"  "hapnoc19"  "hapnwc19"  "hapnpc19"  "haprec19"  "hapdkc19" 
    ## [355] "hapnac19"  "icvacc19"  "getavc19"  "getnvc19"  "vdcond"    "vdovexre" 
    ## [361] "vdtype"    "vdtpsvre"  "vdtpitre"  "vdtpscre"  "vdtpaure"  "vdtpvire" 
    ## [367] "vdtpoire"  "vdtpntre"  "vdtpapre"  "vdtprere"  "vdtpdkre"  "vdtpnare" 
    ## [373] "inwds"     "ainws"     "ainwe"     "binwe"     "cinwe"     "dinwe"    
    ## [379] "finwe"     "ginwe"     "hinwe"     "iinwe"     "kinwe"     "vinwe"    
    ## [385] "inwde"     "jinws"     "jinwe"     "inwtm"     "domain"    "prob"     
    ## [391] "stratum"   "psu"       "rshpsts"   "lvgptnea"  "dvrcdeva"  "marsts"   
    ## [397] "maritalb"  "chldhhe"   "domicil"   "edulvlb"   "eisced"    "edlvebg"  
    ## [403] "edlvehr"   "edlvdcz"   "edlvdee"   "edlvdfi"   "edlvdfr"   "edlvdahu" 
    ## [409] "edlvdlt"   "edlvesi"   "edlvdsk"   "eduyrs"    "pdwrk"     "edctn"    
    ## [415] "uempla"    "uempli"    "dsbld"     "rtrd"      "cmsrv"     "hswrk"    
    ## [421] "dngoth"    "dngref"    "dngdk"     "dngna"     "mainact"   "mnactic"  
    ## [427] "crpdwk"    "pdjobev"   "pdjobyr"   "emplrel"   "emplno"    "wrkctra"  
    ## [433] "estsz"     "jbspv"     "njbspv"    "wkdcorga"  "iorgact"   "wkhct"    
    ## [439] "wkhtot"    "nacer2"    "tporgwk"   "isco08"    "wrkac6m"   "uemp3m"   
    ## [445] "uemp12m"   "uemp5yr"   "mbtru"     "hincsrca"  "hinctnta"  "hincfel"  
    ## [451] "edulvlpb"  "eiscedp"   "edlvpebg"  "edlvpehr"  "edlvpdcz"  "edlvpdee" 
    ## [457] "edlvpdfi"  "edlvpdfr"  "edlvpdahu" "edlvpdlt"  "edlvpesi"  "edlvpdsk" 
    ## [463] "pdwrkp"    "edctnp"    "uemplap"   "uemplip"   "dsbldp"    "rtrdp"    
    ## [469] "cmsrvp"    "hswrkp"    "dngothp"   "dngdkp"    "dngnapp"   "dngrefp"  
    ## [475] "dngnap"    "mnactp"    "crpdwkp"   "isco08p"   "emprelp"   "wkhtotp"  
    ## [481] "edulvlfb"  "eiscedf"   "edlvfebg"  "edlvfehr"  "edlvfdcz"  "edlvfdee" 
    ## [487] "edlvfdfi"  "edlvfdfr"  "edlvfdahu" "edlvfdlt"  "edlvfesi"  "edlvfdsk" 
    ## [493] "emprf14"   "occf14b"   "edulvlmb"  "eiscedm"   "edlvmebg"  "edlvmehr" 
    ## [499] "edlvmdcz"  "edlvmdee"  "edlvmdfi"  "edlvmdfr"  "edlvmdahu" "edlvmdlt" 
    ## [505] "edlvmesi"  "edlvmdsk"  "emprm14"   "occm14b"   "atncrse"   "anctry1"  
    ## [511] "anctry2"   "regunit"   "region"

## Descriprive Stats & Basic Plots

When thinking about statistics we need to make a clear distinction
between the type of variables: continuous, categorical, etc.

    ## $label
    ## [1] "Age of respondent, calculated"
    ## 
    ## $format.spss
    ## [1] "F2.0"
    ## 
    ## $class
    ## [1] "haven_labelled" "vctrs_vctr"     "double"        
    ## 
    ## $labels
    ## Not available 
    ##           999

    ## [1] 50.88645

    ## [1] 18.4512

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   15.00   36.00   51.00   50.89   66.00   90.00     120

    ## Descriptive Statistics  
    ## dat$agea  
    ## Label: Age of respondent, calculated  
    ## N: 18060  
    ## 
    ##                         agea
    ## ----------------- ----------
    ##              Mean      50.89
    ##           Std.Dev      18.45
    ##               Min      15.00
    ##                Q1      36.00
    ##            Median      51.00
    ##                Q3      66.00
    ##               Max      90.00
    ##               MAD      22.24
    ##               IQR      30.00
    ##                CV       0.36
    ##          Skewness      -0.07
    ##       SE.Skewness       0.02
    ##          Kurtosis      -0.93
    ##           N.Valid   17940.00
    ##         Pct.Valid      99.34

![](Script_W1_files/figure-gfm/pressure-1.png)<!-- -->![](Script_W1_files/figure-gfm/pressure-2.png)<!-- -->

    ## $format.spss
    ## [1] "F2.0"

    ## 
    ##    1    2    3    4    5    6    7   55   77   88   99 
    ##  571 2159 2772 5956 1961 2010 2544   22   25   12   28

    ## $levels
    ## [1] "Less than lower secondary"        "Lower secondary"                 
    ## [3] "Lower tier upper secondary"       "Upper tier upper secondary"      
    ## [5] "Advanced vocational"              "Lower tertiary education (BA)"   
    ## [7] "Higher tertiary education (>=MA)" "Other"                           
    ## 
    ## $class
    ## [1] "factor"

    ## Frequencies  
    ## dat$educ  
    ## Type: Factor  
    ## 
    ##                                           Freq   % Valid   % Valid Cum.   % Total   % Total Cum.
    ## -------------------------------------- ------- --------- -------------- --------- --------------
    ##              Less than lower secondary     571      3.17           3.17      3.16           3.16
    ##                        Lower secondary    2159     12.00          15.17     11.95          15.12
    ##             Lower tier upper secondary    2772     15.40          30.58     15.35          30.47
    ##             Upper tier upper secondary    5956     33.10          63.67     32.98          63.44
    ##                    Advanced vocational    1961     10.90          74.57     10.86          74.30
    ##          Lower tertiary education (BA)    2010     11.17          85.74     11.13          85.43
    ##       Higher tertiary education (>=MA)    2544     14.14          99.88     14.09          99.52
    ##                                  Other      22      0.12         100.00      0.12          99.64
    ##                                   <NA>      65                               0.36         100.00
    ##                                  Total   18060    100.00         100.00    100.00         100.00

    ## Frequencies  
    ## dat$eisced  
    ## Type: Numeric  
    ## 
    ##                Freq   % Valid   % Valid Cum.   % Total   % Total Cum.
    ## ----------- ------- --------- -------------- --------- --------------
    ##           1     571     3.162          3.162     3.162          3.162
    ##           2    2159    11.955         15.116    11.955         15.116
    ##           3    2772    15.349         30.465    15.349         30.465
    ##           4    5956    32.979         63.444    32.979         63.444
    ##           5    1961    10.858         74.302    10.858         74.302
    ##           6    2010    11.130         85.432    11.130         85.432
    ##           7    2544    14.086         99.518    14.086         99.518
    ##          55      22     0.122         99.640     0.122         99.640
    ##          77      25     0.138         99.779     0.138         99.779
    ##          88      12     0.066         99.845     0.066         99.845
    ##          99      28     0.155        100.000     0.155        100.000
    ##        <NA>       0                              0.000        100.000
    ##       Total   18060   100.000        100.000   100.000        100.000

![](Script_W1_files/figure-gfm/pressure-3.png)<!-- -->![](Script_W1_files/figure-gfm/pressure-4.png)<!-- -->

    ## $label
    ## [1] "Gender"
    ## 
    ## $format.spss
    ## [1] "F1.0"
    ## 
    ## $class
    ## [1] "haven_labelled" "vctrs_vctr"     "double"        
    ## 
    ## $labels
    ##      Male    Female No answer 
    ##         1         2         9

    ##                                   
    ##                                    Male Female
    ##   Less than lower secondary         245    326
    ##   Lower secondary                   937   1222
    ##   Lower tier upper secondary       1460   1312
    ##   Upper tier upper secondary       2741   3215
    ##   Advanced vocational               828   1133
    ##   Lower tertiary education (BA)     767   1243
    ##   Higher tertiary education (>=MA) 1073   1471
    ##   Other                              16      6

    ## Cross-Tabulation, Row Proportions  
    ## educ * gender  
    ## Data Frame: dat  
    ## 
    ## ---------------------------------- -------- -------------- -------------- ----------------
    ##                                      gender           Male         Female            Total
    ##                               educ                                                        
    ##          Less than lower secondary             245 (42.9%)    326 (57.1%)     571 (100.0%)
    ##                    Lower secondary             937 (43.4%)   1222 (56.6%)    2159 (100.0%)
    ##         Lower tier upper secondary            1460 (52.7%)   1312 (47.3%)    2772 (100.0%)
    ##         Upper tier upper secondary            2741 (46.0%)   3215 (54.0%)    5956 (100.0%)
    ##                Advanced vocational             828 (42.2%)   1133 (57.8%)    1961 (100.0%)
    ##      Lower tertiary education (BA)             767 (38.2%)   1243 (61.8%)    2010 (100.0%)
    ##   Higher tertiary education (>=MA)            1073 (42.2%)   1471 (57.8%)    2544 (100.0%)
    ##                              Other              16 (72.7%)      6 (27.3%)      22 (100.0%)
    ##                               <NA>              33 (50.8%)     32 (49.2%)      65 (100.0%)
    ##                              Total            8100 (44.9%)   9960 (55.1%)   18060 (100.0%)
    ## ---------------------------------- -------- -------------- -------------- ----------------

    ## Cross-Tabulation, Column Proportions  
    ## educ * gender  
    ## Data Frame: dat  
    ## 
    ## ---------------------------------- -------- --------------- ---------------- ----------------
    ##                                      gender            Male           Female            Total
    ##                               educ                                                           
    ##          Less than lower secondary             245 (  3.0%)    326 (  3.27%)     571 (  3.2%)
    ##                    Lower secondary             937 ( 11.6%)   1222 ( 12.27%)    2159 ( 12.0%)
    ##         Lower tier upper secondary            1460 ( 18.0%)   1312 ( 13.17%)    2772 ( 15.3%)
    ##         Upper tier upper secondary            2741 ( 33.8%)   3215 ( 32.28%)    5956 ( 33.0%)
    ##                Advanced vocational             828 ( 10.2%)   1133 ( 11.38%)    1961 ( 10.9%)
    ##      Lower tertiary education (BA)             767 (  9.5%)   1243 ( 12.48%)    2010 ( 11.1%)
    ##   Higher tertiary education (>=MA)            1073 ( 13.2%)   1471 ( 14.77%)    2544 ( 14.1%)
    ##                              Other              16 (  0.2%)      6 (  0.06%)      22 (  0.1%)
    ##                               <NA>              33 (  0.4%)     32 (  0.32%)      65 (  0.4%)
    ##                              Total            8100 (100.0%)   9960 (100.00%)   18060 (100.0%)
    ## ---------------------------------- -------- --------------- ---------------- ----------------

    ## Descriptive Statistics  
    ## agea  
    ## Label: Age of respondent, calculated  
    ## N: 8100  
    ## 
    ##               Mean   Std.Dev     Min   Median     Max   N.Valid   Pct.Valid
    ## ---------- ------- --------- ------- -------- ------- --------- -----------
    ##       agea   49.78     18.23   15.00    50.00   90.00   8042.00       99.28
    ## 
    ## N: 9960  
    ## 
    ##               Mean   Std.Dev     Min   Median     Max   N.Valid   Pct.Valid
    ## ---------- ------- --------- ------- -------- ------- --------- -----------
    ##       agea   51.78     18.58   15.00    52.00   90.00   9898.00       99.38

    ## Descriptive Statistics  
    ## agea  
    ## Label: Age of respondent, calculated  
    ## N: 8100  
    ## 
    ##               Mean   Std.Dev     Min   Median     Max   N.Valid   Pct.Valid
    ## ---------- ------- --------- ------- -------- ------- --------- -----------
    ##       agea   49.78     18.23   15.00    50.00   90.00   8042.00       99.28

    ## Descriptive Statistics  
    ## agea  
    ## Label: Age of respondent, calculated  
    ## N: 9960  
    ## 
    ##               Mean   Std.Dev     Min   Median     Max   N.Valid   Pct.Valid
    ## ---------- ------- --------- ------- -------- ------- --------- -----------
    ##       agea   51.78     18.58   15.00    52.00   90.00   9898.00       99.38

## Regression

The main goal of regression analysis is to see how a set of independent
variables explain the variation of a dependent variables. In its
simplest form, we would have a multiple linear regression of the form:

$Y_{i} = \beta_{0} + \beta_{1}X_{1i}+...+\beta_{k}X_{ki} + \varepsilon_{i}$

# Assumptions OLS:

1)  Normality
2)  Exogeneity
3)  Lack of perfect multicollinearity
4)  Homoscedasticity
5)  Independence of errors
6)  Linearity

<!-- -->

    ## # A tibble: 17,684 × 4
    ##    trstplt             agea      gender educ                            
    ##    <dbl+lbl>           <dbl+lbl> <fct>  <fct>                           
    ##  1 3 [3]               76        Female Upper tier upper secondary      
    ##  2 6 [6]               43        Male   Lower tertiary education (BA)   
    ##  3 3 [3]               50        Female Higher tertiary education (>=MA)
    ##  4 0 [No trust at all] 51        Female Upper tier upper secondary      
    ##  5 0 [No trust at all] 70        Male   Higher tertiary education (>=MA)
    ##  6 0 [No trust at all] 31        Female Upper tier upper secondary      
    ##  7 5 [5]               40        Male   Upper tier upper secondary      
    ##  8 1 [1]               48        Male   Upper tier upper secondary      
    ##  9 2 [2]               71        Male   Upper tier upper secondary      
    ## 10 0 [No trust at all] 71        Male   Less than lower secondary       
    ## # … with 17,674 more rows

    ## 
    ## Call:
    ## lm(formula = trstplt ~ agea + gender + educ, data = dat_reg1)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -3.8659 -2.2062 -0.1776  1.7935  6.8317 
    ## 
    ## Coefficients:
    ##                                       Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)                           3.576878   0.129951  27.525  < 2e-16 ***
    ## agea                                  0.000189   0.001055   0.179 0.857799    
    ## genderFemale                          0.037566   0.038239   0.982 0.325924    
    ## educLower secondary                  -0.378481   0.121733  -3.109 0.001880 ** 
    ## educLower tier upper secondary       -0.198967   0.118272  -1.682 0.092531 .  
    ## educUpper tier upper secondary       -0.412535   0.113631  -3.630 0.000284 ***
    ## educAdvanced vocational               0.126097   0.122294   1.031 0.302509    
    ## educLower tertiary education (BA)     0.162153   0.123235   1.316 0.188259    
    ## educHigher tertiary education (>=MA)  0.234473   0.119669   1.959 0.050088 .  
    ## educOther                            -0.644147   0.559777  -1.151 0.249863    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 2.516 on 17674 degrees of freedom
    ## Multiple R-squared:  0.01117,    Adjusted R-squared:  0.01067 
    ## F-statistic: 22.19 on 9 and 17674 DF,  p-value: < 2.2e-16

    ## 
    ##    1    2    3    4 
    ## 1319 5469 7093 4137
