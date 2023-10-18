Network Stats Activity
================
ECON 122

## Country Migration

Let’s use the same dataset from the previous activity that contains
migration counts for decades between 1960 and 2000 between the origin
(`origincode`) and destination (`destcode`) countries given in the data.
We create a subsetted version of this data that only contains migration
counts of females over `1000` in `2000`.

``` r
> MigrationFlows <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/MigrationFlows.csv")
> MigrationFlowsF <- MigrationFlows %>% 
+    filter(sex == "Female", Y2000>1000) %>% 
+    select(origincode, destcode, Y2000)
```

#### Question 1

Compute the betweenness measure for your migration network using the
`sna` package command `betweenness(network, gmode="digraph")` (since you
have a directed graph). Save the results in a vector then look at
numerical and graphical summaries of the betweenness measure. Which 10
countries have the highest measure of betweenness? Are these the
countries that you expected?

- **Hint:** Creating a dataframe of vertex names and betweeness can help
  with figuring out the `top 10`.

#### Question 2

Create a subgraph from the previous activity using the following smaller
subset of countries. Draw a plot of this network with vertex labels
added. (You can use your code from the previous activity)

``` r
> smallerGroup <- c("USA","CAN","MEX","BRA","CHN","JPN","GBR","PRT")
```

#### Question 3

Modify your plot so that node size is a function of `degree`. Use the
`size` option in `geom_nodes`. What can you learn from this modified
plot?

- **Note:** Use `gmode="digraph"` to indicate a directed graph
- **Note:** Use `geom_nodelabel_repel` so that you can see both the size
  of the node and the label at the same time

#### Question 4

Repeat Q3 but use `betweenness` instead of `degree`. What differences do
you notice? Do they make sense intuitively?

#### Question 5

Compute the density, transitivity (clustering), and diameter values for
this network. What do they tell you about its structure? How do you
think the numbers would vary if we looked at only countries in South
America?
