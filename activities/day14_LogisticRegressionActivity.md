Logistic Regression
================
ECON 122
Day 14

## Comparing models

In this activity you will be comparing the model we used in lecture
(model 1) with a slightly more flexible model that uses more variables
(model 2). I’ll add the code to replicate what we did in lecture

##### Load data and create a factor for good loan/bad loan

``` r
> loans <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/CreditData.csv")
> loans <- loans %>% 
+   mutate(Default = recode_factor(Good.Loan, GoodLoan = "NoDefault",BadLoan = "Default" ))
```

##### Fit the model

``` r
> default.glm1 <- glm(Default ~ log(Credit.amount) + Duration.in.month, 
+                     family="binomial", data=loans)
> default.glm1

Call:  glm(formula = Default ~ log(Credit.amount) + Duration.in.month, 
    family = "binomial", data = loans)

Coefficients:
       (Intercept)  log(Credit.amount)   Duration.in.month  
          -0.70026            -0.13969             0.04333  

Degrees of Freedom: 999 Total (i.e. Null);  997 Residual
Null Deviance:      1222 
Residual Deviance: 1176     AIC: 1182
```

##### Add probabilities and evaluation rates using 0.5 as the cutoff

``` r
> loans <- loans %>%
+   mutate(probs1 = predict(default.glm1, type="response"), 
+          prediction1 = ifelse( probs1 >= .5, "Default", "NoDefault") ) 
> 
> stats <- loans %>% summarize(accuracy = mean(Default == prediction1), 
+             precision = sum(Default == "Default" &  prediction1 == "Default")/sum(prediction1 == "Default"),
+             recall = sum(Default == "Default" & 
+                      prediction1 == "Default")/sum(Default == "Default"))
> stats
# A tibble: 1 × 3
  accuracy precision recall
     <dbl>     <dbl>  <dbl>
1    0.709     0.565   0.13
```

### Question 1: Fit a logistic model that includes the following predictors (3-6 are new)

1.  log credit amount (`log(Credit.amount)`)
2.  Loan duration (`Duration.in.month`)
3.  age of loan holder (`Age.in.years`)
4.  credit history (`Credit.history`)
5.  loan purpose (`Purpose`)
6.  present employment (`Present.employment.since`)

### Question 2: Calculate accuracy, precision, and recall for the new model. How does it compare to the simpler model?

- **Note:** I’ve called the predicted probabilities for the simpler
  model `probs1` so something like `probs2` would make sense for your
  new model.

### Question 3: Plot the double density for model 1 and model 2 at the same time. How do the densities compare across the models? What does that tell you?

- **Hint**: Using the `gather` command on `probs1` and `probs2` may help
  you here.

### Question 4: Plot the ROC curve for both models on the same figure. What does the ROC model tell you about the relative performance of model 1 vs model 2?

- **Hint**: Create a performance object for the second model and use
  `bind_rows` to create one dataframe that has both models. Then when
  you plot the ROC curve, you can use `color=model` to distinguish
  between the two.

##### First, create ROC curve for model 1 (replicating what we did in lecture)

``` r
> preds_obj1 <- prediction(loans$probs1, loans$Default, label.ordering=c("NoDefault","Default"))
> perf_obj1 <- performance(preds_obj1, "tpr","fpr")
> perf_df1 <- data_frame(fpr=unlist(perf_obj1@x.values),
+                        tpr= unlist(perf_obj1@y.values),
+                        threshold=unlist(perf_obj1@alpha.values), 
+                        model="GLM1")
Warning: `data_frame()` was deprecated in tibble 1.1.0.
ℹ Please use `tibble()` instead.
This warning is displayed once every 8 hours.
Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
generated.
```
