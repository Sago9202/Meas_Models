Session 1: Intro to R programming
================
Laura Eberlein, Santiago Gómez-Echeverry & Dimitris Pavlopoulos
2022-10-31

- <a href="#1-getting-to-know-r" id="toc-1-getting-to-know-r">1 Getting to
  know R</a>
  - <a href="#11-first-steps-in-r" id="toc-11-first-steps-in-r">1.1 First
    steps in R</a>
  - <a href="#12-variables" id="toc-12-variables">1.2 Variables</a>
  - <a href="#13-data-structures" id="toc-13-data-structures">1.3 Data
    Structures</a>
- <a href="#exercise-1" id="toc-exercise-1">Exercise 1:</a>
- <a href="#2-importing-and-saving-data"
  id="toc-2-importing-and-saving-data">2 Importing and saving data</a>
  - <a href="#21-working-directory" id="toc-21-working-directory">2.1
    Working directory</a>
- <a href="#3-descriptive-statistics" id="toc-3-descriptive-statistics">3
  Descriptive Statistics</a>

# 1 Getting to know R

In this practical session, we introduce working with R. We illustrate
some basic functionality and help you familiarize yourself with RStudio.

## 1.1 First steps in R

Let’s go through some of the basics of R. We can use R as a simple
calculator.

``` r
2+6
```

    ## [1] 8

Now that we know how to use the + sign for addition, let’s try some
other mathematical operations such as subtraction (-), multiplication
(\*), and division (/).

``` r
10-4
```

    ## [1] 6

``` r
5*3
```

    ## [1] 15

``` r
8/2
```

    ## [1] 4

In R, we always use objects and functions. Functions are what other
programs call commands, a set of instructions that carry out a specific
task. Functions often require some input and generate some output. For
example, instead of using the + operator for addition, we can use the
sum function to add two or more numbers.

``` r
sum(2,6)
```

    ## [1] 8

If you want to have a look at the online documentation of each function
in R, you can use help() or ?function.

``` r
help(sum)
```

    ## starting httpd help server ... done

``` r
?sum
```

In the example above, 2 and 6 are the inputs and 8 is the output. A
function always requires the use of parenthesis or round brackets ().
Inputs to the function are called arguments and go inside the brackets.
The output of a function is displayed on the screen. If we want to save
the results of our output, we can assign it to an object. To assign our
result to an object, we use the assignment operator “\<-”. If we want to
save our results of sum(2,6), we could do the following:

``` r
myresult <- sum(2,6)
myresult
```

    ## [1] 8

The line above creates a new object called myresult in our environment
and saves the result of the function in it.

*Sequences* Sequences are often needed when manipulating data. For
instance, you might want to perform an operation on the first 10 rows of
a data set so we need a way to select the range we are interested in.
There are two ways to create a sequence. Let’s try to create a sequence
of numbers from 1 to 10 using the two methods:

1)  Using the colon : operator. If you’re familiar with spreadsheets
    then you migh have already used : to select cells, for example
    A1:A20. In R, you can use the : to create a sequence in a similar
    fashion:
2)  Using the seq() function. The seq function has a number of options
    which control how the sequence is generated. For example, to create
    a sequence from 0 to 100 in increments of 5, we can use the optional
    “by” argument.

``` r
1:10
```

    ##  [1]  1  2  3  4  5  6  7  8  9 10

``` r
# Alternatively
seq(from = 1,to = 10)
```

    ##  [1]  1  2  3  4  5  6  7  8  9 10

``` r
# Including some jumps on the sequence
seq(from = 0,to = 100, by = 5)
```

    ##  [1]   0   5  10  15  20  25  30  35  40  45  50  55  60  65  70  75  80  85  90
    ## [20]  95 100

## 1.2 Variables

There are basically four types of variables in R:

1.  Numeric (Numbers)
2.  Character (Text, sometimes also called ‘strings’)
3.  Factor (Categorical data)
4.  Logical (True or False)

*Numeric*

``` r
x <- 20
x = 20 # There are different ways of assigning objects
x
```

    ## [1] 20

``` r
class(x) # View the class of the value assigned to x
```

    ## [1] "numeric"

*Character*

Textual data (recognizable by the quotes), either as single characters,
entire words, or even full texts.

