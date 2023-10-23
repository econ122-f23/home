Intro to Classifiers - solution
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
+   mutate(c1 = Duration.in.month > 36 & Credit.amount > 10000, 
+          c2 = Duration.in.month <= 36 & loans$Credit.amount < 2200, 
+          prediction = ifelse(c1 | c2, "BadLoan", "GoodLoan") ) 
> (conf.mat <- table(loans$Good.Loan, loans$prediction))
          
           BadLoan GoodLoan
  BadLoan      140      160
  GoodLoan     354      346
```

#### Question 1:

What is the confusion matrix if you used 36 months as your duration
criteria value? What are the model evaluation stats (accuracy,
precision, recall)?

#### *Answer:*

``` r
> (140+346)/1000 # accuracy
[1] 0.486
> 140/(140 + 354) # precision
[1] 0.2834008
> 140/(140+160) # recall
[1] 0.4666667
> loans %>% summarize(
+             accuracy = mean(Good.Loan == prediction), 
+             precision = sum(Good.Loan == "BadLoan" &  
+                               prediction == "BadLoan")/sum(prediction == "BadLoan"),
+             recall = sum(Good.Loan == "BadLoan" & 
+                      prediction == "BadLoan")/sum(Good.Loan == "BadLoan"))
# A tibble: 1 × 3
  accuracy precision recall
     <dbl>     <dbl>  <dbl>
