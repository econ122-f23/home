Iteration
================
ECON 122
Day 11

## Using `sapply()` and `lapply()`

### Question 1

You are considering moving to the following cities and want to gather
information about them using the `MonthlyWeather` dataset you are
familiar with.

``` r
> weather <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/MonthlyWeather.csv")
> cities <- c("Los Angeles","Atlanta","Dallas","Denver","Minneapolis","Pittsburgh")
```

Find the average monthly temperature (across all time periods available)
for each city using `dplyr`.

### Question 2

Find the average monthly temperature (across all time periods available)
for each city using `sapply`.

1.  You must first create a function that calculates the `mean` when
    given a `city` and a `dataset`. Create this function and test it out
    on one city.

2.  Use `sapply()` to apply your mean function to the vector of cities
    you are considering. Do you get the same answers as `dplyr`?

### Question 3

While the mean is helpful, you would like to know what the extremes are.
Instead of calculating the mean, you would like to create a table that
displays the 3 coldest and hottest observations for each city.

1.  Can you perform this task using the simple `dplyr` commands?

2.  You first need to write a function that outputs a `dataframe` with
    the 3 coldest and hottest observations given a `city` and `dataset`.
    Create this function and test it out on one city.

    -   **Hint:** `bind_rows()` allows you to combine `dataframes`

3.  Now use `sapply()` to apply your function to our selected cities. Is
    there an issue?

4.  What happens if you use `lapply()`? Can you transform your output to
    create 1 table that has a list of cities and their 3 hottest and
    coldest temperatures?

5.  Visualize your results by plotting the 3 hottest and coldest monthly
    temperatures for each city. Which city do you prefer?