``` r
chr <- "Some random text"
chr
```

    ## [1] "Some random text"

``` r
xt <- "20"
xt
```

    ## [1] "20"

Run the code below and see what happens.

``` r
#sum(xt,x) # Why is there an error?
```

Naturally, you cannot perform math with character data. Using the wrong
data type will generally yield an error. You can convert the value to a
different type with the *as* command:

``` r
xt1 <- as.numeric(xt) # converts character into numeric
sum(xt1,x)
```

    ## [1] 40

*Factor*

Factors are variables in R which take on a limited number of different
values, and are employed to refer to categorical variables (nominal or
ordinal).

``` r
f <- as.factor(1:10)
f
```

    ##  [1] 1  2  3  4  5  6  7  8  9  10
    ## Levels: 1 2 3 4 5 6 7 8 9 10

``` r
fac <- factor(c("SPSS", "Stata", "R"))
fac
```

    ## [1] SPSS  Stata R    
    ## Levels: R SPSS Stata

Note that although factors seem like typical numbers, they are not meant
for standard algebra.

``` r
mean(f) 
```

    ## Warning in mean.default(f): argument is not numeric or logical: returning NA

    ## [1] NA

Ordered factors can be created by setting the argument ordered=T

``` r
software <- factor(fac, levels = fac, ordered = T)
software
```

    ## [1] SPSS  Stata R    
    ## Levels: SPSS < Stata < R

*Logical*

Logical is a factor that takes on the values TRUE (also abbreviated T)
and FALSE (F). Logical vectors can be used in mathematical operations:
TRUE is treated as 1 and FALSE as 0.

``` r
test <- ifelse(x<30,TRUE, FALSE)
test
```

    ## [1] TRUE

## 1.3 Data Structures

There are different data structures in R. In the following, we will look
at vectors and data frames.

*Vectors*

A vector in R is a sequence of one or more values of the same data type.
From a social science background, it is very similar to what we often
call a variable.

We can create a vector in R using the *c()* function, where c stands for
collect. A vector can have any of the data types discussed above.

``` r
age <- c(27, 21, 23, 24)
age
```

    ## [1] 27 21 23 24

``` r
master <- c("Sociology", "Psychology", "Economics", "Political Science")
master
```

    ## [1] "Sociology"         "Psychology"        "Economics"        
    ## [4] "Political Science"

*class()* returns the type of a variable or in fact any object in R.

``` r
class(age)
```

    ## [1] "numeric"

``` r
class(master)
```

    ## [1] "character"

Let’s see how many elements our vector contains using the length()
function.

``` r
length(age)
```

    ## [1] 4

Next, we access the first element in our vector. We use square brackets
to access a specific element. The number in the square brackets is the
vector element that we access.

``` r
age[2] # second vector element
```

    ## [1] 21

To access all elements except the first element, we use the *-*
operator.

``` r
age[-2] # all elements except the second one
```

    ## [1] 27 23 24

We can access elements 2 to 4 by using a colon.

``` r
age[2:4]
```

    ## [1] 21 23 24

Finally, we can also access two specific non-adjacent elements, by using
the collect function c().

``` r
age[c(2,4)] # second and fourth element
```

    ## [1] 21 24

*Data frame*

A data frame is an object that holds data in a tabular format similar to
how spreadsheets work. Variables are generally kept in columns and
observations are in rows. To create a data frame, we use the
*data.frame()* function.

``` r
dat <- data.frame(id = 1:4, 
                  age = age, 
                  gender = c("Male", "Female", "Male", "Female"),
                  master = master, 
                  score = 6:9)
dat
```

    ##   id age gender            master score
    ## 1  1  27   Male         Sociology     6
    ## 2  2  21 Female        Psychology     7
    ## 3  3  23   Male         Economics     8
    ## 4  4  24 Female Political Science     9

As you can see, we created a data frame by combining different vectors.
We gave a name to each vector, so the variable names in the dataset
correspond to our vector names.

We can see the names of variables in our dataset with the names
function.

``` r
colnames(dat)
```

    ## [1] "id"     "age"    "gender" "master" "score"

We can also check the variable types in our data by using the *str()*
function.

