Tidy data: Carleton College Energy Activity
================
ECON 122
Day 8,9

The data used in this example is from Carleton College. The goal of this
activity is to help you better understand what issues arise from working
with real world data.

# Building Data

The `AAbuildings` dataset gives the size and year built of buildings on
campus that are considered academic or administrative buildings.

### Question 1

**1.** Run the two read commands below (`read.csv` and
`readr::read_csv`). How do they read in the data differently?

**2.** How many buildings on campus are classified as academic or
administrative (how many rows are there)?

``` r
> AAbuildings <- read.csv("https://raw.githubusercontent.com/mgelman/data/master/AcadAdminBuildings.csv",stringsAsFactors=TRUE)
> glimpse(AAbuildings)
> AAbuildings <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/AcadAdminBuildings.csv")
> glimpse(AAbuildings)
```

# Energy Use Data

A second dataset gives energy use (kiloWatt hour) every 15 minutes for
the 15-16 academic year for all buildings on campus that have an energy
meter installed.

### Question 2

**1.** How have the variable types changed when using `read_csv` instead
of `read.csv`? - e.g. look at Musser, Timestamp

``` r
> energy1 <- read.csv("https://raw.githubusercontent.com/mgelman/data/master/EnergyData1516.csv",stringsAsFactors=TRUE)
> glimpse(energy1)
> local_edition(1)
> energy2 <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/EnergyData1516.csv")
> glimpse(energy2)
```

**2.** Use the `?read_csv` help file to determine why the `read_csv`
command picks character or integer types for some variables. (Hint: look
at the `guess_max` argument)

**3.** The Musser Hall readings in `energy2` should not be logical
types. Why do the results below suggest that this is an issue? (You
could also look at `problems(energy2)`).

``` r
> summary(energy1$Musser_Hall)
> summary(energy2$Musser_Hall)
```

### Question 3

Read the energy data in again using the `read_csv` command below that
specifies column type for `Timestamp` and `dayWeek` and defaults to
double types for all other. The order of the factor levels of `dayWeek`
are also given so we get days ordered correctly in plots. Note that you
will need to wrap a variable name in backticks if it starts with a
non-letter character.

**1.** What are the dimensions of the energy data?

**2.** What do the rows represent? columns represent? Is this “tidy”
data (more narrow than wide)?

**3.** How many buildings on campus are in the energy data?

``` r
> energy <- read_csv("https://raw.githubusercontent.com/mgelman/data/master/EnergyData1516.csv", 
+                    col_type = cols(.default = col_double(), 
+                                    Timestamp = col_datetime(format = ""),
+                                    dayWeek = col_factor(levels=c("Mon","Tues","Wed","Thurs","Fri","Sat","Sun"))))
> glimpse(energy)
> summary(energy1$Musser_Hall)  # can check that summaries match
> summary(energy$Musser_Hall)
> summary(energy$`100_Nevada_Street`)  # use backticks with variable names that start with numbers
```

### Question 4:

**1.** For the `Center_for_Mathematics_&_Computing`: Use the energy data
to plot the average hourly energy usage in October. What trend do you
see?

**2.** For the `Center_for_Mathematics_&_Computing`: Show how your plot
for #1 above varies by day of the week (`dayWeek`). What trends do you
see?

### Question 5

**1.** For the `Center_for_Mathematics_&_Computing`: Use the energy data
to plot the average energy usage in Oct. of 2015 by day of the week
(`dayWeek`). What trend do you see?

-   note: if you use `geom_line` you will need to add `group=1` to your
    `aes` to get a line graph when plotting against the categorical
    variable `dayWeek`. This is because when we use a `factor` variable
    `aes` will set the group to each factor. `geom_line` will then try
    to connect the dots **WITHIN** each group which is just connecting
    to itself. To fix this, we set `group=1` to tell `ggplot` that all
    the observations are part of the same `group` and so to connect the
    line across days of the week. We could also use `group=99`, the main
    idea is that we set all the observations to the **SAME** group.

**2.** How could you add more buildings to your plot? How easy or hard
would this be with the data in the current (wide) format?

# Reshape `energy` data

Create a narrow version of the `energy` data to allow you to *filter* to
select one, or more, buildings to plot and analyze.

### Question 6:

**1.** What are the dimensions of the narrow version of this data?

### Question 7

**1.** Recreate your graph from Question 5 using the narrow version of
this data. What parts of your data wrangling or plot commands do you
need to change?

### Question 8

**1.** Plot a line graph of the average energy usage in Oct. by day of
the week (`dayWeek`) for each `building`. What trends do you see? (can
you see any?)

-   note: for `geom_line` you will need to add `group=building` to your
    `aes` to get a line graph for each building when plotting against
    the categorical variable `dayWeek`

# Joining data

Since we have so many buildings, perhaps limiting our results to
academic/admin buildings will help to clear some of the clutter

### Question 9

**1.** How many buildings are in the energy data?

**2.** How many of the buildings in the energy data are academic/admin
buildings?

**3.** How many academic/admin buildings in the building data are not
included in the energy data?

### Question 10

Create a dataset by joining the energy and acad/admin building datasets
so that you only have acad/admin buildings and full info for both energy
and size/year built.

**1.** Repeat question 8, but this time just for acad/admin buildings.
Are any trends or differences in buildings clearer?

### Question 11: use joined data

**1.** Compute the mean energy use by building for Oct. What buildings
are the top 5 energy users?

**2.** Repeat the question, but this time compute mean energy use per
square foot. Any changes in the top 5?

**3.** Plot the mean energy use per square foot by day of the week for
the top 5 buildings found in the previous question and include info
about their year built. Compare the daily trends in these buildings.
