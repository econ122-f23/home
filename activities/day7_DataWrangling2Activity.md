Data wrangling: multiple data table
================
ECON 122
Day 7

## `nycflights13` package

The `nycflights13` package contains multiple data sets describing
`flights` departing from the NYC area in 2013, along with info on
`airlines`, `airports`, `planes` and `weather` in 2013.

#### 1. Take a look at the `flights` `airlines` and `airports` data set help files.

*hint*: try `?flights`

-   What variable(s) are the keys that connect the `flights` and
    `airlines` data sets?
-   What variable(s) are the keys that connect the `flights` and
    `airports` data sets?

#### 2. Merging `airports` and `flights` data.

-   How many unique flight `destintations` in `flights` are not given in
    the `airports` data? (Hint: look at `anti_join` or `semi_join`)
-   How many airports given in `airports` are not `destintations` given
    in `flights`?
-   Use `left_join` to add `airports` info to the `flights` data. How
    many rows are there in this joined data? Then repeat using
    `inner_join` and `full_join`. Explain the differences in row counts
    for these three ways of joining.
-   Calcuate the median `arr_delay`, average flight `distance`, and
    number of flights for each `destintations`. Plot mean distance vs
    mean arrival delay, using number of flights to determine point size.
    Describe the trend you see.
    -   *hint*: Use the `na.rm=TRUE` flag to remove `NA`s
-   For fun: Use mean arrival delay by `destintations` to map mean delay
    by location on a map of the US. You can filter `lat` and `long` to
    restrict attention to the main 48 states.

#### 3. Use the `weather` data set to add hourly weather information to the `flights` data.

-   The `flights` data contains `hour` and `minute` variables. Do these
    record the departure, scheduled departure, arrival or scheduled
    arrival time?
-   What variables are the keys to connect `flights` and `weather`?

#### 4. Use the `weather` data set to add the hourly weather information to the `flights` data.

-   Plot the daily average departure delay vs. the daily average precip,
    using colors to represent origin. Describe the relationship you
    observe.