``` r
str(dat)
```

    ## 'data.frame':    4 obs. of  5 variables:
    ##  $ id    : int  1 2 3 4
    ##  $ age   : num  27 21 23 24
    ##  $ gender: chr  "Male" "Female" "Male" "Female"
    ##  $ master: chr  "Sociology" "Psychology" "Economics" "Political Science"
    ##  $ score : int  6 7 8 9

Maybe you have noticed the new data frame object in your global
environment window. You can view the dataset in the spreadsheet form
that we are all used to by clicking on the object name.

The data structure clearly implies that there is a relation between the
elements in the column vectors. In other words, that each row represents
a case. In our example, these cases are participants, and the columns
represent:

- the participant id
- demographic variables: age and gender
- their master studies
- grades

*Selecting rows, columns and elements - Subsetting*

Often we want to access certain observations (rows) or certain columns
(variables) or a combination of the two without looking at the entire
dataset all at once. A way to select one column of your data is to use
the dollar sign (\$).

``` r
dat$age # select the age column using the dollar sign
```

    ## [1] 27 21 23 24

Additionally, we can use square brackets to subset data frames. In
square brackets we put a row and a column coordinate separated by a
comma. The row coordinate goes first and the column coordinate second.
For example:

``` r
dat[3,2] # returns the third row and the second column of the data frame.
```

    ## [1] 23

If we leave the column coordinate empty this means we would like all
columns. So, data\[3,\] returns the third row of the dataset.

``` r
dat[3,] # Specific row
```

    ##   id age gender    master score
    ## 3  3  23   Male Economics     8

``` r
dat[,2] # Specific column
```

    ## [1] 27 21 23 24

If we leave the row coordinate empty, R returns the entire column.
data\[,2\] returns the second column of the dataset.

``` r
dat[,2]
```

    ## [1] 27 21 23 24

We can also select all columns but the second one:

``` r
dat[,-2]
```

    ##   id gender            master score
    ## 1  1   Male         Sociology     6
    ## 2  2 Female        Psychology     7
    ## 3  3   Male         Economics     8
    ## 4  4 Female Political Science     9

Or select only columns 1 and 4:

``` r
dat[,c(1,4)]
```

    ##   id            master
    ## 1  1         Sociology
    ## 2  2        Psychology
    ## 3  3         Economics
    ## 4  4 Political Science

If you are working with larger data sets, it is often useful to look at
the first columns in your data frame to get a better understanding of
it. Below we only want to look at the first two rows of our data:

``` r
dat[1:2,]
```

    ##   id age gender     master score
    ## 1  1  27   Male  Sociology     6
    ## 2  2  21 Female Psychology     7

A very useful additional trick is that you can use all the columns to
make comparisons. For example, we can use the gender column to look up
all elements for which the value is “Male”, and use this to select rows.

``` r
dat[dat$gender == "Male",]
```

    ##   id age gender    master score
    ## 1  1  27   Male Sociology     6
    ## 3  3  23   Male Economics     8

You can do the same selecting two columns:

``` r
dat[dat$gender == "Male" & dat$master == "Sociology",]
```

    ##   id age gender    master score
    ## 1  1  27   Male Sociology     6

We can also use a condition, for example whether the students in our
dataset passed the course.

``` r
dat[dat$score>6,]
```

    ##   id age gender            master score
    ## 2  2  21 Female        Psychology     7
    ## 3  3  23   Male         Economics     8
    ## 4  4  24 Female Political Science     9

And use these conditions to *create new variables*:

``` r
dat$pass <- dat$score>6
dat
```

    ##   id age gender            master score  pass
    ## 1  1  27   Male         Sociology     6 FALSE
    ## 2  2  21 Female        Psychology     7  TRUE
    ## 3  3  23   Male         Economics     8  TRUE
    ## 4  4  24 Female Political Science     9  TRUE

# Exercise 1:

With the selection techniques you already learned how to create a subset
of the data. Try to subset the data so that only students who passed
their studies are included. Assign this subset to a new name.

``` r
dat_new <- dat[dat$score>6,]
dat_new
```

    ##   id age gender            master score pass
    ## 2  2  21 Female        Psychology     7 TRUE
    ## 3  3  23   Male         Economics     8 TRUE
    ## 4  4  24 Female Political Science     9 TRUE

``` r
write.csv(dat_new, file = "test_data.csv")
```

