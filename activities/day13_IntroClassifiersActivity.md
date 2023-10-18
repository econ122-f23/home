Intro to Classifiers
================
ECON 122
Day 13

## Example: Predicting loan defaults

A loan will default if either criteria below is met:

- *Duration is longer than 2 years and credit amount is greater than
  10,000 DM.*
- *Duration is 2 years or less and credit amount is less than 2200 DM.*

``` r
> loans <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/CreditData.csv")
> loans <- loans %>%
+   mutate(c1 = Duration.in.month > 24 & Credit.amount > 10000, 
+          c2 = Duration.in.month <= 24 & loans$Credit.amount < 2200, 
+          prediction = ifelse(c1 | c2, "BadLoan", "GoodLoan") ) 
> (conf.mat <- with(loans,table(Good.Loan, prediction)))
          prediction
Good.Loan  BadLoan GoodLoan
  BadLoan      137      163
  GoodLoan     355      345
```

### Question 1:

What is the confusion matrix if you used 36 months as your duration
criteria value? What are the model evaluation stats (accuracy,
precision, recall)?

## Random guessing

Suppose you have ![n](https://latex.codecogs.com/png.latex?n "n")
observations that you want to predict. We know that
![n_0](https://latex.codecogs.com/png.latex?n_0 "n_0") are actually
failures and ![n_1](https://latex.codecogs.com/png.latex?n_1 "n_1") are
actually successes.

### Question 2

You flip a fair coin to determine successes (head) and failures (tails)
for each case. Write down the confusion matrix that you would expect
under this scenario. I.e. what are the expected numbers in each of the
four cells?

### Question 3

Use your confusion matrix from question 2 to compute accuracy,
precision, and recall for this random (fair) guessing prediction method.

### Question 4

Repeat 2 and 3 but you predict a success with probability
![p](https://latex.codecogs.com/png.latex?p "p") and a failure with
probability ![1-p](https://latex.codecogs.com/png.latex?1-p "1-p").

### Question 5

Repeat 2 and 3 but you predict a success with 100% probability!
(i.e. all cases are predicted to be a success).
