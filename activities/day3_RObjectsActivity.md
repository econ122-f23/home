R Objects Activity
================
ECON 122
Day 3

## Objects used in this handout:

``` r
> x <- c(8,2,1,3)
> loans <- read.csv("https://raw.githubusercontent.com/mgelman/data/master/CreditData.csv")
> tweets<- read.csv("https://raw.githubusercontent.com/mgelman/data/master/TrumpTweetData.csv")
> x.mat2 <- cbind(x,2*x)
> x.df <- data.frame(x=x,double.x=x*2)
> my.list <- list(myVec=x, myDf=x.df, myString=c("hi","bye"))
```

### Question 1: data types

- What data type is `x`? What data type is `loans$Duration.in.month`?
- What data type is the vector `c(x, loans$Duration.in.month)`?
- What data type is the vector `c(x,"NA")`?

### Question 2: subsetting and coercion

- How can we get an `x` vector with entries 1 and 2 without using the
  numbers 1 and 2?
- How can we reverse the order of entries in `x`?
- What does `which(x < 5)` equal?
- What does `sum(c(TRUE,FALSE,TRUE,FALSE))` equal?
- What does `sum(x[c(TRUE,FALSE,TRUE,FALSE)])` equal?
- What does `sum(x < 5)` equal?
- What does `sum(x[x < 5])` equal?
- Why does `dim(x.mat2[1:2,1])` return `NULL` while
  `dim(x.mat2[1:2,1:2])` returns a dimension?

### Question 3: Data frames

``` r
> str(tweets$text)
 chr [1:1512] "My economic policy speech will be carried live at 12:15 P.M. Enjoy!" ...
```

- The data set `TrumpTweetData.csv` contains data collected on about
  1500 Trump tweets. The variable `text` contains the text of the
  selected tweets. After reading data in with `read.csv`, R thinks the
  `text` variable is a factor. Does this make sense? (e.g. would you
  treat this as a categorical grouping variable in any analysis?)
- Use **two methods** to find the `text` of the 180th tweet in the Trump
  data.
- What is the class of the `attributes` of the data frame `tweets`?

### Question 4: Lists

- Using `my.list`, show three ways to write one command that gives the
  3rd entry of variable `x` in data frame `myDf`
- What class of object does the command `my.list[3]` return?
- What class of object does the command `my.list[[3]]` return?
- What class of object does the command `unlist(my.list)` return? Why
  are all the entries `character`s?

### Question 5: Loans revisited

- Give meaning to the following statistical summaries of the loans data
  from the test-assignment (interpret the numbers given!):
  - `mean(loans$Good.Loan == "BadLoan")`
  - `mean(loans$Duration.in.month <= 24)`
  - `mean(loans$Duration.in.month[loans$Good.Loan == "BadLoan"] <= 24)`
- Explain what the following `ifelse` command produces.

``` r
> loans$pred.Default1 <- ifelse(loans$Duration.in.month > 24 & loans$Credit.amount > 10000, "predBad", "predGood")
> head(loans[, c("Duration.in.month","Credit.amount","pred.Default1")], 10)
   Duration.in.month Credit.amount pred.Default1
1                  6          1169      predGood
2                 48          5951      predGood
3                 12          2096      predGood
4                 42          7882      predGood
5                 24          4870      predGood
6                 36          9055      predGood
7                 24          2835      predGood
8                 36          6948      predGood
9                 12          3059      predGood
10                30          5234      predGood
```

- Explain what the following `ifelse` command produces.

``` r
> loans$pred.Default <- ifelse(loans$Duration.in.month <= 24 & loans$Credit.amount < 2200, "predBad", loans$pred.Default1)
> head(loans[, c("Duration.in.month","Credit.amount","pred.Default1","pred.Default")], 10)
   Duration.in.month Credit.amount pred.Default1 pred.Default
1                  6          1169      predGood      predBad
2                 48          5951      predGood     predGood
3                 12          2096      predGood      predBad
4                 42          7882      predGood     predGood
5                 24          4870      predGood     predGood
6                 36          9055      predGood     predGood
7                 24          2835      predGood     predGood
8                 36          6948      predGood     predGood
9                 12          3059      predGood     predGood
10                30          5234      predGood     predGood
```

- What data type do the `ifelse` commands above produce (factor or
  character)?

### Question 6: Functions

``` r
> MeanSD <- function(x,plot=FALSE,...)
+ {
+   mean.x <- mean(x,...)
+   sd.x <- sd(x,...)
+   if (plot) 
+     hist(x)
+   return(list(Mean=mean.x,SD=sd.x))
+ }
```

- Use the `MeanSD` function to get mean, sd and histogram for
  `loans$Duration.in.month`
- Why does the first command below return NA’s while the second returns
  mean and SD?

``` r
> MeanSD(c(1,2,3,4,NA))
$Mean
[1] NA

$SD
[1] NA
> MeanSD(c(1,2,3,4,NA), na.rm=TRUE)
$Mean
[1] 2.5

$SD
[1] 1.290994
```

- Change the function above to also include the median in it’s
  statistical summary output.