# 2 Importing and saving data

## 2.1 Working directory

Each R sessions is connected to a particular folder on your computer,
your working directory. We can check where we are by using the function
getwd() which stands for “get the current working directory”. This
resulting path is where the data will be stored.

    ## [1] "C:/Users/Startklar/OneDrive - Vrije Universiteit Amsterdam/Measurement Models in Quantitative Research/3 - Practicals/Meas_Models/Meas_Models"

*2.2 Saving data*

To save a data frame we can use write.csv() that assign a data.frame
object to a CSV-file. THis function takes an object and file path as
input.

``` r
write.csv(dat, file = "test_data.csv") # saves our previously created data frame
```

Have a look at the working directory you are currently using. After
running the previous R code, it should contain a csv file called
“test_data.csv”.

*2.3 Importing data*

Before you load the dataset into R, you first download it and save it
locally in your preferred working directory. We often load existing data
sets into R for analysis. Data come in many different file formats such
as .csv, .sav, .dta, etc.

You probably noticed that we installed a package before importing our
data. Once we have installed a package, we need to load it with the
library() function. After loading the package, we have access to the
package functions.

Let’s have a first look at our data:

``` r
dim(dat) # returns row and column count
```

    ## [1] 18060   513

``` r
nrow(dat) # returns the number of rows
```

    ## [1] 18060

``` r
ncol(dat) # returns the number of columns
```

    ## [1] 513

``` r
# Let’s take a quick peek at the first 10 observations to see what the dataset looks like. By default the head() function returns the first 6 rows, but let’s tell it to return the first 10 rows instead.

head(dat, n = 10) # returns the first parts of a data frame 
```

    ## # A tibble: 10 × 513
    ##    name    essro…¹ edition prodd…²  idno cntry    pweight dweight nwspol netus…³
    ##    <chr>     <dbl> <chr>   <chr>   <dbl> <chr+lb>   <dbl>   <dbl> <dbl+> <dbl+l>
    ##  1 ESS10e…      10 1.3     4.10.2… 10002 BG [Bul…   0.218   1.03   80    1 [Nev…
    ##  2 ESS10e…      10 1.3     4.10.2… 10006 BG [Bul…   0.218   0.879  63    5 [Eve…
    ##  3 ESS10e…      10 1.3     4.10.2… 10009 BG [Bul…   0.218   1.01  390    5 [Eve…
    ##  4 ESS10e…      10 1.3     4.10.2… 10024 BG [Bul…   0.218   0.955  60    5 [Eve…
    ##  5 ESS10e…      10 1.3     4.10.2… 10027 BG [Bul…   0.218   0.841 120    5 [Eve…
    ##  6 ESS10e…      10 1.3     4.10.2… 10048 BG [Bul…   0.218   0.946  60    5 [Eve…
    ##  7 ESS10e…      10 1.3     4.10.2… 10053 BG [Bul…   0.218   1.01   30    5 [Eve…
    ##  8 ESS10e…      10 1.3     4.10.2… 10055 BG [Bul…   0.218   1.03   70    5 [Eve…
    ##  9 ESS10e…      10 1.3     4.10.2… 10059 BG [Bul…   0.218   0.991  60    1 [Nev…
    ## 10 ESS10e…      10 1.3     4.10.2… 10061 BG [Bul…   0.218   1.05   60    1 [Nev…
    ## # … with 503 more variables: netustm <dbl+lbl>, ppltrst <dbl+lbl>,
    ## #   pplfair <dbl+lbl>, pplhlp <dbl+lbl>, polintr <dbl+lbl>, psppsgva <dbl+lbl>,
    ## #   actrolga <dbl+lbl>, psppipla <dbl+lbl>, cptppola <dbl+lbl>,
    ## #   trstprl <dbl+lbl>, trstlgl <dbl+lbl>, trstplc <dbl+lbl>, trstplt <dbl+lbl>,
    ## #   trstprt <dbl+lbl>, trstep <dbl+lbl>, trstun <dbl+lbl>, trstsci <dbl+lbl>,
    ## #   vote <dbl+lbl>, prtvtebg <dbl+lbl>, prtvtbhr <dbl+lbl>, prtvtecz <dbl+lbl>,
    ## #   prtvthee <dbl+lbl>, prtvtefi <dbl+lbl>, prtvtefr <dbl+lbl>, …

