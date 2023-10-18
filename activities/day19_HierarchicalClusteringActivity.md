Hierarchical Clustering Activity
================
ECON 122
Day 19

## Clustering on incoming student characteristics

We will again look at the “classic” college data set of a random sample
of colleges and universities. This time we will look at CA **AND** MA
schools

``` r
> colleges <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/Colleges.csv")
> names(colleges)
 [1] "State"       "College"     "SATM"        "SATV"        "AppsReceive"
 [6] "AppsAccept"  "HStop10"     "HStop25"     "FullTime"    "Tuition"    
[11] "RoomBoard"   "Books"       "Ratio"       "Donate"      "Expend"     
[16] "GradRate"    "Type"        "AvgSalary"   "NumFaculty" 
> colleges2 <- colleges %>% filter(State %in% c("MA","CA"))
> table(colleges2$State)

CA MA 
21 19 
```

We will also focus on the proportion of the incoming class that is in
the top 10% or 25% of their HS class.

``` r
> coll_vars <- names(colleges2)[c(3,4,7,8)]
> coll_vars
[1] "SATM"    "SATV"    "HStop10" "HStop25"
> summary(colleges2[,coll_vars])
      SATM            SATV          HStop10         HStop25      
 Min.   :436.0   Min.   :390.0   Min.   : 1.00   Min.   : 19.00  
 1st Qu.:499.5   1st Qu.:451.5   1st Qu.:22.50   1st Qu.: 47.50  
 Median :547.5   Median :483.0   Median :36.50   Median : 69.50  
 Mean   :557.9   Mean   :502.7   Mean   :41.52   Mean   : 65.70  
 3rd Qu.:590.5   3rd Qu.:551.8   3rd Qu.:54.00   3rd Qu.: 86.25  
 Max.   :750.0   Max.   :660.0   Max.   :98.00   Max.   :100.00  
```

Let’s cluster schools by their incoming class characteristics.

#### Question 1

Why should we standardize the variables of interest before using a
clustering method?

#### Question 2

Standardize our four variables of interest and fit a hierarchical
clustering model. Plot the dendrogram with label names added.

#### Question 3

Which school seems most similar to University of San Francisco? Compare
the SAT and HS class variable values to verify your answer.

#### Question 4

What height would you have to cut this tree to create 3 clusters? Use
the `abline(h=)` function to add a cut line to the previous plot.

#### Question 5

Make 3 clusters and add them as characters to the data frame. Plot a
dendogram that identifies each cluster with a different color.

- Hint: Use `cutree`
- Hint: We can add cluster colors to the dendrogram using the
  `ColorDendrogram` function in the `sparcl` package.

``` r
> ColorDendrogram(coll_hc, y=colleges2$cluster_hc3, labels=colleges2$College, branchlength = 1.6)
```

#### Question 6

What are the characteristics of each cluster? Use either
`density curves` or `boxplots` for the `SAT` and `HS` variables. How
would you label the clusters in a way the general public would
understand?

#### Question 7

Do you prefer kmeans or hiearchical clustering? What are the pros and
cons?