1    0.486     0.283  0.467
```

## Random guessing

Suppose you have ![n](https://latex.codecogs.com/png.latex?n "n")
observations that you want to predict. We know that
![n_0](https://latex.codecogs.com/png.latex?n_0 "n_0") are actually
failures and ![n_1](https://latex.codecogs.com/png.latex?n_1 "n_1") are
actually successes.

#### Question 2

You flip a fair coin to determine successes (head) and failures (tails)
for each case. Write down the confusion matrix that you would expect
under this scenario. I.e. what are the expected numbers in each of the
four cells?

#### *Answer:*

Of all ![n](https://latex.codecogs.com/png.latex?n "n") cases, half will
be predicted to be failures and half success with a fair coin flip
predicting outcomes. So

![\hat{n}\_0 = \hat{n}\_1 = \dfrac{n}{2}](https://latex.codecogs.com/png.latex?%5Chat%7Bn%7D_0%20%3D%20%5Chat%7Bn%7D_1%20%3D%20%5Cdfrac%7Bn%7D%7B2%7D "\hat{n}_0 = \hat{n}_1 = \dfrac{n}{2}")

Using the same logic, half of the actual failures will be successes and
failures:

![TN = FP = \dfrac{n_0}{2}](https://latex.codecogs.com/png.latex?TN%20%3D%20FP%20%3D%20%5Cdfrac%7Bn_0%7D%7B2%7D "TN = FP = \dfrac{n_0}{2}")

and half of the actual successes will be successes and failures:

![FN = TP = \dfrac{n_1}{2}](https://latex.codecogs.com/png.latex?FN%20%3D%20TP%20%3D%20%5Cdfrac%7Bn_1%7D%7B2%7D "FN = TP = \dfrac{n_1}{2}")

| result             | predicted fail                                                                                                                          | predicted success                                                                                                                       | total                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|
| fail (negative)    | ![TN=\dfrac{n_0}{2}](https://latex.codecogs.com/png.latex?TN%3D%5Cdfrac%7Bn_0%7D%7B2%7D "TN=\dfrac{n_0}{2}")                            | ![FP=\dfrac{n_0}{2}](https://latex.codecogs.com/png.latex?FP%3D%5Cdfrac%7Bn_0%7D%7B2%7D "FP=\dfrac{n_0}{2}")                            | ![n_0](https://latex.codecogs.com/png.latex?n_0 "n_0") |
| success (positive) | ![FN= \dfrac{n_1}{2}](https://latex.codecogs.com/png.latex?FN%3D%20%5Cdfrac%7Bn_1%7D%7B2%7D "FN= \dfrac{n_1}{2}")                       | ![TP= \dfrac{n_1}{2}](https://latex.codecogs.com/png.latex?TP%3D%20%5Cdfrac%7Bn_1%7D%7B2%7D "TP= \dfrac{n_1}{2}")                       | ![n_1](https://latex.codecogs.com/png.latex?n_1 "n_1") |
| total              | ![\hat{n}\_0= \dfrac{n}{2}](https://latex.codecogs.com/png.latex?%5Chat%7Bn%7D_0%3D%20%5Cdfrac%7Bn%7D%7B2%7D "\hat{n}_0= \dfrac{n}{2}") | ![\hat{n}\_1= \dfrac{n}{2}](https://latex.codecogs.com/png.latex?%5Chat%7Bn%7D_1%3D%20%5Cdfrac%7Bn%7D%7B2%7D "\hat{n}_1= \dfrac{n}{2}") | ![n](https://latex.codecogs.com/png.latex?n "n")       |

#### Question 3

Use your confusion matrix from question 2 to compute accuracy,
precision, and recall for this random (fair) guessing prediction method.

#### *Answer:*

With a fair coin flip predicting successes, the accuracy will be 50%.

![accuracy = \dfrac{TN + TP}{n} = \dfrac{0.5n_0 + 0.5n_1}{n} = 0.5 \dfrac{n_0+n_1}{n} = 0.5](https://latex.codecogs.com/png.latex?accuracy%20%3D%20%5Cdfrac%7BTN%20%2B%20TP%7D%7Bn%7D%20%3D%20%5Cdfrac%7B0.5n_0%20%2B%200.5n_1%7D%7Bn%7D%20%3D%200.5%20%5Cdfrac%7Bn_0%2Bn_1%7D%7Bn%7D%20%3D%200.5 "accuracy = \dfrac{TN + TP}{n} = \dfrac{0.5n_0 + 0.5n_1}{n} = 0.5 \dfrac{n_0+n_1}{n} = 0.5")

Precision will be equal to the rate of successes in the sample since 50%
of the successes are correctly predicted and 50% of the overall sample
is predicted to be successes:

![precision = \dfrac{TP}{\hat{n}\_1} = \dfrac{0.5n_1}{0.5n} =  \dfrac{n_1}{n}](https://latex.codecogs.com/png.latex?precision%20%3D%20%5Cdfrac%7BTP%7D%7B%5Chat%7Bn%7D_1%7D%20%3D%20%5Cdfrac%7B0.5n_1%7D%7B0.5n%7D%20%3D%20%20%5Cdfrac%7Bn_1%7D%7Bn%7D "precision = \dfrac{TP}{\hat{n}_1} = \dfrac{0.5n_1}{0.5n} =  \dfrac{n_1}{n}")

Recall will be 50% since that is the rate at which we correctly predict
successes:

![Recall = \dfrac{TP}{n_1} = \dfrac{0.5n_1}{n_1} =  0.5](https://latex.codecogs.com/png.latex?Recall%20%3D%20%5Cdfrac%7BTP%7D%7Bn_1%7D%20%3D%20%5Cdfrac%7B0.5n_1%7D%7Bn_1%7D%20%3D%20%200.5 "Recall = \dfrac{TP}{n_1} = \dfrac{0.5n_1}{n_1} =  0.5")

#### Question 4

Repeat 2 and 3 but you predict a success with probability
![p](https://latex.codecogs.com/png.latex?p "p") and a failure with
probability ![1-p](https://latex.codecogs.com/png.latex?1-p "1-p").

#### *Answer:*

Of all ![n](https://latex.codecogs.com/png.latex?n "n") cases,
![p](https://latex.codecogs.com/png.latex?p "p") will be the proportion
of successes and ![1-p](https://latex.codecogs.com/png.latex?1-p "1-p")
the proportion of failures

![\hat{n}\_1 = pn \\\\\\ \\\hat{n}\_0 = (1-p)n](https://latex.codecogs.com/png.latex?%5Chat%7Bn%7D_1%20%3D%20pn%20%5C%20%5C%20%5C%20%20%5C%20%5Chat%7Bn%7D_0%20%3D%20%281-p%29n "\hat{n}_1 = pn \ \ \  \ \hat{n}_0 = (1-p)n")

Of all ![n_0](https://latex.codecogs.com/png.latex?n_0 "n_0") failures,
![p](https://latex.codecogs.com/png.latex?p "p") will be the proportion
of successes and ![1-p](https://latex.codecogs.com/png.latex?1-p "1-p")
the proportion of failures

![TN = (1-p)n_0 \\\\\\\\FP = pn_0](https://latex.codecogs.com/png.latex?TN%20%3D%20%281-p%29n_0%20%5C%20%5C%20%5C%20%5C%20FP%20%3D%20pn_0 "TN = (1-p)n_0 \ \ \ \ FP = pn_0")

Of all ![n_1](https://latex.codecogs.com/png.latex?n_1 "n_1") successes,
![p](https://latex.codecogs.com/png.latex?p "p") will be the proportion
of successes and ![1-p](https://latex.codecogs.com/png.latex?1-p "1-p")
the proportion of failures

![FN = (1-p)n_1 \\\\\\\\TP = pn_1](https://latex.codecogs.com/png.latex?FN%20%3D%20%281-p%29n_1%20%5C%20%5C%20%5C%20%5C%20TP%20%3D%20pn_1 "FN = (1-p)n_1 \ \ \ \ TP = pn_1")

| result             | predicted fail                                                                                                  | predicted success                                                                               | total                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|--------------------------------------------------------|
| fail (negative)    | ![TN=(1-p)n_0](https://latex.codecogs.com/png.latex?TN%3D%281-p%29n_0 "TN=(1-p)n_0")                            | ![FP=pn_0](https://latex.codecogs.com/png.latex?FP%3Dpn_0 "FP=pn_0")                            | ![n_0](https://latex.codecogs.com/png.latex?n_0 "n_0") |
| success (positive) | ![FN= (1-p)n_1](https://latex.codecogs.com/png.latex?FN%3D%20%281-p%29n_1 "FN= (1-p)n_1")                       | ![TP= pn_1](https://latex.codecogs.com/png.latex?TP%3D%20pn_1 "TP= pn_1")                       | ![n_1](https://latex.codecogs.com/png.latex?n_1 "n_1") |
| total              | ![\hat{n}\_0= (1-p)n](https://latex.codecogs.com/png.latex?%5Chat%7Bn%7D_0%3D%20%281-p%29n "\hat{n}_0= (1-p)n") | ![\hat{n}\_1= pn](https://latex.codecogs.com/png.latex?%5Chat%7Bn%7D_1%3D%20pn "\hat{n}_1= pn") | ![n](https://latex.codecogs.com/png.latex?n "n")       |

With a probability ![p](https://latex.codecogs.com/png.latex?p "p")
predicting successes, the accuracy will be a weighted average of the
rates of successes and failures.

![accuracy = \dfrac{TN + TP}{n} = \dfrac{(1-p)n_0 + pn_1}{n} = (1-p)\dfrac{n_0}{n} + p\dfrac{n_1}{n}](https://latex.codecogs.com/png.latex?accuracy%20%3D%20%5Cdfrac%7BTN%20%2B%20TP%7D%7Bn%7D%20%3D%20%5Cdfrac%7B%281-p%29n_0%20%2B%20pn_1%7D%7Bn%7D%20%3D%20%281-p%29%5Cdfrac%7Bn_0%7D%7Bn%7D%20%2B%20p%5Cdfrac%7Bn_1%7D%7Bn%7D "accuracy = \dfrac{TN + TP}{n} = \dfrac{(1-p)n_0 + pn_1}{n} = (1-p)\dfrac{n_0}{n} + p\dfrac{n_1}{n}")

Precision will be equal to the rate of successes in the sample since
![p](https://latex.codecogs.com/png.latex?p "p") proportion of the
successes are correctly predicted and
![p](https://latex.codecogs.com/png.latex?p "p") proportion of the
overall sample is predicted to be successes:

![precision = \dfrac{TP}{\hat{n}\_1} = \dfrac{pn_1}{pn} =  \dfrac{n_1}{n}](https://latex.codecogs.com/png.latex?precision%20%3D%20%5Cdfrac%7BTP%7D%7B%5Chat%7Bn%7D_1%7D%20%3D%20%5Cdfrac%7Bpn_1%7D%7Bpn%7D%20%3D%20%20%5Cdfrac%7Bn_1%7D%7Bn%7D "precision = \dfrac{TP}{\hat{n}_1} = \dfrac{pn_1}{pn} =  \dfrac{n_1}{n}")

Recall will be
![100p](https://latex.codecogs.com/png.latex?100p "100p")% since that is
the rate at which we correctly predict successes:

![Recall = \dfrac{TP}{n_1} = \dfrac{pn_1}{n_1} =  p](https://latex.codecogs.com/png.latex?Recall%20%3D%20%5Cdfrac%7BTP%7D%7Bn_1%7D%20%3D%20%5Cdfrac%7Bpn_1%7D%7Bn_1%7D%20%3D%20%20p "Recall = \dfrac{TP}{n_1} = \dfrac{pn_1}{n_1} =  p")

#### Question 5

Repeat 2 and 3 but you predict a success with 100% probability!
(i.e. all cases are predicted to be a success).

#### *Answer:*

This is question 5 with
![p=1](https://latex.codecogs.com/png.latex?p%3D1 "p=1") so

| result             | predicted fail                                                                               | predicted success                                                                            | total                                                  |
|--------------------|----------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|--------------------------------------------------------|
| fail (negative)    | ![TN=0](https://latex.codecogs.com/png.latex?TN%3D0 "TN=0")                                  | ![FP=n_0](https://latex.codecogs.com/png.latex?FP%3Dn_0 "FP=n_0")                            | ![n_0](https://latex.codecogs.com/png.latex?n_0 "n_0") |
| success (positive) | ![FN= 0](https://latex.codecogs.com/png.latex?FN%3D%200 "FN= 0")                             | ![TP= n_1](https://latex.codecogs.com/png.latex?TP%3D%20n_1 "TP= n_1")                       | ![n_1](https://latex.codecogs.com/png.latex?n_1 "n_1") |
| total              | ![\hat{n}\_0= 0](https://latex.codecogs.com/png.latex?%5Chat%7Bn%7D_0%3D%200 "\hat{n}_0= 0") | ![\hat{n}\_1= n](https://latex.codecogs.com/png.latex?%5Chat%7Bn%7D_1%3D%20n "\hat{n}_1= n") | ![n](https://latex.codecogs.com/png.latex?n "n")       |

With a probability ![p](https://latex.codecogs.com/png.latex?p "p")
predicting successes, the accuracy will be the rate of successes in the
sample:

![accuracy = \dfrac{TN + TP}{n} = \dfrac{0 + n_1}{n} = \dfrac{n_1}{n}](https://latex.codecogs.com/png.latex?accuracy%20%3D%20%5Cdfrac%7BTN%20%2B%20TP%7D%7Bn%7D%20%3D%20%5Cdfrac%7B0%20%2B%20n_1%7D%7Bn%7D%20%3D%20%5Cdfrac%7Bn_1%7D%7Bn%7D "accuracy = \dfrac{TN + TP}{n} = \dfrac{0 + n_1}{n} = \dfrac{n_1}{n}")

Precision will be equal to the rate of successes in the sample:

![precision = \dfrac{TP}{\hat{n}\_1} = \dfrac{n_1}{n}](https://latex.codecogs.com/png.latex?precision%20%3D%20%5Cdfrac%7BTP%7D%7B%5Chat%7Bn%7D_1%7D%20%3D%20%5Cdfrac%7Bn_1%7D%7Bn%7D "precision = \dfrac{TP}{\hat{n}_1} = \dfrac{n_1}{n}")

Recall will be ![100](https://latex.codecogs.com/png.latex?100 "100")%
since that is the rate at which we correctly predict successes:

![Recall = \dfrac{TP}{n_1} = \dfrac{n_1}{n_1} =  1](https://latex.codecogs.com/png.latex?Recall%20%3D%20%5Cdfrac%7BTP%7D%7Bn_1%7D%20%3D%20%5Cdfrac%7Bn_1%7D%7Bn_1%7D%20%3D%20%201 "Recall = \dfrac{TP}{n_1} = \dfrac{n_1}{n_1} =  1")