``` r
summary(dat[,(colnames(dat)=="name" | colnames(dat)=="agea" | colnames(dat)=="eisced" | colnames(dat)=="gndr")])
```

    ##      name                gndr            agea           eisced      
    ##  Length:18060       Min.   :1.000   Min.   :15.00   Min.   : 1.000  
    ##  Class :character   1st Qu.:1.000   1st Qu.:36.00   1st Qu.: 3.000  
    ##  Mode  :character   Median :2.000   Median :51.00   Median : 4.000  
    ##                     Mean   :1.551   Mean   :50.89   Mean   : 4.633  
    ##                     3rd Qu.:2.000   3rd Qu.:66.00   3rd Qu.: 6.000  
    ##                     Max.   :2.000   Max.   :90.00   Max.   :99.000  
    ##                                     NA's   :120

In cases with large data sets like this we might want to *select a
subset of variables* that we want to work with.

    ## [1] 18060     3

    ## # A tibble: 6 × 3
    ##   agea      eisced gndr      
    ##   <dbl+lbl>  <dbl> <dbl+lbl> 
    ## 1 76             4 2 [Female]
    ## 2 43             6 1 [Male]  
    ## 3 50             7 2 [Female]
    ## 4 51             4 2 [Female]
    ## 5 70             7 1 [Male]  
    ## 6 31             4 2 [Female]

# 3 Descriptive Statistics

When talking about descriptive statistics, we first need to know what
type of variable each item is.

*Continuous*

For *continuous* items, the type of descriptive statistics we present
are related to central tendency and variability measures. We will use
the descr() function from the summarytools package.

Be aware that this function will give you results if you use them with
categorical variables, but these would not be meaningful. From the
selected variables the only ones that are truly continuous are age.

``` r
#install.packages("summarytools")
library(summarytools)
descr(dat2$agea)
```

    ## Descriptive Statistics  
    ## dat2$agea  
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

This function provides a lot of useful information. The N.valid is the
total non missing answers for the variable, followed by a series of
descriptive statistics like the mean, standard deviation, median,
minimum, maximum, and others. You can also transpose the table,
depending on which direction you prefer.

``` r
descr(dat2$agea, transpose = T)
```

    ## Descriptive Statistics  
    ## dat2$agea  
    ## Label: Age of respondent, calculated  
    ## N: 18060  
    ## 
    ##               Mean   Std.Dev     Min      Q1   Median      Q3     Max     MAD     IQR     CV
    ## ---------- ------- --------- ------- ------- -------- ------- ------- ------- ------- ------
    ##       agea   50.89     18.45   15.00   36.00    51.00   66.00   90.00   22.24   30.00   0.36
    ## 
    ## Table: Table continues below
    ## 
    ##  
    ## 
    ##              Skewness   SE.Skewness   Kurtosis    N.Valid   Pct.Valid
    ## ---------- ---------- ------------- ---------- ---------- -----------
    ##       agea      -0.07          0.02      -0.93   17940.00       99.34

You can also get the descriptive statistics of a continuous variable by
group:

``` r
desc <- stby(data = dat2[,c("agea")], 
     INDICES   = dat2$gndr, 
     FUN = descr, 
     stats = "common", 
     transpose = TRUE)
desc
```

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

*Missing values*

Using the function above, we saw that our variable of interest (age) has
a total of 17940 non missing answers. Since our data has 1806 entries,
this means that the variable contains some missing values that R refers
to as *“NA”*. There are different ways of dealing with NAs. In the
following, we will delete missing values to keep the rectangular
structure of our data.This means, when we delete a missing value from
one variable, we delete it for the entire row of the dataset.

First, we introduce the is.na() function. We supply a vector to the
function and it checks for every element, whether it is missing or not.
R returns true or false. Let’s use the function on our variable.

``` r
head(is.na(dat2$agea), n = 10) # There are too many values, let's just check the first 10 cases
```

    ##  [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE

To see the amount of missing values (NA in R) in our variable, we can
combine is.na() with the table() function.

``` r
table(is.na(dat2$agea)) # We have 120 missing values in our variable
```

    ## 
    ## FALSE  TRUE 
    ## 17940   120

