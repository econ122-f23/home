Network GoT Activity
================
ECON 122
Day 22

## Game of Thrones network

Consider the data described in the [Game of Thrones
handout](https://www.maa.org/sites/default/files/pdf/Mathhorizons/NetworkofThrones%20%281%29.pdf).
Read in the edgelist and weights from the Storm of Swords novel.

``` r
> got <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/stormofswords.csv")
> got
```

Two characters are connected if their names appear within 15 words of
one another in the novel. The edge weight counts the number of these
occurances. The edge list is not directed (even though the variables
names suggest such).

### Create network

The page rank algorithm is available in `igraph`. To redo the results we
see in the paper, we will use this package to create and analyze this
network. Here we create an `igraph` network object using the edge list
(the first two coloumns of `got`) along with edge variables (any columns
after cols 1-2). Note that we want the edge weights to be lower case for
`igraph` to recognize the variable as an edge weight that is used for
certain graph stat calculations.

``` r
> names(got) <- tolower(names(got))
> names(got)
> got.net <- graph_from_data_frame(got, directed=FALSE) 
```

The minimum number of associations between two characters is 4 and the
max is 96 (between Bran and Hodor).

``` r
> got.net
> summary(E(got.net)$weight)
> E(got.net)[E(got.net)$weight == 96]
```

#### Question 1

- How many nodes (characters) are in this network?
- How many edges? What proportion of possible edges are realized?
- How many components does this network have?

**Note:** I’ve listed the commands below but you still have to figure
out what they capture

``` r
> ecount(got.net)
> vcount(got.net)
> is.connected(got.net)
> components(got.net)
> graph.density(got.net)
```

### Centrality stats: Degree

Let’s next look at the centrality stats for characters in the network.
In case you have the `statnet` package loaded, the stats below with
names in common specifically reference the `igraph` package.

Node degree counts the number of characters that a given node is
associated with. The weighted degree (given by `graph.strength`) is the
sum of the edge weights for edges connecting a node to other characters.
This weighted degree counts the total number of interactions a character
has with others in the network. Here we compute the degrees and create a
data frame of them:

``` r
> V(got.net)$degree <- igraph::degree(got.net)
> V(got.net)$wtdegree <- graph.strength(got.net)
> stats <- data_frame(name = V(got.net)$name, 
+                     degree = V(got.net)$degree, 
+                     wtdegree = V(got.net)$wtdegree )
```

#### Question 2

- Who are the five characters with highest degree? Highest weighted
  degree? Verify that these values (look like they) match those in
  Figure 3 of the GoT paper.  
- Explain how Robb can have higher degree than Bran but lower weighted
  degree.

### Centrality stats: Betweenness and closeness

Here are the unweighted versions of betweenness and closeness. Note that
the “conventional” closeness measure is the inverse of the mean shortest
path distance between a node and all other nodes in the network, so that
larger values (closer to 1) indicate a higher level of closeness. The
GoT paper computes the inverse of this (i.e. mean path distance), so
that lower values (closer to 1) indicate a higher level of closeness.

``` r
> V(got.net)$betweenness <- igraph::betweenness(got.net, weights=NA)
> V(got.net)$closeness <- igraph::closeness(got.net, normalized = TRUE, weights=NA)
> V(got.net)$inv.closeness <- 1/V(got.net)$closeness
```

#### Question 3

- Add these stats to the `stats` data frame created above. Verify that
  the top ranked characters match those shown in Figure 3
- How can a character like Daenerys have a low rank for closeness but a
  much higher rank for betweenness. (You can use Figure 2 in the GoT
  paper to visualize the structure.)

### Centrality stats: Google page rank

The GoT gives a simple description of the page rank centrality measure.
The basic idea is that a node will have a higher page rank value (and
higher “centrality”) if it is connected to important nodes. The page
rank of node `i` is a function of the weighted sum of the page ranks of
its neighbors (who `i` is connected to) with weights given by the edge
weight between node `i` and its neighbor divided by the total weighted
degree of the neighbor.

For example, consider the page ranks of Catelyn and Hodor. Both are
connected to Bran, who has a weighted degree of 344. Bran has a total of
4 interactions with Catelyn so his page rank value is weighted by the
fraction 4/344, or 0.01, when computing Catelyn’s page rank. But Hodor’s
page rank calculation is influenced much more by Bran’s value, since he
has 96 interactions with Bran, which makes up a 96/344, or 0.28,
fraction of all of Bran’s interactions. In this way, Hodor’s page rank
will be closer to Bran’s value because he has more interactions with him
than Catelyn.

#### Question 4

- Compute the page rank values below, then add them to the `stats` data
  frame.
- Verify that the characters with the top 6 page rank value are the same
  set (but in a different order) as the top 6 in Figure 3.
- How can Daenerys have such a high page rank but low degree?
- Plot the network with node or label size determined by the page rank
  value.

``` r
> V(got.net)$page.rank <- page_rank(got.net)$vector
```

### Community detection

Community detection in networks is a process of finding clusters
(communities) of nodes that are highly connected within a cluster and
have few connections across clusters. Figure 2 in the GoT uses color to
denote the 7 communities found in their analysis.

There are a variety of algorithms to do this, but most depend on the
modularity of the cluster assignment. Modularity compares the weight
between two nodes in the same cluster to the expected weight between the
two nodes under a random assignment of edges. The higher the modularity
value, the higher the level of clustering (with a max value of 1).

The article mentions uses the Louvain algorithm, which is a hierarchical
method similar to hierarchical clustering for unsupervised learning.
Nodes start out as individual clusters, then are merged together to
create communities to increase modularity the most at each step (in a
local, greedy way). The algorithm stops when modularity can’t be
increased by an additional step.

``` r
> got.cl <- cluster_louvain(got.net)
> got.cl
> modularity(got.cl)
> table(membership(got.cl))
> V(got.net)$got.cl <- membership(got.cl)
```

#### Question 5

- Verify that the Louvian function above gives us 7 communities that
  seem to match those in GoT Figure 2
- Which community is the largest?
- What is the value of modularity for the community memberships found by
  the Louvian algorithm?
- Plot the network with colors representing each community (check to see
  if your figure matches Fig 2)

### Random networks

Is the value of modularity in question 5 large? What values would be
expected from a graph with 107 nodes and 352 edges if the edges were
randomly assigned with no clustering or communities?

The `erdos.renyi.game` function can create such a network. Here we
assign the number of nodes and edges, then edges are randomly assigned
to pairs of nodes (with no direction, no loops, no multiple edges
between nodes). Then we assign the edge weights to the random network’s
352 edges. Now we have a network with the same number of nodes, edges,
edge weights, and density as the GoT network.

``` r
> test <- erdos.renyi.game(vcount(got.net), ecount(got.net), type="gnm")
> E(test)$weight <- got$weight
> plot(test)
```

#### Question 6

- How many clusters were found in this random network?
- What is the modularity of this random network’s clusters? Is the GoT
  network’s modularity higher?

To help assess how different the GoT’s modularity is compared to the
random network’s, we could create lots of random networks (with the same
basic network structure), fit the cluster algorithm and compute their
modularity. If the GoT’s modularity is higher than these values, we
could claim that the observed GoT modularity is higher than what we’d
expect in a random graph with similar basic structure.

Here is a function that creates one random network with the right
structure. The output is the modularity of the Louvian cluster choice:

``` r
> sim <- function(net)
+ {
+   test.sim <- erdos.renyi.game(vcount(net), ecount(net), type="gnm")
+   E(test.sim)$weight = E(net)$weight
+   modularity(cluster_louvain(test.sim))
+ }
```

Then repeat this 1000 times:

``` r
> mods <- replicate(1000,sim(got.net))
```

Compare the GoT network’s modularity to the simuluated values:

``` r
> hist(mods, xlim=c(.45,.65))
> abline(v=modularity(got.cl))
```

#### Question 7

- How does the GoT modularity compare to the simulated ones? What does
  this suggest about the communities found in the GoT network?
