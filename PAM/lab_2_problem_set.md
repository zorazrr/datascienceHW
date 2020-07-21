Lab 2 Problem Set
================

  - [Hands-on Task 1: Wrangle the Craigslist
    data](#hands-on-task-1-wrangle-the-craigslist-data)
      - [Load the listing data.](#load-the-listing-data.)
      - [Create a new data frame that is limited to 1 bedroom
        units.](#create-a-new-data-frame-that-is-limited-to-1-bedroom-units.)
      - [Mutate fields in `scraped` that are currently character but
        should be numeric as new
        columns.](#mutate-fields-in-scraped-that-are-currently-character-but-should-be-numeric-as-new-columns.)
      - [Create a new data frame with listings that mention “affordable”
        in their
        title](#create-a-new-data-frame-with-listings-that-mention-affordable-in-their-title)
      - [Create a column in `scraped` indicating whether the rent asked
        is more than
        $800.](#create-a-column-in-scraped-indicating-whether-the-rent-asked-is-more-than-800.)
      - [Summarize the average square footage for 1, 2 and 3 bedroom
        units.](#summarize-the-average-square-footage-for-1-2-and-3-bedroom-units.)
      - [Create a summary statistic table with the minimum, maximum and
        average rent values for 1 bedroom
        units.](#create-a-summary-statistic-table-with-the-minimum-maximum-and-average-rent-values-for-1-bedroom-units.)
      - [Create a summary table for the proportion of 1, 2 and 3 bedroom
        units with rents below Fair Market Rent levels set by the
        Department of Housing and Urban
        Development.](#create-a-summary-table-for-the-proportion-of-1-2-and-3-bedroom-units-with-rents-below-fair-market-rent-levels-set-by-the-department-of-housing-and-urban-development.)
      - [If housing assistance allows households to rent units up to the
        FMR level, how much choice would you say they have on the rental
        markes? What policy proposals, if any, would you propose given
        the evidence you’ve generated using current rental
        listings?](#if-housing-assistance-allows-households-to-rent-units-up-to-the-fmr-level-how-much-choice-would-you-say-they-have-on-the-rental-markes-what-policy-proposals-if-any-would-you-propose-given-the-evidence-youve-generated-using-current-rental-listings)
  - [Hands-on Task 2: Making some plots of the Craigslist
    data](#hands-on-task-2-making-some-plots-of-the-craigslist-data)
      - [Create and interpret a scatterplot of square footage by rent
        asked for 2 bedroom listings using
        `ggplot()`.](#create-and-interpret-a-scatterplot-of-square-footage-by-rent-asked-for-2-bedroom-listings-using-ggplot.)
      - [Create and interpret a bar chart of average square footage by
        bedroom size using
        `ggplot()`.](#create-and-interpret-a-bar-chart-of-average-square-footage-by-bedroom-size-using-ggplot.)
      - [Create and interpret a histogram of square footage using
        `ggplot()`.](#create-and-interpret-a-histogram-of-square-footage-using-ggplot.)
      - [Create and interpret a ggplot of your choice using the listing
        data that incorporates the color
        aesthetic.](#create-and-interpret-a-ggplot-of-your-choice-using-the-listing-data-that-incorporates-the-color-aesthetic.)
  - [Hands-on Task 3: Correlation](#hands-on-task-3-correlation)
      - [Estimate the correlation between square footage and rent
        overall and interpret this
        statistic.](#estimate-the-correlation-between-square-footage-and-rent-overall-and-interpret-this-statistic.)
  - [Hands-on Task 4: Make a map](#hands-on-task-4-make-a-map)
      - [Create a map of 2 bedroom units listed in May with `ggplot()`
        or
        `leaflet()`](#create-a-map-of-2-bedroom-units-listed-in-may-with-ggplot-or-leaflet)
      - [Create a map of 1 bedroom units listed in May that have a rent
        asked that is below Fair Market Rent with `ggplot()` or
        `leaflet()`](#create-a-map-of-1-bedroom-units-listed-in-may-that-have-a-rent-asked-that-is-below-fair-market-rent-with-ggplot-or-leaflet)

# Hands-on Task 1: Wrangle the Craigslist data

Here you will use `dplyr` to complete process the listing data that we
started with to get a feel for writing data manipulation code. Once we
are done preparing the data, we will do some basic data visualization
and statistical analysis to understand patterns and relationships within
the data.

## Load the listing data.

``` r
#add your code here
```

## Create a new data frame that is limited to 1 bedroom units.

``` r
#add your code here
```

## Mutate fields in `scraped` that are currently character but should be numeric as new columns.

``` r
#add your code here
```

## Create a new data frame with listings that mention “affordable” in their title

``` r
#add your code here
```

## Create a column in `scraped` indicating whether the rent asked is more than $800.

``` r
#add your code here
```

## Summarize the average square footage for 1, 2 and 3 bedroom units.

``` r
#add your code here
```

## Create a summary statistic table with the minimum, maximum and average rent values for 1 bedroom units.

``` r
#add your code here
```

## Create a summary table for the proportion of 1, 2 and 3 bedroom units with rents below Fair Market Rent levels set by the Department of Housing and Urban Development.

You will want to consult
[this](https://www.rentdata.org/ithaca-ny-msa/2018) site for the FMR
values. Hint: you could use `case_when()` to create a FMR column with
each bedroom size’s FMR value and then `mutate()` another column
flagging if the row’s rent was greater than or less than the FMR.

``` r
#add your code here
```

## If housing assistance allows households to rent units up to the FMR level, how much choice would you say they have on the rental markes? What policy proposals, if any, would you propose given the evidence you’ve generated using current rental listings?

Write your response here

<br>

<hr>

<br>

# Hands-on Task 2: Making some plots of the Craigslist data

## Create and interpret a scatterplot of square footage by rent asked for 2 bedroom listings using `ggplot()`.

``` r
#add your code here
```

## Create and interpret a bar chart of average square footage by bedroom size using `ggplot()`.

``` r
#add your code here
```

## Create and interpret a histogram of square footage using `ggplot()`.

``` r
#add your code here
```

## Create and interpret a ggplot of your choice using the listing data that incorporates the color aesthetic.

``` r
#add your code here
```

<br>

<hr>

<br>

# Hands-on Task 3: Correlation

## Estimate the correlation between square footage and rent overall and interpret this statistic.

``` r
#add your code here
```

<br>

<hr>

<br>

# Hands-on Task 4: Make a map

## Create a map of 2 bedroom units listed in May with `ggplot()` or `leaflet()`

``` r
#add your code here
```

## Create a map of 1 bedroom units listed in May that have a rent asked that is below Fair Market Rent with `ggplot()` or `leaflet()`

``` r
#add your code here
```