``` r
# Note: If you run the mean function on a continuous variable which contains missing values, R will get you an error
mean(dat2$agea) 
```

    ## [1] NA

``` r
# use na.rm=TRUE to exclude missing values 
mean(dat2$agea, na.rm = TRUE) 
```

    ## [1] 50.88645

``` r
sd(dat2$agea, na.rm = TRUE)
```

    ## [1] 18.4512

So, our variable has 120 missing values. Our dataset has 18060 rows.
Check your global environment to confirm this or use the nrow()
function. If we delete all missing values from agea, our dataset will
lose 120 rows.

Before we delete missing values, we introduce the which() function. It
returns the row indexes (the rows in the dataset) where some condition
is true. So if we use which() and is.na(), we get the row numbers in our
dataset where values are missing on agea.

    ##   [1]   525   707   717   756   791   870   966  1156  1380  1419  1532  1602
    ##  [13]  1730  1781  1876  1915  1931  1956  2254  2364  2471  2484  8721  9483
    ##  [25]  9727 10340 10349 10357 10394 10425 10427 10449 10458 10489 10521 10525
    ##  [37] 10537 10616 10653 10673 10696 10761 10783 10859 10929 10968 11030 11038
    ##  [49] 11081 11111 11121 11136 11219 11316 11329 11374 11467 11484 11548 11621
    ##  [61] 11624 11660 11676 11683 11705 11759 11762 11769 11772 11848 11853 16648
    ##  [73] 16671 16691 16704 16741 16836 16953 16966 16980 16997 17014 17089 17104
    ##  [85] 17137 17156 17172 17200 17215 17245 17275 17333 17434 17468 17507 17515
    ##  [97] 17526 17567 17576 17590 17601 17602 17609 17610 17614 17622 17664 17734
    ## [109] 17753 17768 17769 17774 17783 17842 17862 17890 17947 17953 17981 18035

We said that our dataset will lose 120 rows. Let’s use the length()
function to confirm that this is the case.

    ## [1] 120

As we can see, we have indeed identified 120 rows that we would like to
delete from our dataset.

We now delete the rows with missing values on age by overwriting our
original dataset with a new dataset that is a copy of the old without
missing values on age. To subset our dataset, we use the square
brackets. We can use the *!* operator, which means *“not”*. So the
function returns “TRUE” if an observation is not missing.

Confirm that our new dataset (dat2) has 17940 rows remaining.

*Categorical*

For categorical variables the mean and previously presented statistics
are not meaningful. We need to describe them in a different way. For
this we will use the summarytools package and focus on the variables
education and gender.

    ## $format.spss
    ## [1] "F2.0"

    ## 
    ##    1    2    3    4    5    6    7   55   77   88   99 
    ##  569 2151 2749 5911 1958 2001 2525   21   25   12   18

    ## $levels
    ## [1] "Less than lower secondary"        "Lower secondary"                 
    ## [3] "Lower tier upper secondary"       "Upper tier upper secondary"      
    ## [5] "Advanced vocational"              "Lower tertiary education (BA)"   
    ## [7] "Higher tertiary education (>=MA)" "Other"                           
    ## 
    ## $class
    ## [1] "factor"

    ## $label
    ## [1] "Gender"
    ## 
    ## $format.spss
    ## [1] "F1.0"
    ## 
    ## $labels
    ##      Male    Female No answer 
    ##         1         2         9 
    ## 
    ## $class
    ## [1] "haven_labelled" "vctrs_vctr"     "double"

    ##                                   
    ##                                    Male Female
    ##   Less than lower secondary         286    281
    ##   Lower secondary                   929   1217
    ##   Lower tier upper secondary       1180   1552
    ##   Upper tier upper secondary       2635   3257
    ##   Advanced vocational               896   1053
    ##   Lower tertiary education (BA)     878   1124
    ##   Higher tertiary education (>=MA) 1172   1341
    ##   Other                               6     15

*Frequency tables*

