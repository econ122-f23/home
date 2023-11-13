Kmeans Clustering Activity
================
ECON 122
Day 18

## Clustering using Incoming student characteristics

We will look at a “classic” college data set of a random sample of
colleges and universities. For this activity we will focus on CA
colleges and universities.

``` r
> colleges <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/Colleges.csv")
> names(colleges)
 [1] "State"       "College"     "SATM"        "SATV"        "AppsReceive"
 [6] "AppsAccept"  "HStop10"     "HStop25"     "FullTime"    "Tuition"    
[11] "RoomBoard"   "Books"       "Ratio"       "Donate"      "Expend"     
[16] "GradRate"    "Type"        "AvgSalary"   "NumFaculty" 
> colleges2 <- colleges %>% filter(State=="CA")
```

Instead of focusing just on `SATM` and `SATV` we will also consider
`AppsReceive`.

``` r
> coll_vars <- names(colleges2)[c(3,4,5)]
> coll_vars
[1] "SATM"        "SATV"        "AppsReceive"
> summary(colleges2[,coll_vars])
      SATM            SATV        AppsReceive   
 Min.   :472.0   Min.   :425.0   Min.   :  346  
 1st Qu.:531.0   1st Qu.:456.0   1st Qu.:  959  
 Median :549.0   Median :490.0   Median : 1916  
 Mean   :575.3   Mean   :511.4   Mean   : 2704  
 3rd Qu.:590.0   3rd Qu.:560.0   3rd Qu.: 3037  
 Max.   :750.0   Max.   :660.0   Max.   :12229  
```

First, let’s plot the schools against two of the variables `SATM` and
`SATV`

``` r
> set.seed(7)
> ggplot(colleges2, aes(SATM,SATV)) + 
+   geom_point() + 
+   geom_text(aes(label=College),position=position_jitter(width=0,height=20),size=2.5) + 
+   coord_fixed(xlim = c(400, 800),ylim=c(400,665)) 
```

![](day18_KmeansClusteringActivity_Solution_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

#### Question 1

Just by looking at the figure above, can you predict roughly what 3
different clusters would look like when using k-means clustering?

**Ans:**

> A naive answer is that we would expect the clusters to form in groups
> roughly according to `SATM` and `SATV` groups. However, since we are
> including `AppsReceive` into our criteria it’s not clear how this will
> affect the clusters.

#### Question 2

Use k-means clustering with a `k=3` to cluster the data based on `SATM`,
`SATV`, and `AppsReceive`. Add the cluster assignment to your dataset
and plot the same figure as above but with colors representing the
clusters. Do the clusters match your predictions from Question 1? Why or
why not?

**Ans:**

``` r
> km_out <- kmeans(colleges2[,coll_vars], centers=3, nstart=20)
> colleges2 <- colleges2 %>% mutate(cluster_assign = as.character(km_out$cluster))
> 
> set.seed(7)
> ggplot(colleges2, aes(SATM,SATV,color=cluster_assign)) + 
+   geom_point() + 
+   geom_text(aes(label=College),position=position_jitter(width=0,height=20),size=2.5) + 
+   coord_fixed(xlim = c(400, 800),ylim=c(400,665)) 
```

![](day18_KmeansClusteringActivity_Solution_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

> The clusters don’t correspond that well to the spatial position of
> points in the `SATM` and `SATV` dimension. This is likely due to the
> fact that `AppsReceive` has a much larger scale and so the distance
> metric will be dominated by that variable. The clusters will represent
> distance in this dimension. We can see this by plotting the clusters
> along the `AppsReceive` dimension on the y-axis

``` r
> set.seed(7)
> ggplot(colleges2, aes(SATM,AppsReceive,color=cluster_assign)) + 
+   geom_point() + 
+   geom_text(aes(label=College),position=position_jitter(width=0,height=20),size=2.5) 
```

![](day18_KmeansClusteringActivity_Solution_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

#### Question 3

One reason the clustering might have been different from your
expectations is because we haven’t appropiately scaled the data. Do all
the variables have similar scale? Re-do Question 2 using an appropiate
scaling. Are the clusters closer to what you were expecting?

**Ans:**

> The output below shows `AppsReceive` has a larger scale than the other
> variables. If we scale all the variables, the clusters make more sense
> when looking at `SATM` vs `SATV`

``` r
> summary(colleges2[,coll_vars])
      SATM            SATV        AppsReceive   
 Min.   :472.0   Min.   :425.0   Min.   :  346  
 1st Qu.:531.0   1st Qu.:456.0   1st Qu.:  959  
 Median :549.0   Median :490.0   Median : 1916  
 Mean   :575.3   Mean   :511.4   Mean   : 2704  
 3rd Qu.:590.0   3rd Qu.:560.0   3rd Qu.: 3037  
 Max.   :750.0   Max.   :660.0   Max.   :12229  
```

``` r
> km_out_std <- kmeans(scale(colleges2[,coll_vars]), centers=3, nstart=20)
> colleges2 <- colleges2 %>% mutate(cluster_assign_std = as.character(km_out_std$cluster))
> 
> set.seed(7)
> ggplot(colleges2, aes(SATM,SATV,color=cluster_assign_std)) + 
+   geom_point() + 
+   geom_text(aes(label=College),position=position_jitter(width=0,height=20),size=2.5) + 
+   coord_fixed(xlim = c(400, 800),ylim=c(400,665)) 
```

![](day18_KmeansClusteringActivity_Solution_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

#### Question 4:

Even after standardizing the data, the clusters may seem visually off
when plotted on the `SATM` vs `SATV` scale. Why is that? What are the
characeristics of the schools that seem to not fit well?

- Hint: Recreating your plot but using `AppsReceive` on the y-axis may
  help explain the clusters.

**Ans:**

> Plotting `AppsReceive` against `SATM` shows that the clustering takes
> into account both `SATM` and `AppsReceive` more equally once we
> standardize

``` r
> set.seed(7)
> ggplot(colleges2, aes(SATM,AppsReceive,color=cluster_assign_std)) + 
+   geom_point() + 
+   geom_text(aes(label=College),position=position_jitter(width=0,height=20),size=2.5) 
```

![](day18_KmeansClusteringActivity_Solution_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

#### Question 5:

Up to now we’ve been using clusters of 3 to split up the data. Using the
standardized data, create a plot that shows how the values of `withinss`
(within cluster sum of squared residuals) vary as `k` varies from 1 to
20.

Using this plot, what do you think the optimal level of `k` is? Why?

> k=3 actually seems pretty optimal. That is where we see the “elbow” in
> this plot. Higher cluster values will decrease the SS but not by
> enough to make it worth while (just adds complexity).

``` r
> set.seed(77)
> km_twss <- sapply(1:20, function(x) kmeans(scale(colleges2[,coll_vars]), centers=x, nstart=20)$tot.withinss)
> km_twss
 [1] 60.000000000 29.119041186 13.435175861  7.726492505  5.550642360
 [6]  3.903824680  3.098815878  2.176129636  1.543231061  1.191565244
[11]  0.921694856  0.680171926  0.519860726  0.405488747  0.333245108
[16]  0.226655250  0.101708303  0.047443037  0.009564464  0.004448399
> ggplot(data_frame(k=1:20,km_twss), aes(x=k, y=km_twss)) + geom_point() + geom_line()
Warning: `data_frame()` was deprecated in tibble 1.1.0.
ℹ Please use `tibble()` instead.
This warning is displayed once every 8 hours.
Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
generated.
```

![](day18_KmeansClusteringActivity_Solution_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->
