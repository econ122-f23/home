Network Graphs Activity
================
ECON 122
Day 20

## Country Migration

The following dataset contains migration counts for decades between 1960
and 2000 between the origin (`origincode`) and destination (`destcode`)
countries given in the data.

``` r
> MigrationFlows <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/MigrationFlows.csv")
> MigrationFlows
# A tibble: 107,184 × 8
   sex   destcode origincode  Y1960  Y1970  Y1980  Y1990  Y2000
   <chr> <chr>    <chr>       <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
 1 Male  FRA      AFG          1471     29     55     91    923
 2 Male  FRA      DZA        521679 723746 794288 861691 425229
 3 Male  FRA      AUS         14614   1906   1483    903   9168
 4 Male  FRA      AUT         12375   4861   4686   2761   7764
 5 Male  FRA      AZE           188      4     20     12    118
 6 Male  FRA      BLR           390      0     26     88    245
 7 Male  FRA      BLZ           623     22     25     38    391
 8 Male  FRA      BEN           233   5736   4409    397    166
 9 Male  FRA      ALB         15967     17      4   3586  10017
10 Male  FRA      ASM             0      0      0      0      0
# … with 107,174 more rows
```

#### Question 1

Create a subsetted version of this data, called `MigrationFlowsF`, that
only contains migration counts of `females` `over 1000` in 2000. How
many cases are in this dataset?

#### Question 2

The data frame you created in question 1 can be used as the edge list
for a migration network in 2000. Create a `network` object that makes a
directional network with edges indicating migration from the origin
country to a destination country. How many nodes are in this network?
How many edges?

#### Question 3

Visualizing all countries at once is likely to be overwhelming. Let’s
analyze the following countries:

``` r
> smallerGroup <- c("USA","CAN","MEX","BRA","CHN","JPN","GBR","PRT")
```

Draw a plot of this network with `ggnetwork` and `ggplot` with vertex
labels added. What patterns do you see in the plot?

- **Note:** Because we have arrows going into and out of the same
  countries, using `curvature=0.2` in `geom_edges` helps better
  visualize the flows
- **Note:** Setting a seed `set.seed(x)` can help to keep your network
  figyre constant each time you run your code

#### Question 4

Is `Y2000`, migration in 2000, an edge or vertex attribute? Add it to
your smaller network from question 3 using the
`set.xxxx.attribute(network, "name", values)`.

#### Question 5

Modify your plot from question 3 so that edge width is a function of
migration flow size. Use the `size` option in `geom_edges`. What
patterns do you notice about migration flows?

- **Note:** Coloring each `edge` by `country of origin` is helpful to
  visualize the flows better

#### Question 6

For a given country, imagine we want to focus on where the inflows of
migrants are coming from. Create a new `edge attribute` that calculates
for each destination country the ratio of inward migration from relative
to all inward migration. Do you learn anything different from this
Figure relative to Q5?