The freq() function generates frequency tables with counts, proportions,
as well as missing data information.

    ## Frequencies  
    ## dat2$educ  
    ## Type: Factor  
    ## 
    ##                                           Freq   % Valid   % Valid Cum.   % Total   % Total Cum.
    ## -------------------------------------- ------- --------- -------------- --------- --------------
    ##              Less than lower secondary     567      3.18           3.18      3.16           3.16
    ##                        Lower secondary    2146     12.04          15.22     11.96          15.12
    ##             Lower tier upper secondary    2732     15.33          30.55     15.23          30.35
    ##             Upper tier upper secondary    5892     33.06          63.61     32.84          63.19
    ##                    Advanced vocational    1949     10.94          74.55     10.86          74.06
    ##          Lower tertiary education (BA)    2002     11.23          85.78     11.16          85.22
    ##       Higher tertiary education (>=MA)    2513     14.10          99.88     14.01          99.23
    ##                                  Other      21      0.12         100.00      0.12          99.34
    ##                                   <NA>     118                               0.66         100.00
    ##                                  Total   17940    100.00         100.00    100.00         100.00

    ## ### Frequencies  
    ## #### dat2$educ  
    ## **Type:** Factor  
    ## 
    ## |                               &nbsp; |  Freq | % Valid | % Valid Cum. | % Total | % Total Cum. |
    ## |-------------------------------------:|------:|--------:|-------------:|--------:|-------------:|
    ## |        **Less than lower secondary** |   567 |    3.18 |         3.18 |    3.16 |         3.16 |
    ## |                  **Lower secondary** |  2146 |   12.04 |        15.22 |   11.96 |        15.12 |
    ## |       **Lower tier upper secondary** |  2732 |   15.33 |        30.55 |   15.23 |        30.35 |
    ## |       **Upper tier upper secondary** |  5892 |   33.06 |        63.61 |   32.84 |        63.19 |
    ## |              **Advanced vocational** |  1949 |   10.94 |        74.55 |   10.86 |        74.06 |
    ## |    **Lower tertiary education (BA)** |  2002 |   11.23 |        85.78 |   11.16 |        85.22 |
    ## | **Higher tertiary education (>=MA)** |  2513 |   14.10 |        99.88 |   14.01 |        99.23 |
    ## |                            **Other** |    21 |    0.12 |       100.00 |    0.12 |        99.34 |
    ## |                           **\<NA\>** |   118 |         |              |    0.66 |       100.00 |
    ## |                            **Total** | 17940 |  100.00 |       100.00 |  100.00 |       100.00 |
    ## 
    ## #### dat2$gender  
    ## **Type:** Factor  
    ## 
    ## |     &nbsp; |  Freq | % Valid | % Valid Cum. | % Total | % Total Cum. |
    ## |-----------:|------:|--------:|-------------:|--------:|-------------:|
    ## |   **Male** |  8042 |   44.83 |        44.83 |   44.83 |        44.83 |
    ## | **Female** |  9898 |   55.17 |       100.00 |   55.17 |       100.00 |
    ## | **\<NA\>** |     0 |         |              |    0.00 |       100.00 |
    ## |  **Total** | 17940 |  100.00 |       100.00 |  100.00 |       100.00 |

We can also use the same function, and provide multiple variables at
once, getting the frequency tables for each specific variable.

    ## ### Frequencies  
    ## #### dat2$educ  
    ## **Type:** Factor  
    ## 
    ## |                               &nbsp; |  Freq | % Valid | % Valid Cum. | % Total | % Total Cum. |
    ## |-------------------------------------:|------:|--------:|-------------:|--------:|-------------:|
    ## |        **Less than lower secondary** |   567 |    3.18 |         3.18 |    3.16 |         3.16 |
    ## |                  **Lower secondary** |  2146 |   12.04 |        15.22 |   11.96 |        15.12 |
    ## |       **Lower tier upper secondary** |  2732 |   15.33 |        30.55 |   15.23 |        30.35 |
    ## |       **Upper tier upper secondary** |  5892 |   33.06 |        63.61 |   32.84 |        63.19 |
    ## |              **Advanced vocational** |  1949 |   10.94 |        74.55 |   10.86 |        74.06 |
    ## |    **Lower tertiary education (BA)** |  2002 |   11.23 |        85.78 |   11.16 |        85.22 |
    ## | **Higher tertiary education (>=MA)** |  2513 |   14.10 |        99.88 |   14.01 |        99.23 |
    ## |                            **Other** |    21 |    0.12 |       100.00 |    0.12 |        99.34 |
    ## |                           **\<NA\>** |   118 |         |              |    0.66 |       100.00 |
    ## |                            **Total** | 17940 |  100.00 |       100.00 |  100.00 |       100.00 |
    ## 
    ## #### dat2$gender  
    ## **Type:** Factor  
    ## 
    ## |     &nbsp; |  Freq | % Valid | % Valid Cum. | % Total | % Total Cum. |
    ## |-----------:|------:|--------:|-------------:|--------:|-------------:|
    ## |   **Male** |  8042 |   44.83 |        44.83 |   44.83 |        44.83 |
    ## | **Female** |  9898 |   55.17 |       100.00 |   55.17 |       100.00 |
    ## | **\<NA\>** |     0 |         |              |    0.00 |       100.00 |
    ## |  **Total** | 17940 |  100.00 |       100.00 |  100.00 |       100.00 |

*Cross-tables*

For categorical variables, if we want to estimate frequency tables
across multiple other groups, we estimate cross-tables. These present
the frequency of variable 1 at each level of variable 2, and vice versa,
depending on which direction you want to read the table.

To do this we use the function *ctable()*. Here we see the cross-table
between gender and education level. For this the main 2 arguments we
have to provide are 2 categorical variables of interest. You also
include the prop argument, which specifies which proportions you want to
show. In this first example we include don’t include any:

    ## Cross-Tabulation, Row Proportions  
    ## educ * gender  
    ## Data Frame: dat2  
    ## 
    ## ---------------------------------- -------- -------------- -------------- ----------------
    ##                                      gender           Male         Female            Total
    ##                               educ                                                        
    ##          Less than lower secondary             286 (50.4%)    281 (49.6%)     567 (100.0%)
    ##                    Lower secondary             929 (43.3%)   1217 (56.7%)    2146 (100.0%)
    ##         Lower tier upper secondary            1180 (43.2%)   1552 (56.8%)    2732 (100.0%)
    ##         Upper tier upper secondary            2635 (44.7%)   3257 (55.3%)    5892 (100.0%)
    ##                Advanced vocational             896 (46.0%)   1053 (54.0%)    1949 (100.0%)
    ##      Lower tertiary education (BA)             878 (43.9%)   1124 (56.1%)    2002 (100.0%)
    ##   Higher tertiary education (>=MA)            1172 (46.6%)   1341 (53.4%)    2513 (100.0%)
    ##                              Other               6 (28.6%)     15 (71.4%)      21 (100.0%)
    ##                               <NA>              60 (50.8%)     58 (49.2%)     118 (100.0%)
    ##                              Total            8042 (44.8%)   9898 (55.2%)   17940 (100.0%)
    ## ---------------------------------- -------- -------------- -------------- ----------------

Here we include column proportions:

    ## Cross-Tabulation, Column Proportions  
    ## educ * gender  
    ## Data Frame: dat2  
    ## 
    ## ---------------------------------- -------- ---------------- --------------- ----------------
    ##                                      gender             Male          Female            Total
    ##                               educ                                                           
    ##          Less than lower secondary             286 (  3.56%)    281 (  2.8%)     567 (  3.2%)
    ##                    Lower secondary             929 ( 11.55%)   1217 ( 12.3%)    2146 ( 12.0%)
    ##         Lower tier upper secondary            1180 ( 14.67%)   1552 ( 15.7%)    2732 ( 15.2%)
    ##         Upper tier upper secondary            2635 ( 32.77%)   3257 ( 32.9%)    5892 ( 32.8%)
    ##                Advanced vocational             896 ( 11.14%)   1053 ( 10.6%)    1949 ( 10.9%)
    ##      Lower tertiary education (BA)             878 ( 10.92%)   1124 ( 11.4%)    2002 ( 11.2%)
    ##   Higher tertiary education (>=MA)            1172 ( 14.57%)   1341 ( 13.5%)    2513 ( 14.0%)
    ##                              Other               6 (  0.07%)     15 (  0.2%)      21 (  0.1%)
    ##                               <NA>              60 (  0.75%)     58 (  0.6%)     118 (  0.7%)
    ##                              Total            8042 (100.00%)   9898 (100.0%)   17940 (100.0%)
    ## ---------------------------------- -------- ---------------- --------------- ----------------
