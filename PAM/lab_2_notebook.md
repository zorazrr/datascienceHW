Lab Tutorial 2 - The Rent Is Too High
================

  - [Overview](#overview)
      - [Goals](#goals)
      - [Data](#data)
  - [Preamble: Load the packages and data for our
    analysis](#preamble-load-the-packages-and-data-for-our-analysis)
  - [Part A: Using `dplyr` verbs to explore the listing
    data](#part-a-using-dplyr-verbs-to-explore-the-listing-data)
      - [`filter()`](#filter)
      - [`select()`](#select)
      - [`mutate()`](#mutate)
      - [`summarize()`](#summarize)
      - [“Piping” `dplyr` functions with the magrittr `%>%`
        operator](#piping-dplyr-functions-with-the-magrittr-operator)
      - [`group_by()`](#group_by)
      - [`arrange()`](#arrange)
      - [Bringing it all together](#bringing-it-all-together)
  - [Part B: Learning the basics of `ggplot2` for data
    visualization](#part-b-learning-the-basics-of-ggplot2-for-data-visualization)
      - [A quick example](#a-quick-example)
      - [Tidy data](#tidy-data)
      - [`aes()`-thetics](#aes-thetics)
      - [`geom`etry functions](#geometry-functions)
      - [Adding our pieces together](#adding-our-pieces-together)
      - [Saving visualizations](#saving-visualizations)
  - [Part C: Learning the basics of `sf` for spatial
    analysis](#part-c-learning-the-basics-of-sf-for-spatial-analysis)
      - [Remember how we have spatial
        data?](#remember-how-we-have-spatial-data)
      - [Plotting points](#plotting-points)
      - [Making a quick map](#making-a-quick-map)
  - [Summary](#summary)

<br>

<hr>

<br>

# Overview

## Goals

In this lab tutorial, we will focus on honing our data analysis skills
using the `tidyverse` libraries. These software libraries include:

  - `dplyr` - a *very* important package for handling most data
    manipulation tasks
  - `ggplot2` - functions to create data visualizations with the
    “grammar of graphics”
  - `tibble` - a special data frame object with some nice features to
    improve usability
  - `tidyr` - functions to change the structure of data to redefine what
    a row means
  - `readr` - functions to load different filetypes of structured data
    and to parse the values into R classes
  - `stringr` - functions to work with character class, or string,
    values in a data frame (e.g., look for patterns)
  - `forcats` - functions to work with factor class values (where
    integer values correspond to a set of character values)

A particular goal will be to understand how the six most common verbs of
`dplyr` give us a framework for wrangling data into the format we want
for running statistical analyses. After this primer on data
manipulation, we will also learn some `ggplot2` and `sf` code for
creating plots and maps with the data we’ve prepared.

## Data

The data for this lab are a set of apartment listings in the Ithaca, NY
area that we scraped from the internet. Rental listings indicate a
housing vacancy somewhere in the real world, so these are intrinsically
*spatial data* that contain information about the unit itself, as well
as information about its location in physical space. Since we are
working with spatial data, the final part of this lab will introduce
tools that R has for acting as a *Geographic Information System* (GIS).

<br>

<hr>

<br>

# Preamble: Load the packages and data for our analysis

``` r
library(tidyverse) #we will use dplyr, readr and other libraries from this metalibrary
library(sf)        #this is what will make R into a Geographic Information System (GIS)
library(lubridate) #this will give us functions to work with dates more easily
library(leaflet)   #this will allow us to easily make interactive maps with base maps

#if needed, install libraries with install.packages()
#e.g.: install.packages("sf")
```

For this problem set, we will use a set of data that are stored in an
.RData file. This is somewhat different from a flat file, or spreadsheet
of data, which may be stored as comma separated values (CSV). RData
files allow us to save data that are not easily structured as
conventional spreadsheets and can also be used to store all objects in
your environment if you want to create checkpoints in your analysis.

In this case, the file we are loading contains a data frame of listings
that includes a “simple features” geometry column that denotes where
each listing is located in physical space.

``` r
load("./input/ithaca_rentals.RData")
```

Now let’s see what our environment has in it after loading the RData
file

``` r
ls()
```

    ## [1] "scraped"

We now have an object `scraped` in memory. Let’s see what *class* the
object is by passing the object to the `class()` function

``` r
class(scraped)
```

    ## [1] "sf"         "data.frame"

This output shows that the object we loaded is a “sf”, or simple
feature, class. The output shows “data.frame” too, because “sf” objects
are a special form of a data frame that is *spatially aware*.

We can use the glimpse function on `scraped` to take a peek at what this
object contains

``` r
glimpse(scraped)
```

    ## Rows: 13,153
    ## Columns: 14
    ## $ listing_date            <date> 2020-02-08, 2020-02-08, 2020-02-01, 2020-02-…
    ## $ listing_loc             <chr> "Ithaca", "Ithaca", "Ithaca", "Ithaca", "Itha…
    ## $ listing_title           <chr> "Stunning 2 bedroom Balcony Available 4/6!", …
    ## $ scraped_beds            <chr> "2BR", "1BR", "1BR", "1BR", "2BR", "2BR", "1B…
    ## $ scraped_baths           <chr> "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1B…
    ## $ scraped_rent            <chr> "$1240", "$1257", "$1005", "$1375", "$1200", …
    ## $ scraped_sqft            <chr> "1025\r\nft\r\n2", "820\r\nft\r\n2", "480\r\n…
    ## $ scraped_address         <chr> "On TCAT Route 32", "600 Warren Road near Upt…
    ## $ scraped_neighborhoods   <chr> "(37 Uptown Road #16D Ithaca, NY)", "(600 War…
    ## $ scraped_google_maps_url <chr> "https://www.google.com/maps/search/42.480390…
    ## $ scraped_avail           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ post_id                 <chr> "post id: 7089197572", "post id: 7086433186",…
    ## $ post_origin             <chr> "3 days ago\r\n 2020-03-07 15:14", "7 days ag…
    ## $ geometry                <POINT [°]> POINT (-76.47501 42.48072), POINT (-76.…

This output shows the total number of rows in `scraped`, the name of
each column in `scraped` along with the column *type* and the first few
values.

The final column named `geometry` is what makes this object spatial in
nature—each row actually contains two values, one for the projected
longitude coordinate and one for the projected latitude coordinate.

<br>

<hr>

<br>

# Part A: Using `dplyr` verbs to explore the listing data

Now that the data are loaded, let’s try using the `dplyr` library to
explore and analyze the listings. There are six key functions, or verbs,
to this library that give us a vocabulary for analyzing our data. They
are:

1.  `filter()` - look at specified rows of data based on an expression
2.  `select()` - look at specified columns of data based on name, type
    or a pattern
3.  `mutate()` - create a new column based on another or modfiy an
    existing column
4.  `summarize()` - create a new data frame based on *aggregating*
    variables with other functions like sum()
5.  `group_by()` - group the table by one or more variables, usually
    before creating new variables or a new data frame
6.  `arrange()` - sort the data by a column or columns of interest

Throughout this section we will review how to accomplish common data
wrangling tasks in `dplyr` and provide comparison base R code to
demonstrate the advantages that using these verbs can provide. We will
conclude by discussing less common `dplyr` verbs and by linking to
important resources for mastering this library.

Side note: It is important to keep in mind that there are usually many
ways to “skin the cat” when programming. `dplyr` provides one toolkit
for doing data analysis that emphasizes consistency and
interpretability. This enables users to accomplish the most essential
data wrangling tasks in a way that others can easily read and
understand.

## `filter()`

One of the most essential things we can do when analyzing data, spatial
or non-spatial, is to look at subsets of rows in the overall table.

The dplyr verb, or function, `filter()` takes a data frame as its first
argument, followed by one or more expressions that define which rows to
return. At its most basic level, `filter()` returns rows where the given
expression evaluated to be `TRUE`.

### Equals / does not equal

Let’s try filtering to listings that are for 2 bedroom units based on
their `scraped_beds` value.

``` r
filter(scraped, scraped_beds == "2BR")
```

Since `scraped_beds` is currently a *character* type column, the two
most basic expressions would be to filter based on rows being equal
(`==`) to some value (e.g. “2BR”), or being not equal to some value
(`!=`). Character values need to be quoted. If we do not quote values
(e.g., “1BA”), R thinks we are trying to refer to a variable/column in
our data frame rather than a specific value. *Remember:* R reserves
single `=` for assignment of objects, and `==` for evaluating
expressions based on equality.

We can look at the expression outside of the `filter()` call to see how
this filtering based on `TRUE` values works. Note we need to point R to
the data frame of interest since we are not using `filter()` where we
name the data frame of interest first.

``` r
scraped$scraped_beds == "2BR"
```

    ##  [1]  TRUE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE
    ##  [ reached getOption("max.print") -- omitted 13143 entries ]

### Greater/less than

For a numeric or date column (like `listing_date`), we can also use
greater than (`>`) or less than (`<`) operators to create a filtering
expression. This can also be modified to be greater/less than or equal
to by adding an equals sign (`>=`, `<=`). We will test this by filtering
to listings posted on or after to March 1st. Note the year-month-day
format used for R dates.

``` r
filter(scraped, listing_date >= "2020-03-01")
```

### Multiple expressions

If we have a set of values we want to filter with, we can either create
a conjunction using the AND (`&`) or OR (`|`) operators. Here we will
filter to 2BR listings posted on or after March 1, combining the two
previous expressions into one.

``` r
filter(scraped, listing_date >= "2020-03-01" & scraped_beds == "2BR")
```

For instances where we want to filter by multiple conditions combined by
`&` operators, we can also create multiple filter arguments like the
following:

``` r
filter(scraped, listing_date >= "2020-03-01", scraped_beds == "2BR")
```

### Creating a new object based on a subset

And if we want to save some subset of rows as a new data frame, we use
an assignment operator (either `=` or `<-`) in combination with our
`filter()` function call.

``` r
#first we assign our filter output to a new object called march_listings
march_listings <- filter(scraped, listing_date >= "2020-03-01", listing_date < "2020-04-01")

#now we look at the result
glimpse(march_listings)

#check the unique date values now in march_listings
unique(march_listings$listing_date)
```

### Beyond the basics

#### Using a set of values

There are many other ways to create filtering expressions. The `%in%`
operator allows you to provide a set of values with `c()` function to
then create filters that would otherwise require many OR (`|`)
operators.

``` r
filter(march_listings, scraped_beds %in% c("1BR", "2BR", "3BR"))
#equivalent to filter(march_listings, scraped_beds == "1BR" | scraped_beds == "2BR" | scraped_beds == "3BR")
```

#### Using string matching

For character type columns like `scraped_neighborhoods`, we can also use
string functions like `str_detect()` that allows us to match a pattern.
Here we will return listings that mentioned “Collegetown” in the
`scraped_neighborhoods` field.

``` r
filter(scraped, str_detect(scraped_neighborhoods, pattern = "Collegetown"))
```

#### Removing rows with missing values in a column

If we want to filter out rows without complete data, we can use the
`is.na()` function to create this expression for `filter()`. If we run
`is.na()` on a given column, we get `TRUE` or `FALSE` values (i.e. a
logical vector) for whether the row’s value was an `NA` or not.

``` r
is.na(scraped$scraped_rent)
```

    ##   [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [13] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [25] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [37] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [49] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [61] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [73] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [85] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [97] FALSE FALSE FALSE FALSE
    ##  [ reached getOption("max.print") -- omitted 13053 entries ]

We can use `table()` on this type of function call to compute a quick
tabulation of how many rows have an `NA`.

``` r
table(is.na(scraped$scraped_rent))
```

We can then `filter()` `NA`s out of the data frame by testing rows for
if they are not `NA` with `!is.na()`

``` r
filter(scraped, !is.na(scraped_rent))
```

<br>

## `select()`

The `select()` function allows us to pick subsets of *columns* in our
data frame. This is useful if we have many columns and want to remove
some, whether due to them being no longer needed or to prepare a table
for printing or sharing. `select()`, like `filter()` takes a data frame
as its first argument, and then allows users to name columns they want
to keep as second, third, etc. columns.

### Basic column selection

If we use select without an assignment operator (e.g., `=`, `<-`), we
print this subset of columns to the console. This is like using
`filter()` to print subsets of rows to console as we did in the prior
section. Note how we drop the columns that are not named.

``` r
#select listing_date and listing_title columns from scraped
date_title <- select(scraped, listing_date, listing_title)

glimpse(date_title)
```

    ## Rows: 13,153
    ## Columns: 3
    ## $ listing_date  <date> 2020-02-08, 2020-02-08, 2020-02-01, 2020-02-03, 2020-0…
    ## $ listing_title <chr> "Stunning 2 bedroom Balcony Available 4/6!", "2 Bedroom…
    ## $ geometry      <POINT [°]> POINT (-76.47501 42.48072), POINT (-76.46898 42.4…

When we use `select()`, we create a new data frame (or in this case
*simple feature* data frame) using the columns that we named in the
function call. This is important to remember, because this means we are
going to have the same class object upon assigning the results to a new
object. Note how since we have an sf object with a `geometry` column,
`dplyr` automatically adds this in so the data stay spatial unless we
explicitly use a function to drop it.

``` r
#select listing_date and listing_title columns from scraped, save to object new_df
new_df <- select(scraped, listing_date, listing_title)

glimpse(new_df)
```

### Using `select()` to reorder a data frame

Sometimes it is useful to reorder the columns in a data frame if we want
to produce a table for printing or if some values like row IDs might
make sense to have first in the table. We can use the `everything()`
function within `select()` to ensure that we don’t inadvertently drop
columns but just reorder them.

``` r
reordered_df <- select(scraped, listing_title, everything())

glimpse(reordered_df)
```

    ## Rows: 13,153
    ## Columns: 14
    ## $ listing_title           <chr> "Stunning 2 bedroom Balcony Available 4/6!", …
    ## $ listing_date            <date> 2020-02-08, 2020-02-08, 2020-02-01, 2020-02-…
    ## $ listing_loc             <chr> "Ithaca", "Ithaca", "Ithaca", "Ithaca", "Itha…
    ## $ scraped_beds            <chr> "2BR", "1BR", "1BR", "1BR", "2BR", "2BR", "1B…
    ## $ scraped_baths           <chr> "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1B…
    ## $ scraped_rent            <chr> "$1240", "$1257", "$1005", "$1375", "$1200", …
    ## $ scraped_sqft            <chr> "1025\r\nft\r\n2", "820\r\nft\r\n2", "480\r\n…
    ## $ scraped_address         <chr> "On TCAT Route 32", "600 Warren Road near Upt…
    ## $ scraped_neighborhoods   <chr> "(37 Uptown Road #16D Ithaca, NY)", "(600 War…
    ## $ scraped_google_maps_url <chr> "https://www.google.com/maps/search/42.480390…
    ## $ scraped_avail           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ post_id                 <chr> "post id: 7089197572", "post id: 7086433186",…
    ## $ post_origin             <chr> "3 days ago\r\n 2020-03-07 15:14", "7 days ag…
    ## $ geometry                <POINT [°]> POINT (-76.47501 42.48072), POINT (-76.…

### Selecting based on name patterns

The `scraped` data frame has many columns that follow a naming
convention where `scraped` as a prefix denotes a column scraped directly
from the online listing with no data processing. Other times we might
have suffixes for columns that denote the year of measurement for a
dataset where rows capture unique people or households (or some other
unit) that were measured on multiple occasions over time. We can use
`starts_with()` and `ends_with()` to quickly grab column subsets based
on pattern matching.

``` r
scraped_cols <- select(scraped, starts_with("scraped"))

glimpse(scraped_cols)
```

    ## Rows: 13,153
    ## Columns: 9
    ## $ scraped_beds            <chr> "2BR", "1BR", "1BR", "1BR", "2BR", "2BR", "1B…
    ## $ scraped_baths           <chr> "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1B…
    ## $ scraped_rent            <chr> "$1240", "$1257", "$1005", "$1375", "$1200", …
    ## $ scraped_sqft            <chr> "1025\r\nft\r\n2", "820\r\nft\r\n2", "480\r\n…
    ## $ scraped_address         <chr> "On TCAT Route 32", "600 Warren Road near Upt…
    ## $ scraped_neighborhoods   <chr> "(37 Uptown Road #16D Ithaca, NY)", "(600 War…
    ## $ scraped_google_maps_url <chr> "https://www.google.com/maps/search/42.480390…
    ## $ scraped_avail           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ geometry                <POINT [°]> POINT (-76.47501 42.48072), POINT (-76.…

``` r
#Suppose we had a dataset where a household's information was measured each year from 2000-2010 with columns marking the year of measurement with a year suffix. If we wanted columns with information for 2004, we would use the following pseudo code.

#select(hypothetical_df, ends_with("2004"))
```

### Selecting based on column type

There are instances where we might want to select based on a condition,
like all columns that are character type. We can use the special
`where()` function within select to grab such columns.

``` r
char_cols <- select(scraped, where(is_character))

glimpse(char_cols)
```

    ## Rows: 13,153
    ## Columns: 13
    ## $ listing_loc             <chr> "Ithaca", "Ithaca", "Ithaca", "Ithaca", "Itha…
    ## $ listing_title           <chr> "Stunning 2 bedroom Balcony Available 4/6!", …
    ## $ scraped_beds            <chr> "2BR", "1BR", "1BR", "1BR", "2BR", "2BR", "1B…
    ## $ scraped_baths           <chr> "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1B…
    ## $ scraped_rent            <chr> "$1240", "$1257", "$1005", "$1375", "$1200", …
    ## $ scraped_sqft            <chr> "1025\r\nft\r\n2", "820\r\nft\r\n2", "480\r\n…
    ## $ scraped_address         <chr> "On TCAT Route 32", "600 Warren Road near Upt…
    ## $ scraped_neighborhoods   <chr> "(37 Uptown Road #16D Ithaca, NY)", "(600 War…
    ## $ scraped_google_maps_url <chr> "https://www.google.com/maps/search/42.480390…
    ## $ scraped_avail           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ post_id                 <chr> "post id: 7089197572", "post id: 7086433186",…
    ## $ post_origin             <chr> "3 days ago\r\n 2020-03-07 15:14", "7 days ag…
    ## $ geometry                <POINT [°]> POINT (-76.47501 42.48072), POINT (-76.…

### Select a range of adjacent columns

We can also select a range of columns that are adjacent to each other by
using the `:` operator to denote a sequence of columns. We could select
all columns from `listing_date` to `scraped_sqft` using the following:

``` r
col_range <- select(scraped, listing_date:scraped_sqft)

glimpse(col_range)
```

    ## Rows: 13,153
    ## Columns: 8
    ## $ listing_date  <date> 2020-02-08, 2020-02-08, 2020-02-01, 2020-02-03, 2020-0…
    ## $ listing_loc   <chr> "Ithaca", "Ithaca", "Ithaca", "Ithaca", "Ithaca", "Itha…
    ## $ listing_title <chr> "Stunning 2 bedroom Balcony Available 4/6!", "2 Bedroom…
    ## $ scraped_beds  <chr> "2BR", "1BR", "1BR", "1BR", "2BR", "2BR", "1BR", "1BR",…
    ## $ scraped_baths <chr> "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba",…
    ## $ scraped_rent  <chr> "$1240", "$1257", "$1005", "$1375", "$1200", "$1240", "…
    ## $ scraped_sqft  <chr> "1025\r\nft\r\n2", "820\r\nft\r\n2", "480\r\nft\r\n2", …
    ## $ geometry      <POINT [°]> POINT (-76.47501 42.48072), POINT (-76.46898 42.4…

### `pull()` vs `select()`

If we want to grab a column of a data frame and return the value as a
vector (like using `$` in `df$var`), we use the `pull()` verb. This is
like `select()` but is limited to a single column and returns a vector.

``` r
pull(scraped, listing_date)
```

    ##   [1] "2020-02-08" "2020-02-08" "2020-02-01" "2020-02-03" "2020-02-03"
    ##   [6] "2020-02-03" "2020-02-03" "2020-02-03" "2020-02-03" "2020-02-03"
    ##  [11] "2020-02-03" "2020-02-03" "2020-02-03" "2020-02-03" "2020-02-03"
    ##  [16] "2020-02-04" "2020-02-07" "2020-02-04" "2020-02-04" "2020-02-04"
    ##  [21] "2020-02-05" "2020-02-05" "2020-02-05" "2020-02-06" "2020-02-06"
    ##  [26] "2020-02-07" "2020-02-07" "2020-02-07" "2020-02-07" "2020-02-08"
    ##  [31] "2020-02-08" "2020-02-10" "2020-02-10" "2020-02-10" "2020-02-10"
    ##  [36] "2020-02-11" "2020-02-12" "2020-02-12" "2020-02-13" "2020-02-13"
    ##  [41] "2020-02-15" "2020-02-16" "2020-02-16" "2020-02-16" "2020-02-16"
    ##  [46] "2020-02-16" "2020-02-16" "2020-02-17" "2020-02-17" "2020-02-17"
    ##  [51] "2020-02-17" "2020-02-17" "2020-02-17" "2020-02-17" "2020-02-17"
    ##  [56] "2020-02-17" "2020-02-17" "2020-02-17" "2020-02-17" "2020-02-17"
    ##  [61] "2020-02-19" "2020-02-19" "2020-02-19" "2020-02-19" "2020-02-19"
    ##  [66] "2020-02-19" "2020-02-19" "2020-02-20" "2020-02-20" "2020-02-20"
    ##  [71] "2020-02-20" "2020-02-20" "2020-02-20" "2020-02-20" "2020-02-20"
    ##  [76] "2020-02-20" "2020-02-21" "2020-02-21" "2020-02-21" "2020-02-21"
    ##  [81] "2020-02-21" "2020-02-21" "2020-01-30" "2020-01-26" "2020-01-27"
    ##  [86] "2020-01-27" "2020-01-27" "2020-01-27" "2020-01-28" "2020-01-28"
    ##  [91] "2020-01-28" "2020-01-28" "2020-01-28" "2020-01-29" "2020-01-29"
    ##  [96] "2020-01-30" "2020-01-30" "2020-01-30" "2020-01-30" "2020-01-30"
    ##  [ reached 'max' / getOption("max.print") -- omitted 13053 entries ]

<br>

## `mutate()`

Now that we have the tools to trim data to particular rows and columns
using `filter()` and `select()`, we can focus on how we might create new
columns or new data frames (respectively) using the `mutate()` and
`summarize()` functions.

### Making a new column

Let’s say we want to mutate a column that flags whether a listing is a 1
bedroom unit or not. We pass scraped as our first argument, and then set
our second argument to be an expression that assigns values to a column
with a new name not already present in our data frame. We use the
`mutate()` and say that our new variable `is_1br` equals whether or not
`scraped_beds == "1BR"`

``` r
#basic idea: mutate(our_df, new_var = some expression or function that returns one value for each row)

#we need to use mutate with assignment to ensure our new column is saved
#here we add a new column to existing data frame scraped, 
#but we can also create entirely new data frames
scraped <- mutate(scraped, is_1br = scraped_beds == "1BR")

glimpse(scraped)
```

    ## Rows: 13,153
    ## Columns: 15
    ## $ listing_date            <date> 2020-02-08, 2020-02-08, 2020-02-01, 2020-02-…
    ## $ listing_loc             <chr> "Ithaca", "Ithaca", "Ithaca", "Ithaca", "Itha…
    ## $ listing_title           <chr> "Stunning 2 bedroom Balcony Available 4/6!", …
    ## $ scraped_beds            <chr> "2BR", "1BR", "1BR", "1BR", "2BR", "2BR", "1B…
    ## $ scraped_baths           <chr> "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1B…
    ## $ scraped_rent            <chr> "$1240", "$1257", "$1005", "$1375", "$1200", …
    ## $ scraped_sqft            <chr> "1025\r\nft\r\n2", "820\r\nft\r\n2", "480\r\n…
    ## $ scraped_address         <chr> "On TCAT Route 32", "600 Warren Road near Upt…
    ## $ scraped_neighborhoods   <chr> "(37 Uptown Road #16D Ithaca, NY)", "(600 War…
    ## $ scraped_google_maps_url <chr> "https://www.google.com/maps/search/42.480390…
    ## $ scraped_avail           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ post_id                 <chr> "post id: 7089197572", "post id: 7086433186",…
    ## $ post_origin             <chr> "3 days ago\r\n 2020-03-07 15:14", "7 days ag…
    ## $ geometry                <POINT [°]> POINT (-76.47501 42.48072), POINT (-76.…
    ## $ is_1br                  <lgl> FALSE, TRUE, TRUE, TRUE, FALSE, FALSE, TRUE, …

``` r
summary(scraped$is_1br)
```

    ##    Mode   FALSE    TRUE    NA's 
    ## logical    9042    3738     373

We can see from `summary(scraped$is_1br)` that this preserves `NA`
values from `scraped_beds`. If there was no valid value for
`scraped_beds` it does not take on a value in `is_1br`. This new column
is of type logical, since it can only take on `TRUE` or `FALSE` values.

### Using another function within mutate()

This kind of logical column for conditions can be useful, but many times
we want to create a new column based on manipulating values of an
existing one. Here we will use other functions within `mutate()` to make
this happen.

Right now, our data frame has many character columns where numeric
columns might be more advantageous. Examples include `scraped_beds`,
`scraped_baths`, `scraped_rent` and `scraped_sqft` since they all could
be simplified to a numeric value that could be used for arithmetic or
statistical computations.

Let’s use the `parse_number()` function from the `readr` library to
create a new column that captures what number was present in the
`scraped_beds` field.

``` r
scraped <- mutate(scraped, clean_beds = parse_number(scraped_beds))

glimpse(scraped)
```

    ## Rows: 13,153
    ## Columns: 16
    ## $ listing_date            <date> 2020-02-08, 2020-02-08, 2020-02-01, 2020-02-…
    ## $ listing_loc             <chr> "Ithaca", "Ithaca", "Ithaca", "Ithaca", "Itha…
    ## $ listing_title           <chr> "Stunning 2 bedroom Balcony Available 4/6!", …
    ## $ scraped_beds            <chr> "2BR", "1BR", "1BR", "1BR", "2BR", "2BR", "1B…
    ## $ scraped_baths           <chr> "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1B…
    ## $ scraped_rent            <chr> "$1240", "$1257", "$1005", "$1375", "$1200", …
    ## $ scraped_sqft            <chr> "1025\r\nft\r\n2", "820\r\nft\r\n2", "480\r\n…
    ## $ scraped_address         <chr> "On TCAT Route 32", "600 Warren Road near Upt…
    ## $ scraped_neighborhoods   <chr> "(37 Uptown Road #16D Ithaca, NY)", "(600 War…
    ## $ scraped_google_maps_url <chr> "https://www.google.com/maps/search/42.480390…
    ## $ scraped_avail           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ post_id                 <chr> "post id: 7089197572", "post id: 7086433186",…
    ## $ post_origin             <chr> "3 days ago\r\n 2020-03-07 15:14", "7 days ag…
    ## $ geometry                <POINT [°]> POINT (-76.47501 42.48072), POINT (-76.…
    ## $ is_1br                  <lgl> FALSE, TRUE, TRUE, TRUE, FALSE, FALSE, TRUE, …
    ## $ clean_beds              <dbl> 2, 1, 1, 1, 2, 2, 1, 1, 1, 1, 1, 2, 2, 2, 2, …

R returns a warning because some of these scraped values did not contain
a number in them. These rows accordingly have a `NA` for `clean_beds`.
We can check our work by first filtering to the rows with `NA` values in
`clean_beds` and then selecting the scraped and clean columns for
inspection.

``` r
beds_na <- filter(scraped, is.na(clean_beds))

select(beds_na, scraped_beds, clean_beds)
```

    ## Simple feature collection with 373 features and 2 fields
    ## geometry type:  POINT
    ## dimension:      XY
    ## bbox:           xmin: -76.61429 ymin: 42.40418 xmax: -76.18002 ymax: 42.6036
    ## geographic CRS: WGS 84
    ## First 10 features:
    ##    scraped_beds clean_beds                   geometry
    ## 1          <NA>         NA POINT (-76.48267 42.44552)
    ## 2          <NA>         NA POINT (-76.48267 42.44552)
    ## 3          <NA>         NA   POINT (-76.49708 42.445)
    ## 4          <NA>         NA POINT (-76.48267 42.44552)
    ## 5          <NA>         NA POINT (-76.48267 42.44552)
    ## 6          <NA>         NA POINT (-76.48267 42.44552)
    ## 7          <NA>         NA   POINT (-76.49708 42.445)
    ## 8          <NA>         NA POINT (-76.48267 42.44552)
    ## 9          <NA>         NA POINT (-76.48267 42.44552)
    ## 10         <NA>         NA   POINT (-76.49708 42.445)

### Overwriting an existing column

In looking at a summary of this new variable `clean_beds`, we can see
that at least one user mistakenly put the rent value in the bedroom
field. This shows how online data can be messy because they are user
volunteered information.

We can use the `ifelse()` function to deal with implausible values and
set them to `NA`. Let’s say that 6 bedrooms (a very large house) is the
ceiling we want to set for our new variable. The `ifelse()` function
allows us to vary what we do in a mutate function based on some
expression that we set. The syntax is `ifelse(condition, if_true,
else)`.

``` r
scraped <- mutate(scraped, clean_beds = ifelse(clean_beds > 6, NA, clean_beds))

summary(scraped$clean_beds)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   0.000   1.000   2.000   2.057   3.000   6.000     505

### Mutating multiple columns at once

If we want to do a set of column mutates in one fell swoop, we pass
additional arguments to `mutate()` like in the following code where each
argument has its own line:

``` r
#first parse character to numeric
scraped <- mutate(scraped, 
                  clean_rent = parse_number(scraped_rent),
                  clean_sqft = parse_number(scraped_sqft),
                  clean_baths = parse_number(scraped_baths))
```

    ## Warning: 582 parsing failures.
    ## row col expected        actual
    ## 401  -- a number available now
    ## 409  -- a number available now
    ## 438  -- a number -            
    ## 500  -- a number available now
    ## 508  -- a number available now
    ## ... ... ........ .............
    ## See problems(...) for more details.

    ## Warning: 84 parsing failures.
    ##  row col expected   actual
    ##  296  -- a number sharedBa
    ##  367  -- a number sharedBa
    ##  454  -- a number sharedBa
    ##  975  -- a number sharedBa
    ## 1306  -- a number sharedBa
    ## .... ... ........ ........
    ## See problems(...) for more details.

``` r
glimpse(scraped)
```

    ## Rows: 13,153
    ## Columns: 19
    ## $ listing_date            <date> 2020-02-08, 2020-02-08, 2020-02-01, 2020-02-…
    ## $ listing_loc             <chr> "Ithaca", "Ithaca", "Ithaca", "Ithaca", "Itha…
    ## $ listing_title           <chr> "Stunning 2 bedroom Balcony Available 4/6!", …
    ## $ scraped_beds            <chr> "2BR", "1BR", "1BR", "1BR", "2BR", "2BR", "1B…
    ## $ scraped_baths           <chr> "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1Ba", "1B…
    ## $ scraped_rent            <chr> "$1240", "$1257", "$1005", "$1375", "$1200", …
    ## $ scraped_sqft            <chr> "1025\r\nft\r\n2", "820\r\nft\r\n2", "480\r\n…
    ## $ scraped_address         <chr> "On TCAT Route 32", "600 Warren Road near Upt…
    ## $ scraped_neighborhoods   <chr> "(37 Uptown Road #16D Ithaca, NY)", "(600 War…
    ## $ scraped_google_maps_url <chr> "https://www.google.com/maps/search/42.480390…
    ## $ scraped_avail           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ post_id                 <chr> "post id: 7089197572", "post id: 7086433186",…
    ## $ post_origin             <chr> "3 days ago\r\n 2020-03-07 15:14", "7 days ag…
    ## $ geometry                <POINT [°]> POINT (-76.47501 42.48072), POINT (-76.…
    ## $ is_1br                  <lgl> FALSE, TRUE, TRUE, TRUE, FALSE, FALSE, TRUE, …
    ## $ clean_beds              <dbl> 2, 1, 1, 1, 2, 2, 1, 1, 1, 1, 1, 2, 2, 2, 2, …
    ## $ clean_rent              <dbl> 1240, 1257, 1005, 1375, 1200, 1240, 1257, 125…
    ## $ clean_sqft              <dbl> 1025, 820, 480, 1, 1025, 1025, 820, 820, 820,…
    ## $ clean_baths             <dbl> 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, …

We would want to now set ceiling and floor values for these columns to
adjudicate issues with what users inputs or what our scrapers identified
for the column value.

``` r
#first parse character to numeric
scraped <- mutate(scraped, 
                  clean_rent = ifelse(clean_rent < 100, NA, clean_rent),
                  clean_rent = ifelse(clean_rent > 5000, NA, clean_rent),
                  clean_sqft = ifelse(clean_sqft < 50, NA, clean_sqft),
                  clean_sqft = ifelse(clean_sqft > 10000, NA, clean_sqft),
                  clean_baths = ifelse(clean_baths > 10, NA, clean_baths))

summary(scraped$clean_rent)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##     121    1028    1378    1429    1650    4800      57

### Making a categorical variable (i.e. factor type)

Factor type variables can be useful if we want to establish an ordered
variable where values are labelled but arithmetic is not appropriate. An
example we will use here is a categorical measure of bedroom sizes for
apartments where we truncate the top value to be “4+” and capture all
listings for units with 4 bedrooms or more with this factor level.

`dplyr` has a function called `case_when()` that allows us to specify
such a variable with appropriate expressions

``` r
scraped <- mutate(scraped,
                  cat_beds = case_when(
                    clean_beds == 0 ~ "0",
                    clean_beds == 1 ~ "1",
                    clean_beds == 2 ~ "2",
                    clean_beds == 3 ~ "3",
                    clean_beds >= 4 ~ "4+"
                  ))

#tabulate counts for this variable, be sure to print NAs with argument useNA = "always"
table(scraped$cat_beds, useNA = "always")
```

    ## 
    ##    0    1    2    3   4+ <NA> 
    ##  626 3738 4229 3090  965  505

``` r
scraped <- mutate(scraped, clean_post  = parse_number(post_id))
feb_listings <- filter(scraped, listing_date >= "2020-02-01" & listing_date < "2020-03-01")
summary(feb_listings)
```

    ##   listing_date        listing_loc        listing_title      scraped_beds      
    ##  Min.   :2020-02-01   Length:656         Length:656         Length:656        
    ##  1st Qu.:2020-02-16   Class :character   Class :character   Class :character  
    ##  Median :2020-02-24   Mode  :character   Mode  :character   Mode  :character  
    ##  Mean   :2020-02-19                                                           
    ##  3rd Qu.:2020-02-26                                                           
    ##  Max.   :2020-02-29                                                           
    ##                                                                               
    ##  scraped_baths      scraped_rent       scraped_sqft       scraped_address   
    ##  Length:656         Length:656         Length:656         Length:656        
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##  scraped_neighborhoods scraped_google_maps_url scraped_avail     
    ##  Length:656            Length:656              Length:656        
    ##  Class :character      Class :character        Class :character  
    ##  Mode  :character      Mode  :character        Mode  :character  
    ##                                                                  
    ##                                                                  
    ##                                                                  
    ##                                                                  
    ##    post_id          post_origin                 geometry     is_1br       
    ##  Length:656         Length:656         POINT        :656   Mode :logical  
    ##  Class :character   Class :character   epsg:4326    :  0   FALSE:456      
    ##  Mode  :character   Mode  :character   +proj=long...:  0   TRUE :191      
    ##                                                            NA's :9        
    ##                                                                           
    ##                                                                           
    ##                                                                           
    ##    clean_beds      clean_rent     clean_sqft    clean_baths   
    ##  Min.   :0.000   Min.   : 500   Min.   : 387   Min.   :0.000  
    ##  1st Qu.:1.000   1st Qu.:1091   1st Qu.: 840   1st Qu.:1.000  
    ##  Median :2.000   Median :1395   Median :1000   Median :1.000  
    ##  Mean   :2.179   Mean   :1448   Mean   :1104   Mean   :1.253  
    ##  3rd Qu.:3.000   3rd Qu.:1690   3rd Qu.:1200   3rd Qu.:1.250  
    ##  Max.   :6.000   Max.   :4800   Max.   :3250   Max.   :5.000  
    ##  NA's   :18      NA's   :2      NA's   :203    NA's   :13     
    ##    cat_beds           clean_post       
    ##  Length:656         Min.   :7.052e+09  
    ##  Class :character   1st Qu.:7.079e+09  
    ##  Mode  :character   Median :7.086e+09  
    ##                     Mean   :7.086e+09  
    ##                     3rd Qu.:7.090e+09  
    ##                     Max.   :7.105e+09  
    ## 

If we want to `filter()` or create expressions with this new categorical
variable, we need to remember that values must be quoted.

<br>

## `summarize()`

If we have a set of data that we want to get *overall* statistics on,
like counts or averages, we can use the `summarize()` verb that `dplyr`
provides. Let’s try counting the number of 2 bedroom units in our data.
We will use summarize by itself at first, but this verb becomes much
more powerful after we combine it with the `group_by()` verb in order to
create groupwise summaries (e.g., average rent for 0B, 1B, 2B, etc by
grouping by `clean_beds`).

The most important thing to remember is that `mutate()` expects us to
provide it with functions that will produce as many values as there are
rows in the data. In contrast, `summarize()` expects us to provide it
with a function that will evaluate to a single value.

### Tallying counts

Here we call `summarize()` with our data frame as the first argument,
then we set up an equation that assigns values to a new variable
`total_2b` using the `sum()` of an expression for whether the
`clean_beds` column equaled 2. This syntax is similar to `mutate()`, but
the exception is that we compute a value that describes the *entire*
data set, as opposed to a values for each row. `mutate()` creates new
columns within an existing data frame, whereas `summarize()` creates new
columns in a new data frame.

``` r
summarize(scraped, total_2b = sum(clean_beds == 2))
```

    ## Simple feature collection with 1 feature and 1 field
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.90302 ymin: 42.10337 xmax: -76.03615 ymax: 42.93978
    ## geographic CRS: WGS 84
    ##   total_2b                       geometry
    ## 1       NA MULTIPOINT ((-78.90302 42.9...

When we run this code, we should immediately notice that the new column
of interest `total_2b` has `NA` for its value. This is because when we
tried to compute the sum of rows where `clean_beds` equaled 2, `sum()`
encountered `NA` values that it doesn’t know what to do with.

We can resolve this in a couple different ways. We can either `filter()`
out NA values permanently using an expression that says “keep rows if
they are not NA for some column”

``` r
new_df <- filter(scraped, !is.na(clean_beds))
```

Or, we can resolve this by telling `sum()` to simply ignore/remove `NA`
values during the computation:

``` r
summarize(scraped, total_2b = sum(clean_beds == 2, na.rm = TRUE))
```

    ## Simple feature collection with 1 feature and 1 field
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.90302 ymin: 42.10337 xmax: -76.03615 ymax: 42.93978
    ## geographic CRS: WGS 84
    ##   total_2b                       geometry
    ## 1     4229 MULTIPOINT ((-78.90302 42.9...

### Computing averages

`summarize()` is like `mutate()` in the sense that it is a broad
framework for manipulating data into a new structure using other
functions. We can do very simple computations like a `mean()`, but
should we have functions for computing advanced statistics, inequality
indices or other values, we could use them within `summarize()` too.

``` r
summarize(scraped, mean_rent = mean(clean_rent, na.rm = TRUE))
```

    ## Simple feature collection with 1 feature and 1 field
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.90302 ymin: 42.10337 xmax: -76.03615 ymax: 42.93978
    ## geographic CRS: WGS 84
    ##   mean_rent                       geometry
    ## 1  1428.989 MULTIPOINT ((-78.90302 42.9...

### Other summary functions

Common summary statistic functions include `median()`, `min`, `max()`,
`length(unique())`, `sd()`. Each of these can be used within the context
of `summarize()` since they will compute these statistics over all rows
in the data frame and return a single value.

Like `mutate()`, we can compute multiple summary columns in a single
`summarize()` function call.

``` r
rent_tab <-
  summarize(scraped, 
          med_rent = median(clean_rent, na.rm = TRUE),
          min_rent = min(clean_rent, na.rm = TRUE),
          max_rent = max(clean_rent, na.rm = TRUE),
          unique_rent = length(unique(clean_rent, na.rm = TRUE)),
          sd_rent = sd(clean_rent, na.rm = TRUE))
print(rent_tab)
```

    ## Simple feature collection with 1 feature and 5 fields
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.90302 ymin: 42.10337 xmax: -76.03615 ymax: 42.93978
    ## geographic CRS: WGS 84
    ##   med_rent min_rent max_rent unique_rent  sd_rent
    ## 1   1377.5      121     4800         445 635.7105
    ##                         geometry
    ## 1 MULTIPOINT ((-78.90302 42.9...

<br>

## “Piping” `dplyr` functions with the magrittr `%>%` operator

Now that we know some of the most essential `dplyr` functions, let’s
take a minute to learn how we can “pipe” multiple functions together
into a set of data manipulation tasks. This is useful if, for example,
we want to first do some filtering, then make a column or two, and then
summarize overall information about the data set.

The `magrittr` library that is part of the `tidyverse` adds the `%>%`
operator to R for piping functions. The basic idea is that `%>%` passes
the results of the prior function call to the next one as the first
argument. The end result is identical.

``` r
#instead of:
no_pipe <- filter(scraped, clean_beds == 2)

#we can use the pipe operator %>% to pass scraped to filter()
w_pipe <- scraped %>% filter(clean_beds == 2)

identical(no_pipe, w_pipe)
```

    ## [1] TRUE

This may not seem advantageous at first, but the power of this syntax
change comes through chaining multiple operations together. In the
following example we will filter to 2 bedroom listings and then
summarize this filtered set’s median rent asked. We save this result to
new object `med_2b` and then print it to console.

``` r
med_2b <- scraped %>% filter(clean_beds == 2, !is.na(clean_rent)) %>% summarize(med_rent = median(clean_rent))

med_2b
```

    ## Simple feature collection with 1 feature and 1 field
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -76.8791 ymin: 42.10337 xmax: -76.03615 ymax: 42.63714
    ## geographic CRS: WGS 84
    ##   med_rent                       geometry
    ## 1     1425 MULTIPOINT ((-76.8791 42.38...

If we omit assignment with `<-` or `=`, the result of our pipe is
printed to console rather than saved to an object (whether new or
through overwriting an existing one).

### Emphasizing legibility by writing code vertically

The `%>%` pipe operator is therefore powerful for handling complex data
manipulations in a manner that just requires us to think about what
`dplyr` verbs are needed for each step. This makes `dplyr` an efficient
way to think about and write code for analyses.

However, the second real advantage that comes with using `dplyr` and
`%>%` together comes from switching from writing code horizontally to
writing code vertically. In the prior example, you can see how using 3
or more functions quickly starts to use up our screen real estate. We
solve this problem by writing vertically, and we also make it clear that
each set of steps builds on the prior function’s output. Altogether,
this helps to make `dplyr` code easy to read and understand as a set of
tasks that are chained together with the `%>%` pipe.

Look at the following example where we do the extend the task as before
but with writing vertically instead:

``` r
rent_2b <- scraped %>% 
  filter(cat_beds == "2", !is.na(clean_rent)) %>% 
  summarize(med_rent = median(clean_rent),
            mean_rent = mean(clean_rent),
            sd_rent = sd(clean_rent))

rent_2b
```

    ## Simple feature collection with 1 feature and 3 fields
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -76.8791 ymin: 42.10337 xmax: -76.03615 ymax: 42.63714
    ## geographic CRS: WGS 84
    ##   med_rent mean_rent  sd_rent                       geometry
    ## 1     1425  1397.009 282.3962 MULTIPOINT ((-76.8791 42.38...

### Best practices for pipes

There is no hard and fast rule for how much is too much piping, but a
good practice is to write pipes that accomplish a coherent set of tasks.
We want to avoid writing *everything* in a script as a pipe, because
sometimes it is important to save intermediary objects as a way of
building from point A to point B. If everything is all one pipe and it
fails, it can become hard to debug the code to find out at what point
our pipe is breaking.

<br>

## `group_by()`

A common task in data wrangling involves computing *groupwise*
statistics. An example would be to compute the average square footage of
units based on their bedroom size, or the average income of persons
based on demographic characteristics (e.g., age, sex, gender, race,
ethnicity).

We can use the `group_by()` function in combination with our other
`dplyr` verbs and the pipe operator `%>%` to accomplish a lot in just a
few lines of code.

### Groupwise summaries

One use of `group_by()` is in tandem with `summarize()`, where we
produce a new data frame based on summary statistics of each level of
the grouping variable. This means if we have 5 groups, the new data
frame will have 5 rows with columns indicating the values computed for
each group.

``` r
scraped %>% #take our listing data
  filter(!is.na(cat_beds)) %>% #remove rows with missing values
  group_by(cat_beds) %>% #group the data by bedroom size
  tally() %>% #compute number of listings for each bedroom size
  ungroup() %>%
  mutate(prop = n/sum(n))
```

    ## Simple feature collection with 5 features and 3 fields
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.90302 ymin: 42.10337 xmax: -76.03615 ymax: 42.93978
    ## geographic CRS: WGS 84
    ## # A tibble: 5 x 4
    ##   cat_beds     n                                                 geometry   prop
    ## * <chr>    <int>                                         <MULTIPOINT [°]>  <dbl>
    ## 1 0          626 ((-76.67021 42.44205), (-76.66258 42.54207), (-76.52865… 0.0495
    ## 2 1         3738 ((-78.90302 42.93978), (-76.86736 42.38024), (-76.72492… 0.296 
    ## 3 2         4229 ((-76.8791 42.38874), (-76.87419 42.38192), (-76.81691 … 0.334 
    ## 4 3         3090 ((-78.66828 42.7929), (-76.66245 42.53932), (-76.66099 … 0.244 
    ## 5 4+         965 ((-76.6615 42.54334), (-76.6572 42.5405), (-76.58563 42… 0.0763

The `n()` function is a useful for tool for counting the number of
observations in each level of our grouping variable. We can use
`tally()` is a shortcut to `summarize(n = n())`.

We can also compute statistics like medians or averages using
`summarize()`:

``` r
scraped %>% #take our listing data
  filter(!is.na(clean_rent), !is.na(cat_beds)) %>% #remove rows with missing values
  group_by(cat_beds) %>% #group the data by bedroom size
  summarize(med_rent = median(clean_rent)) #compute median rents
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## Simple feature collection with 5 features and 2 fields
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.90302 ymin: 42.10337 xmax: -76.03615 ymax: 42.93978
    ## geographic CRS: WGS 84
    ## # A tibble: 5 x 3
    ##   cat_beds med_rent                                                     geometry
    ##   <chr>       <dbl>                                             <MULTIPOINT [°]>
    ## 1 0            1210 ((-76.67021 42.44205), (-76.66258 42.54207), (-76.52865 42.…
    ## 2 1            1127 ((-78.90302 42.93978), (-76.86736 42.38024), (-76.72492 42.…
    ## 3 2            1425 ((-76.8791 42.38874), (-76.87419 42.38192), (-76.81691 42.1…
    ## 4 3            1815 ((-78.66828 42.7929), (-76.66245 42.53932), (-76.66099 42.5…
    ## 5 4+           2000 ((-76.6615 42.54334), (-76.6572 42.5405), (-76.58563 42.481…

### Groupwise mutates

Another grouped operation would be to compute a new column in the
original input data frame that is based on group values. Here we compute
the difference between each row’s rent asked and the average rent asked
for a given bedroom size. This could be used to understand which
listings are relatively more or less expensive than others advertised
during the timespan of our data.

``` r
tempo <-
  scraped %>% #take our listing data
    filter(!is.na(clean_rent), !is.na(cat_beds)) %>% #remove rows with missing values
    group_by(cat_beds) %>% #group the data by bedroom size
    mutate(rent_diff = clean_rent - mean(clean_rent)) #compute difference of listing's rent and the average rent for apartments of its bedroom size
options(scipen = 99)
summary(tempo$rent_diff)
```

    ##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
    ## -1733.56  -202.01    36.99     0.00   202.99  2566.44

### Multiple grouping variables

We can use multiple grouping variables too. In this example:

  - First we use a function to first grab the month that a listing was
    in, save this as a new column
  - Then we group by bedroom size and listing month
  - Finally, we’ll compute the typical (i.e. median) rent observed in
    each month for each bedroom size.

<!-- end list -->

``` r
med_by_month <- scraped %>% #start with scraped, save result of pipe as med_by_month
  filter(!is.na(clean_rent)) %>% #filter out NAs
  mutate(listing_month = month(listing_date)) %>% #make new column that indicates month listed
  group_by(clean_beds, listing_month) %>% #group the data by bedroom size AND listing month
  summarize(median_rent = median(clean_rent)) #compute monthly median for each bed size
```

    ## `summarise()` regrouping output by 'clean_beds' (override with `.groups` argument)

``` r
med_by_month %>% select(listing_month, median_rent)
```

    ## Simple feature collection with 38 features and 2 fields
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.90302 ymin: 42.10337 xmax: -76.03615 ymax: 42.93978
    ## geographic CRS: WGS 84
    ## # A tibble: 38 x 3
    ##    listing_month median_rent                                            geometry
    ##            <dbl>       <dbl>                                    <MULTIPOINT [°]>
    ##  1             2         925 ((-76.49886 42.43735), (-76.494 42.42955), (-76.49…
    ##  2             3         925 ((-76.50153 42.43563), (-76.50043 42.44837), (-76.…
    ##  3             4        1143 ((-76.66258 42.54207), (-76.52865 42.46008), (-76.…
    ##  4             5        1242 ((-76.67021 42.44205), (-76.52865 42.46008), (-76.…
    ##  5             1        1227 ((-78.90302 42.93978), (-76.52861 42.46004), (-76.…
    ##  6             2        1200 ((-78.90302 42.93978), (-76.66299 42.54206), (-76.…
    ##  7             3        1199 ((-76.68798 42.29159), (-76.66191 42.54604), (-76.…
    ##  8             4        1107 ((-76.72492 42.61949), (-76.68798 42.29159), (-76.…
    ##  9             5        1050 ((-76.86736 42.38024), (-76.66191 42.54604), (-76.…
    ## 10             1        1415 ((-76.54294 42.46598), (-76.53559 42.46468), (-76.…
    ## # … with 28 more rows

This example shows how we can use multiple grouping variables to create
more complex summary tables. We might group by a number of demographic
variables when working with person-level data, or use a time index like
in this case when working with household panel data (where a given
household is surveyed on multiple occasions over some timespan).

<br>

## `arrange()`

`arrange()` is the `dplyr` verb that we have not discussed yet allows us
to sort the data frame by some variable. This is an important task in
some instances where row order matters for a computation, OR where
ordering the data by some values helps make the table more legible
(e.g., sorting the values about U.S. cities by alphabetically by name or
by descending population size).

### Ascending

The simplest use of `arrange()` is to just pass it a single variable. In
the following we *finally* get around to reordering `scraped` by
listing\_date (oldest -\> newest). By assigning the result of the pipe
to the name of the starting object, we overwrite `scraped` with this
newly sorted version of the same data.

``` r
scraped <- scraped %>%
  arrange(listing_date)
```

### Descending

We can use `desc()` for the variable we sort by to achieve a sorted
table based on descending values (in this case, newest -\> oldest)

``` r
scraped <- scraped %>%
  arrange(desc(listing_date))
```

<br>

## Bringing it all together

This overview has equipped you with a robust set of tools for doing data
analyses of your own. While we have just covered the basics here, we can
use the `dplyr` verbs by themselves or with other software libraries to
tackle whatever analytic tasks we may encounter.

<br>

<hr>

<br>

# Part B: Learning the basics of `ggplot2` for data visualization

The second focus of this lab is to introduce the “grammar of graphics”
that `ggplot2` uses.

`ggplot2` is a programming interface for high-quality data
visualizations based on the idea that the *data* should be what you
think about the most when creating a visualization. Many alternative
approaches to data visualization require learning a specific syntax for
each type of visualization you might want to produce.

Basic plots include:

  - histogram - demonstrate distribution of a single variable
  - scatterplot - show relationship between two variables
  - bar chart - illustrate differences by group in one or more variables
  - line chart - describe differences within group over time or
    according to another variable

These are essential types of data visualization and `ggplot2` can be
used to quickly assemble beautiful versions of these graphics. The true
value of `ggplot2`, however, is that it brings these visualizations,
along with really any other visualization you can dream up into a
coherent framework. Instead of learning a new function with new syntax
for each type of graphic you want to make, `ggplot2` makes all of
graphics expressible through a single “grammar”.

## A quick example

### Preparing data for plotting

Let’s dive into an example to demonstrate how `ggplot2` works. We will
first prepare a data frame to use for plotting using `dplyr` functions:

``` r
#first, let's create a data frame for plotting
scraped_no_geo <- scraped %>%
  
  #we will drop rows with missing data on columns of interest and limit the bedroom sizes
  filter(!is.na(clean_sqft), !is.na(clean_rent), !is.na(cat_beds)) %>%
  filter(cat_beds %in% c("1", "2", "3")) %>%
  
  #we will make a month column
  mutate(listing_month = month(listing_date)) %>%
  
  #now limit to march through may
  filter(listing_month %in% c(3, 4, 5)) %>%
  
  #we will also drop the geometry column in this because we are not making spatial plots
  st_drop_geometry() %>%
  
  #finally we'll make sure our data aren't grouped from the prior dplyr examples
  ungroup()
```

### Making our plot

We are interested in the relationship between the square footage of a
rental unit and the rent that the landlord is asking. We might expect
there to be a *positive association* where larger rental units tend to
command higher asking rents.

Starting from the left of the first line: we will call `ggplot()` and
make our first argument a data frame. This tells ggplot that we want
this data frame to be the focus of our plot.

Then we get to `aes()`. This defines the *aesthetics* of our plot. The
aesthetics of our plot define how variables map onto plot dimensions.
These dimensions can by `x` and `y`, like on a Cartesian coordinate
system, but also things like the `color` or `size` of items that we plot
with a `geom` function. Here we map `clean_sqft` to the `x` aesthetic
and `clean_rent` to the `y` aesthetic in order to visualize if there is
a relationship between the size of an apartment and the rent that
landlords are asking for it.

Finally, we add to this `ggplot()` function a `geom_point()` function
that says to plot those aesthetics using a point for each observation.
We will talking later about how `ggplot2` expects data to be structured
as well as what `geom`s we have available for plotting. If we don’t pass
`ggplot2` a geom, then R will print a blank plot (possibly with axes if
we defined them).

``` r
#now that we have made the data frame we need, let's make a plot as our second step
ggplot(scraped_no_geo, aes(x = clean_sqft, y = clean_rent)) +
  geom_point()
```

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-47-1.png)<!-- -->

So key takeaways so far:

  - give `ggplot()` a data frame as the first argument
  - define your aesthetics with the second argument `aes()`
  - add a `geom` to define how the aesthetics get plotted

## Tidy data

To become a `ggplot2` master, it helps to understand the concept of
*tidy data*. The basic notion is that we want each of our rows of data
to be able to be defined as a coherent unit of analysis. Then,
`ggplot()` will print one geom for each one row in the data frame that
we pass to it.

Right now, we have *listing* level data. When we passed it to `ggplot()`
in the prior example, we produced a plot with one point per row of data.

If we wanted a bar graph of the average rent per bedroom size (e.g., 0,
1, 2, etc), then we’d need to *first* summarize our data so that each
row of this summarized data frame denotes a bedroom size level, *then*
pass this new data frame to `ggplot()`.

This logic extends to data whether they are people, neighborhoods,
countries or widgets. `ggplot()` expects us to know that 1 row:1 geom.
So think about what the bars, points or lines of your plot are going to
be and wrangle the data accordingly.

## `aes()`-thetics

The main aesthetics of `ggplot2` include:

  - `x` - horizontal axis
  - `y` - vertical axis
  - `color` - hue of points or lines
  - `fill` - hue of inside of bars, heatmap squares,
  - `size` - plot size of points, lines, etc
  - `linetype` - whether lines are solid, dashed, dotted
  - `shape` - whether points are circles, squares, triangles, etc.

These can either be set manually or variably.

If we manually set the aesthetic value, we can make it so all geoms are
treated the same. See below where we make all points larger and into
hollow circles. We set aesthetics manually in a `geom` function. You can
see a diagram of R shapes (and their codes) [here](./etc/r-shapes.png).

``` r
ggplot(scraped_no_geo, aes(x = clean_sqft, y = clean_rent)) +
  geom_point(size = 4, shape = 1) 
```

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-48-1.png)<!-- -->

This stands in contrast to setting aesthetics with a variable. We use
the `aes()` function to define aesthetics in this manner. In the
following example we will color the points in our scatterplot with the
bedroom size categorical variable we made earlier in Part A.

``` r
ggplot(scraped_no_geo, aes(x = clean_sqft, y = clean_rent, color = cat_beds)) +
  geom_point()
```

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-49-1.png)<!-- -->

## `geom`etry functions

Common `geom` functions include:

  - `geom_point()` - plot each row of data frame as a point
  - `geom_line()` - plot rows as a connected series with a line

<!-- end list -->

``` r
sum_df <- scraped_no_geo %>%
  group_by(listing_month, cat_beds) %>%
  summarize(median = median(clean_rent))
```

    ## `summarise()` regrouping output by 'listing_month' (override with `.groups` argument)

``` r
ggplot(sum_df, aes(x = listing_month, y = median, color = cat_beds)) +
  geom_line()
```

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-50-1.png)<!-- -->

  - `geom_bar()` - plot row as a bar. We specify `stat = "identity"` to
    tell ggplot that each bar should use our `y` aesthetic which is the
    median estimates we created, as opposed to the default `stat =
    "count"` where `ggplot()` counts the number of cases at particular
    `x` values.

<!-- end list -->

``` r
sum_df <- scraped_no_geo %>%
  group_by(cat_beds) %>%
  summarize(median = median(clean_rent))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
ggplot(sum_df, aes(x = cat_beds, y = median)) +
  geom_bar(stat = "identity")
```

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-51-1.png)<!-- -->

Note how the default `stat = "count"` produces three equally sized bars
since our `sum_df` has one row for each value of `x`.

``` r
ggplot(scraped, aes(x = cat_beds)) +
  geom_bar()
```

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-52-1.png)<!-- -->

  - `geom_histogram()` - plot distribution of a variable

<!-- end list -->

``` r
ggplot(scraped_no_geo, aes(x = clean_rent)) +
  geom_histogram()
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-53-1.png)<!-- -->

  - `geom_smooth()` - add a regression line using a linear or smooth
    fit. The message R returns about `geom_smooth() using formula 'y ~
    x'` means that R is estimating a line of best fit, or regression
    line, where values of our `x` variable explain variation in our `y`
    variable. We may also refer to this as *regressing y on x*. We cover
    linear regression in more detail in Lab 4.

<!-- end list -->

``` r
ggplot(scraped_no_geo, aes(x = clean_sqft, y = clean_rent, color = cat_beds)) +
  geom_point() +
  geom_smooth(method = "lm")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-54-1.png)<!-- -->

Some annotation related geoms include:

  - `geom_vline()` / `geom_hline()` / `geom_abline()` - add line
    manually, like to denote a particular value of interest (e.g., a
    time when some policy was implemented) or to draw attention to
    differences (e.g., relative risks greater than 0). The former
    example is something we will discuss further in Lab 4.
  - `geom_text()` / `geom_label()` - add text or label for each row
    rather than point. This can be useful, for example, if points on a
    scatter plot denote particular countries or states where we can add
    a layer of information about what points are which cases with a
    simple label.

## Adding our pieces together

Here’s a more polished version of our example graphic, where we add a
`color` aesthetic, labels for the aesthetics and a simple theme to
spruce up the final product.

``` r
ggplot(scraped_no_geo, aes(x = clean_sqft, y = clean_rent, color = cat_beds)) +
  geom_point() +
  labs(x = "Unit size", y = "Rent asked", color = "Number of bedrooms") +
  scale_y_continuous(labels = scales::dollar) +
  scale_color_brewer(palette = "Reds") +
  theme_bw()
```

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-55-1.png)<!-- -->

Note how in this example we added helper functions to our `ggplot()` to
customize labels (`labs()`), scales (`scale_y_continuous()`,
`scale_color_brewer()`) and the overall plot theme (`theme_bw()`). [The
official `ggplot2`
cheatsheet](https://rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)
covers how you can add these support functions to customize each detail
of your visualization.

## Saving visualizations

We can use the `ggsave()` function to store the plot we produce as a
jpeg, png or pdf file.

``` r
ggplot(scraped_no_geo, aes(x = clean_sqft, y = clean_rent, color = cat_beds)) +
  geom_point() +
  labs(x = "Unit size", y = "Rent asked", color = "Number of bedrooms") +
  scale_y_continuous(labels = scales::dollar) +
  scale_color_brewer(palette = "Reds") +
  theme_bw() +
  ggsave(filename = "./output/ggplot_example.pdf", width = 8, height = 8)
```

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-56-1.png)<!-- -->

<br>

<hr>

<br>

# Part C: Learning the basics of `sf` for spatial analysis

## Remember how we have spatial data?

We have been using the data for this lab for various *aspatial* analyses
where we look at the distribution of one variable, the association of
two variables, or summary statistics like `median()` values of one
variable across another grouping variable.

In this final section of Lab 2, we will introduce the syntax for using
the `geometry` column of our data to look at their spatial distribution.
This builds on the prior section where we learned the basics of
`ggplot()` and how we use different `geom` functions to map rows of our
data to different types of data visualizations.

## Plotting points

The key addition for using the `geometry` column of our data that
contains all the spatial information is the `geom` function `geom_sf()`.
Since we have a simple features `geometry` column that makes our data
frame a spatial simple features object, `ggplot()` knows that we want to
make a spatial data visualization when we use `geom_sf()`. We will
filter to listings from the first half of March to avoid overloading our
computers with this part of the exercise.

``` r
scraped <- scraped %>% 
  filter(listing_date >= "2020-03-01", listing_date < "2020-03-16")

#remind R what our CRS is
scraped <- st_set_crs(scraped, "EPSG:4326")

#plot the data
ggplot(scraped) +
  geom_sf()
```

![](lab_2_notebook_files/figure-gfm/unnamed-chunk-57-1.png)<!-- -->

When we make this plot, we see a set of points that are clustered
together with some going outward from the main cluster.

## Making a quick map

The one thing that would be *really* helpful for making this plot into a
proper map is to add a basemap. Basemaps give us pointers as to where
our points or polygons (e.g. a neighborhood unit) are located relative
to roads or other landmarks (e.g., Cornell) that we might be familiar
with. In other contexts where we might map a familiar set of spatial
data like the States of the U.S. or counties in a given State, basemaps
are not quite as essential.

We will use the `leaflet` library to accomplish this task. This library
allows us to create interactive maps that allow zooming in and out, as
well as easy incorporation of base maps. If you are reading this on
GitHub, the map is a static image, but if you downloaded the repository
and are running the code on your computer the map produced by the next
code chunk will be interactive.

The syntax of `leaflet` is a little different from ggplot, but for our
basic map is fairly straightforward. The biggest difference is that we
use the pipe operator `%>%` rather than the `+` operator as in `ggplot`.
We pass `leaflet()` our `sf` object of interest, then pipe that to
`addTiles()` to add the base map, then pipe that to `addMarkers()` to
add the points as markers on top of the base map.

``` r
leaflet(scraped) %>%
  addTiles() %>%
  addMarkers()
```

<!--html_preserve-->

<div id="htmlwidget-1d9acecd4202a2fdfb96" class="leaflet html-widget" style="width:672px;height:480px;">

</div>

<script type="application/json" data-for="htmlwidget-1d9acecd4202a2fdfb96">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addTiles","args":["//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",null,null,{"minZoom":0,"maxZoom":18,"tileSize":256,"subdomains":"abc","errorTileUrl":"","tms":false,"noWrap":false,"zoomOffset":0,"zoomReverse":false,"opacity":1,"zIndex":1,"detectRetina":false,"attribution":"&copy; <a href=\"http://openstreetmap.org\">OpenStreetMap<\/a> contributors, <a href=\"http://creativecommons.org/licenses/by-sa/2.0/\">CC-BY-SA<\/a>"}]},{"method":"addMarkers","args":[[42.43505,42.5050600000001,42.453422,42.453062,42.4565300000001,42.48174,42.419997,42.38808,42.38808,42.38808,42.427672,42.406922,42.592915,42.440646,42.436588,42.435802,42.435802,42.436588,42.471476,42.436743,42.431354,42.454731,42.4707570000001,42.509547,42.452753,42.511393,42.449969,42.441513,42.439834,42.405363,42.364545,42.437716,42.4418590000001,42.4418590000001,42.444962,42.442042,42.4418590000001,42.4418590000001,42.440557,42.438102,42.338554,42.470123,42.470866,42.452753,42.439462,42.445519,42.43898,42.449818,42.419991,42.467246,42.453415,42.598732,42.389845,42.445042,42.38808,42.460082,42.432056,42.419997,42.377482,42.40894,42.409198,42.409198,42.476827,42.409198,42.409198,42.409198,42.409871,42.406922,42.409871,42.476827,42.426357,42.426357,42.431038,42.445714,42.427758,42.540222,42.426621,42.450724,42.38808,42.470123,42.470866,42.453422,42.486153,42.17695,42.594796,42.437716,42.445534,42.438102,42.479931,42.445534,42.445534,42.440557,42.445534,42.445972,42.445534,42.445534,42.486091,42.486091,42.486091,42.486091,42.476827,42.476827,42.476827,42.476827,42.472812,42.511393,42.453062,42.510231,42.511393,42.1070610000001,42.513745,42.447221,42.481332,42.476827,42.1070610000001,42.481332,42.481332,42.481332,42.438913,42.438913,42.440963,42.438864,42.438895,42.430894,42.425504,42.451559,42.446272,42.440662,42.43076,42.430941,42.445042,42.434342,42.434502,42.435822,42.434342,42.40894,42.4379050000001,42.435822,42.434502,42.435822,42.445042,42.436988,42.436988,42.440963,42.434708,42.444453,42.419997,42.377482,42.409198,42.409198,42.409198,42.409198,42.431038,42.409198,42.409871,42.406922,42.409871,42.426357,42.426357,42.445714,42.427758,42.540222,42.426621,42.450724,42.449818,42.419991,42.430792,42.4349,42.454793,42.460041,42.419991,42.430792,42.4349,42.454793,42.453415,42.453415,42.47927,42.438512,42.486091,42.4418590000001,42.540222,42.476827,42.478594,42.48108,42.4565300000001,42.486091,42.486091,42.441167,42.5589630000001,42.460082,42.479931,42.452092,42.445073,42.450272,42.439497,42.44567,42.4565300000001,42.434708,42.476827,42.436867,42.440977,42.480496,42.38808,42.38808,42.476827,42.4425440000001,42.543088,42.439591,42.439143,42.441092,42.441092,42.476827,42.293834,42.476827,42.476827,42.479931,42.479931,42.470123,42.338554,42.470866,42.437713,42.481332,42.2271179999999,42.511287,42.481332,42.476827,42.447221,42.419997,42.441096,42.441096,42.436038,42.387766,42.428584,42.481332,42.438967,42.476827,42.38808,42.38808,42.38808,42.481332,42.407941,42.445006,42.435865,42.47854,42.47854,42.481332,42.430894,42.439596,42.438895,42.486091,42.438864,42.439776,42.486091,42.451559,42.439776,42.440963,42.451719,42.428486,42.1070610000001,42.440963,42.458715,42.434151,42.438512,42.472162,42.431787,42.439497,42.44567,42.4565300000001,42.479931,42.436867,42.440977,42.480496,42.38808,42.38808,42.476827,42.4425440000001,42.543088,42.439591,42.439591,42.439143,42.441092,42.441092,42.293834,42.476827,42.476827,42.479931,42.479931,42.470123,42.338554,42.470866,42.437713,42.481332,42.2271179999999,42.511287,42.481332,42.476827,42.447221,42.419997,42.441096,42.441096,42.436038,42.387766,42.428584,42.481332,42.438967,42.476827,42.38808,42.38808,42.38808,42.481332,42.407941,42.445006,42.476827,42.476827,42.435865,42.47854,42.47854,42.481332,42.430894,42.439596,42.438895,42.440187,42.5589630000001,42.44,42.419991,42.460041,42.46013,42.460041,42.5589630000001,42.44,42.419991,42.460041,42.46013,42.460041,42.453415,42.453415,42.442099,42.434502,42.441434,42.441694,42.438102,42.479931,42.444564,42.43076,42.436743,42.460041,42.47854,42.417597,42.472812,42.511393,42.453062,42.510231,42.511393,42.486091,42.486091,42.436306,42.486091,42.4565300000001,42.440627,42.437882,42.338554,42.440646,42.470123,42.476827,42.437638,42.536827,42.38808,42.38808,42.38808,42.486091,42.389845,42.381711,42.486091,42.539552,42.52466,42.436306,42.486091,42.476827,42.440737,42.440737,42.440737,42.440737,42.441172,42.441172,42.436483,42.419997,42.453422,42.476827,42.476827,42.450843,42.434339,42.486091,42.444468,42.434339,42.43898,42.439776,42.439776,42.44826,42.44178,42.435865,42.435865,42.435692,42.435865,42.479931,42.481332,42.486153,42.476827,42.476827,42.487112,42.545021,42.435041,42.445162,42.438253,42.403193,42.486091,42.440727,42.435041,42.476827,42.441434,42.441447,42.438087,42.440504,42.434886,42.434886,42.476827,42.476827,42.4410420000001,42.441117,42.441052,42.441117,42.486091,42.441052,42.441052,42.441052,42.479931,42.481332,42.481332,42.436306,42.486091,42.4416320000001,42.4416320000001,42.47854,42.476827,42.453062,42.47854,42.38808,42.38808,42.38808,42.403193,42.486091,42.389845,42.381711,42.486091,42.486091,42.539552,42.52466,42.436306,42.486091,42.476827,42.440737,42.440737,42.440737,42.440737,42.440727,42.441172,42.441172,42.436483,42.419997,42.453422,42.476827,42.476827,42.450843,42.434339,42.486091,42.476827,42.444468,42.434339,42.43898,42.439776,42.439776,42.44826,42.44178,42.476827,42.487112,42.435865,42.435865,42.435865,42.479931,42.481332,42.486153,42.486153,42.545021,42.435692,42.435041,42.445162,42.438253,42.435041,42.441434,42.46013,42.441447,42.438087,42.440504,42.434886,42.434886,42.476827,42.476827,42.419991,42.441117,42.441052,42.441117,42.441052,42.460041,42.453415,42.441052,42.441052,42.479931,42.481332,42.481332,42.486091,42.4416320000001,42.424344,42.4565300000001,42.447362,42.466073,42.444962,42.481332,42.481332,42.474089,42.46013,42.419991,42.460041,42.474089,42.434502,42.441872,42.435822,42.456901,42.468398,42.486091,42.481332,42.481332,42.478594,42.442422,42.476827,42.4295470000001,42.486091,42.486091,42.486091,42.486091,42.486091,42.486091,42.486091,42.46013,42.478594,42.435419,42.445042,42.443281,42.486091,42.43076,42.434342,42.472812,42.460082,42.450272,42.443707,42.4565300000001,42.38808,42.445534,42.445972,42.513745,42.445534,42.445534,42.445073,42.486091,42.486091,42.486091,42.486091,42.486091,42.486091,42.437716,42.438102,42.440557,42.44567,42.426357,42.426357,42.409871,42.406922,42.409198,42.476827,42.409198,42.409871,42.409198,42.409198,42.409198,42.476827,42.40894,42.4295470000001,42.4295470000001,42.4295470000001,42.4295470000001,42.442099,42.476827,42.486091,42.486091,42.476827,42.476827,42.338554,42.4254950000001,42.470123,42.441607,42.441577,42.441911,42.441911,42.442439,42.441694,42.4415720000001,42.38808,42.38808,42.457112,42.430894,42.446817,42.452092,42.438895,42.438864,42.486091,42.486091,42.486091,42.445006,42.440963,42.479317,42.453422,42.419997,42.440963,42.479931,42.38808,42.445534,42.445534,42.445972,42.445534,42.476827,42.445534,42.445073,42.486091,42.486091,42.486091,42.486091,42.486091,42.486091,42.437716,42.438102,42.440557,42.44567,42.513745,42.426357,42.426357,42.409871,42.406922,42.409198,42.4565300000001,42.409198,42.409871,42.409198,42.409198,42.409198,42.476827,42.40894,42.4295470000001,42.4295470000001,42.4295470000001,42.4295470000001,42.4295470000001,42.442099,42.486091,42.486091,42.476827,42.476827,42.338554,42.4254950000001,42.470123,42.441607,42.441577,42.441911,42.441911,42.442439,42.441694,42.4415720000001,42.476827,42.38808,42.38808,42.457112,42.430894,42.453422,42.446817,42.450272,42.452092,42.438895,42.438864,42.419997,42.486091,42.486091,42.486091,42.445006,42.440963,42.479317,42.440963,42.476827,42.441694,42.4415720000001,42.476827,42.476827,42.476827,42.38808,42.38808,42.457112,42.430894,42.446817,42.450272,42.452092,42.438895,42.438864,42.486091,42.486091,42.38808,42.38808,42.445519,42.445519,42.445519,42.474089,42.436087,42.419991,42.449818,42.4295470000001,42.474089,42.436087,42.419991,42.449818,42.474089,42.43305,42.43305,42.419991,42.47927,42.510231,42.453062,42.453422,42.427214,42.419997,42.511393,42.472812,42.511393,42.437596,42.453422,42.445042,42.434342,42.446564,42.439462,42.457112,42.438102,42.441694,42.440649,42.453422,42.419997,42.449818,42.439317,42.38808,42.38808,42.38808,42.440652,42.441592,42.440396,42.409198,42.476827,42.476827,42.476827,42.449818,42.419991,42.47854,42.453415,42.453415,42.453415,42.419997,42.482214,42.419997,42.419997,42.439071,42.43909,42.439042,42.429613,42.486091,42.445073,42.445002,42.486091,42.439591,42.439591,42.4416320000001,42.4416320000001,42.470123,42.470866,42.419997,42.419997,42.435822,42.434342,42.446272,42.434502,42.451559,42.419997,42.445042,42.435822,42.434342,42.434342,42.434502,42.451559,42.425504,42.436988,42.43076,42.419997,42.439071,42.43909,42.439042,42.429613,42.486091,42.445073,42.486091,42.439591,42.439591,42.4416320000001,42.439071,42.4416320000001,42.470123,42.470866,42.419997,42.419997,42.435822,42.434342,42.435822,42.435865,42.419997,42.439071,42.43909,42.439042,42.429613,42.47854,42.440449,42.419997,42.439071,42.43909,42.439042,42.429613,42.440449,42.43909,42.439042,42.436262,42.419997,42.445534,42.445042,42.440662,42.451559,42.435822,42.436988,42.435822,42.434342,42.4565300000001,42.54564,42.381924,42.445042,42.440662,42.434502,42.486091,42.486091,42.338554,42.435022,42.435022,42.38808,42.38808,42.470123,42.476827,42.440669,42.440669,42.444962,42.453422,42.486091,42.368043,42.442692,42.394459,42.476827,42.442593,42.443321,42.442593,42.481332,42.481332,42.425651,42.486091,42.486091,42.419991,42.486091,42.486091,42.439532,42.437496,42.478751,42.437496,42.4426369999999,42.47854,42.486091,42.476827,42.441208,42.438029,42.452763,42.44032,42.440361,42.435924,42.435924,42.4358350000001,42.4358350000001,42.437504,42.445519,42.445519,42.445519,42.419991,42.419991,42.419991,42.419991,42.419991,42.419991,42.419991,42.419991,42.486091,42.474089,42.454093,42.454093,42.454093,42.453415,42.458712,42.458712,42.481332,42.474089,42.453415,42.453415,42.453415,42.453415,42.47927,42.52466,42.438637,42.451559,42.470123,42.447362,42.486153,42.439596,42.440671,42.460082,42.4349,42.460041,42.460041,42.47927,42.441694,42.338554,42.434502,42.430894,42.440662,42.434886,42.435822,42.441052,42.439834,42.38808,42.445145,42.48174,42.447221,42.451853,42.474089,42.394,42.438102,42.440557,42.476827,42.438102,42.440557,42.4593050000001,42.419997,42.419997,42.442491,42.486091,42.486091,42.471476,42.444962,42.419997,42.428066,42.345569,42.347201,42.437882,42.448587,42.470866,42.470123,42.425651,42.436588,42.435802,42.435802,42.435802,42.439143,42.4593050000001,42.54564,42.429123,42.437716,42.438102,42.440557,42.419997,42.38808,42.486091,42.486091,42.486091,42.486091,42.345044,42.453422,42.490474,42.444453,42.424084,42.438102,42.440557,42.4593050000001,42.442491,42.486091,42.486091,42.471476,42.439462,42.438102,42.440557,42.4593050000001,42.419997,42.442491,42.486091,42.486091,42.470866,42.471476,42.444962,42.598672,42.438102,42.440557,42.4593050000001,42.438102,42.440557,42.4593050000001,42.419997,42.442491,42.486091,42.486091,42.486091,42.471476,42.439071,42.43909,42.439042,42.4565300000001,42.429613,42.445073,42.486091,42.439591,42.4565300000001,42.4416320000001,42.4416320000001,42.470123,42.434502,42.419997,42.435822,42.434342,42.446272,42.434502,42.451559,42.434502,42.445042,42.435822,42.434342,42.434342,42.434502,42.451559,42.425504,42.436988,42.43076,42.445042,42.434708,42.440662,42.445042,42.434342,42.43784,42.468697,42.4683510000001,42.52466,42.419991,42.539552,42.486091,42.38808,42.38808,42.436761,42.481332,42.481332,42.476827,42.476827,42.476827,42.476827,42.36444,42.430612,42.439462,42.434886,42.486091,42.486091,42.440646,42.476827,42.476827,42.430931,42.444931,42.434886,42.440504,42.438087,42.441447,42.441434,42.435041,42.434832,42.434832,42.439071,42.438253,42.435041,42.476827,42.476827,42.434126,42.434126,42.439042,42.4426729999999,42.445519,42.445519,42.445519,42.481332,42.419991,42.419991,42.481332,42.419991,42.419991,42.419991,42.419991,42.460041,42.46013,42.460082,42.460041,42.453415,42.453415,42.453415,42.453415,42.453415,42.453415,42.413865,42.413865,42.60353,42.486091,42.430941,42.598732,42.38808,42.409198,42.486091,42.486091,42.291588,42.43466,42.428906,42.441172,42.474984,42.441172,42.436483,42.345569,42.345569,42.345569,42.435988,42.438855,42.480022,42.446817,42.435822,42.478594,42.482018,42.345569,42.38808,42.436588,42.436483,42.345569,42.345569,42.474984,42.435988,42.438855,42.486091,42.440963,42.436988,42.46013,42.594898,42.453422,42.470866,42.470123,42.453415,42.425651,42.486091,42.486091,42.486091,42.486091,42.345044,42.439143,42.419997,42.438102,42.440557,42.4593050000001,42.442491,42.486091,42.4565300000001,42.419991,42.471476,42.444962,42.345569,42.347201,42.437882,42.448587,42.436588,42.435802,42.435802,42.435802,42.4593050000001,42.54564,42.429123,42.437716,42.438102,42.440557,42.443768,42.443768,42.435022,42.434032,42.38808,42.445519,42.481332,42.413865,42.60353,42.38808,42.440963,42.47854,42.430941,42.437716,42.446272,42.441092,42.452027,42.479931,42.445519,42.439776,42.439776,42.44826,42.476827,42.440646,42.445534,42.445534,42.445534,42.419991,42.5050600000001,42.431354,42.454731,42.38808,42.38808,42.38808,42.4565300000001,42.441101,42.479821,42.470123,42.470866,42.445073,42.409198,42.406922,42.409198,42.406922,42.40894,42.409198,42.409198,42.406922,42.436867,42.610552,42.486091,42.486091,42.486091,42.419997,42.440977,42.481332,42.481332,42.447472,42.476827,42.476827,42.481332,42.440857,42.476827,42.476827,42.441592,42.478411,42.435537,42.479931,42.437716,42.438102,42.476827,42.476827,42.476827,42.439776,42.1070610000001,42.1070610000001,42.1070610000001,42.481332,42.436892,42.439564,42.476827,42.445002,42.480013,42.38808,42.38808,42.43898,42.445006,42.44826,42.44178,42.435865,42.486091,42.486091,42.486091,42.490474,42.444453,42.424084,42.409198,42.445519,42.445519,42.481332,42.460041,42.540196,42.460041,42.460041,42.46013,42.46013,42.453415,42.440669,42.460041,42.436988,42.4295470000001,42.44498,42.511422,42.474984,42.481332,42.481332,42.419997,42.434342,42.434708,42.440662,42.434342,42.440847,42.4565300000001,42.434502,42.435822,42.43076,42.435822,42.4565300000001,42.429742,42.436988,42.4410420000001,42.4379050000001,42.445042,42.436988,42.451559,42.481332,42.451559,42.425504,42.446272,42.429613,42.486091,42.441052,42.441117,42.441092,42.441092,42.430183,42.481332,42.481332,42.435537,42.436483,42.38808,42.609854,42.38808,42.441172,42.441172,42.440727,42.486091,42.486091,42.481332,42.435041,42.438253,42.434832,42.434832,42.435041,42.441434,42.441447,42.440557,42.545021,42.476827,42.476827,42.476827,42.481332,42.476827,42.453422,42.4295470000001,42.437716,42.4295470000001,42.438102,42.4565300000001,42.440847,42.4565300000001,42.481332,42.435865,42.419991,42.486091,42.486091,42.486091,42.440646,42.445534,42.445534,42.481332,42.445972,42.445534,42.445534,42.445534,42.38808,42.436867,42.38808,42.38808,42.4565300000001,42.441101,42.479821,42.470123,42.476827,42.470866,42.445073,42.409198,42.406922,42.419997,42.409198,42.406922,42.40894,42.409198,42.409198,42.406922,42.486091,42.486091,42.486091,42.419997,42.440977,42.481332,42.481332,42.610552,42.447472,42.476827,42.476827,42.481332,42.486091,42.38808,42.440857,42.476827,42.476827,42.441592,42.478411,42.435537,42.479931,42.437716,42.438102,42.476827,42.476827,42.419997,42.476827,42.1070610000001,42.1070610000001,42.1070610000001,42.436892,42.439564,42.476827,42.445002,42.480013,42.38808,42.478594,42.38808,42.43898,42.4410420000001,42.445519,42.445519,42.460041,42.4295470000001,42.460041,42.456196,42.419991,42.419991,42.460041,42.540196,42.419991,42.460041,42.460041,42.46013,42.46013,42.453415,42.453415,42.541873,42.437351,42.486091,42.434342,42.438895,42.451559,42.449969,42.4295470000001,42.48108,42.440649,42.434708,42.434708,42.39307,42.598732,42.436262,42.486091,42.364545,42.434342,42.450077,42.454093,42.460041,42.47927,42.441694,42.453415,42.47927,42.47927,42.476827,42.435822,42.441694,42.4416570000001,42.441117,42.441117,42.441117,42.441117,42.486091,42.442292,42.603792,42.476827,42.598732,42.598672,42.598732,42.439462,42.598732,42.5987550000001,42.439462,42.439462,42.441161,42.442099,42.598732,42.440449,42.440449,42.440449,42.440449,42.4411460000001,42.440847,42.440847,42.440449,42.444453,42.476827,42.481332,42.456585,42.435865,42.435865,42.435865,42.419997,42.481332,42.381924,42.425504,42.451559,42.451559,42.481332,42.436988,42.436988,42.476827,42.445042,42.476827,42.476827,42.446272,42.4416320000001,42.4416320000001,42.440662,42.440662,42.43076,42.434342,42.430941,42.594401,42.445042,42.434342,42.435802,42.435802,42.435802,42.436588,42.435822,42.435822,42.434502,42.434502,42.603602,42.603602,42.435893,42.434886,42.434886,42.425651,42.470123,42.486091,42.486091,42.486091,42.470866,42.438907,42.438907,42.4565300000001,42.434243,42.4593050000001,42.4565300000001,42.437882,42.440724,42.4416320000001,42.440724,42.516189,42.439143,42.486091,42.486091,42.486091,42.486091,42.437716,42.438102,42.440557,42.696194,42.476827,42.43909,42.445073,42.419991,42.444962,42.452927,42.441096,42.474489,42.4413470000001,42.473547,42.441096,42.4413470000001,42.441096,42.422555,42.441557,42.438512,42.438855,42.444341,42.435988,42.428486,42.438733,42.431787,42.440187,42.4413470000001,42.441096,42.403193,42.472162,42.438512,42.472162,42.434151,42.467714,42.451719,42.487687,42.451719,42.436038,42.452474,42.458715,42.514947,42.4413470000001,42.536337,42.476827,42.486091,42.487112,42.476827,42.433835,42.432722,42.440504,42.440504,42.441117,42.441117,42.441117,42.441117,42.486091,42.441694,42.4416570000001,42.445042,42.441117,42.441117,42.445519,42.441167,42.460041,42.419991,42.458712,42.458712,42.454093,42.454093,42.454093,42.603602,42.478594,42.478594,42.460041,42.47927,42.603602,42.478594,42.438895,42.434342,42.456585,42.486091,42.435802,42.452232,42.460041,42.446564,42.441172,42.446817,42.434342,42.479931,42.486091,42.1070610000001,42.486091,42.46013,42.460041,42.460041,42.460041,42.419997,42.476827,42.441694,42.442292,42.603792,42.598732,42.598732,42.598672,42.598732,42.439462,42.598732,42.5987550000001,42.439462,42.439462,42.442099,42.598732,42.436892,42.441117,42.419997,42.476827,42.1070610000001,42.1070610000001,42.1070610000001,42.481332,42.476827,42.439564,42.476827,42.445002,42.480013,42.38808,42.38808,42.43898,42.440669,42.440449,42.434502,42.476827,42.486091,42.486091,42.486091,42.486091,42.345044,42.439143,42.419997,42.453422,42.419997,42.490474,42.444453,42.424084,42.38808,42.38808,42.438253,42.38808,42.4565300000001,42.441101,42.479821,42.470123,42.470866,42.445073,42.409198,42.406922,42.409198,42.406922,42.40894,42.409198,42.409198,42.406922,42.436867,42.610552,42.486091,42.486091,42.486091,42.419997,42.440977,42.481332,42.481332,42.447472,42.476827,42.476827,42.481332,42.440857,42.476827,42.476827,42.441592,42.445519,42.445519,42.481332,42.481332,42.419991,42.460041,42.460041,42.46013,42.46013,42.419991,42.419991,42.419991,42.460041,42.453415,42.453415,42.509547,42.453062,42.440449,42.479931,42.419997,42.486091,42.511393,42.4707570000001,42.486091,42.339064,42.476827,42.476827,42.486091,42.486091,42.486091,42.440724,42.440724,42.440737,42.440681,42.476827,42.44,42.419991,42.453422,42.481332,42.478411,42.435537,42.479931,42.437716,42.438102,42.476827,42.476827,42.419997,42.476827,42.1070610000001,42.1070610000001,42.1070610000001,42.436892,42.476827,42.445002,42.480013,42.38808,42.38808,42.43898,42.440669,42.598732,42.435822,42.476827,42.476827,42.419997,42.490474,42.444453,42.424084,42.38808,42.38808,42.476827,42.38808,42.4565300000001,42.441101,42.479821,42.470123,42.470866,42.445073,42.409198,42.406922,42.409198,42.406922,42.419997,42.40894,42.409198,42.409198,42.406922,42.436867,42.610552,42.486091,42.486091,42.486091,42.419997,42.440977,42.481332,42.481332,42.441117,42.441117,42.445519,42.481332,42.481332,42.540196,42.460041,42.460041,42.46013,42.46013,42.46013,42.419991,42.419991,42.419991,42.453415,42.453415,42.476827,42.476827,42.434708,42.440649,42.434708,42.435802,42.43466,42.439317,42.439462,42.456303,42.482018,42.449623,42.47854,42.47854,42.479931,42.435802,42.43466,42.48108,42.440649,42.434708,42.434708,42.39307,42.598732,42.595495,42.440361,42.422555,42.486153,42.438637,42.445519,42.460082,42.474089,42.460041,42.454093,42.460041,42.47927,42.476827,42.419997,42.419997,42.419991,42.476827,42.447472,42.476827,42.476827,42.481332,42.440857,42.476827,42.441592,42.478411,42.435537,42.479931,42.437716,42.438102,42.476827,42.476827,42.1070610000001,42.1070610000001,42.1070610000001,42.481332,42.436892,42.476827,42.345044,42.445002,42.480013,42.38808,42.38808,42.43898,42.590186,42.448367,42.52466,42.441117,42.426357,42.439143,42.442292,42.609854,42.440857,42.486091,42.486091,42.486091,42.453422,42.490474,42.444453,42.424084,42.38808,42.38808,42.38808,42.441101,42.479821,42.442513,42.441117,42.516189,42.409198,42.441052,42.602844,42.433835,42.610552,42.445519,42.445519,42.481332,42.460041,42.540196,42.419991,42.46013,42.460041,42.460041,42.46013,42.46013,42.419991,42.456585,42.481332,42.1070610000001,42.338554,42.509547,42.405363,42.439834,42.48174,42.447221,42.419997,42.486091,42.486091,42.486091,42.486091,42.551971,42.438102,42.38808,42.38808,42.437567,42.478594,42.481332,42.476827,42.442292,42.481332,42.478594,42.481332,42.481332,42.419991,42.474089,42.381602,42.417597,42.478594,42.460082,42.438102,42.419997,42.470123,42.470866,42.445073,42.409198,42.406922,42.409198,42.406922,42.40894,42.409198,42.409198,42.406922,42.436867,42.486091,42.486091,42.486091,42.440977,42.445534,42.441117,42.445714,42.419991,42.453415,42.486091,42.486091,42.486091,42.511393,42.4707570000001,42.486091,42.339064,42.476827,42.4379050000001,42.434126],[-76.49532,-76.47158,-76.49914,-76.444611,-76.486907,-76.33975,-76.482953,-76.361697,-76.361697,-76.361697,-76.381678,-76.497885,-76.182479,-76.480398,-76.490976,-76.48929,-76.48929,-76.490976,-76.484705,-76.489998,-76.496109,-76.490671,-76.448793,-76.471375,-76.445413,-76.471978,-76.503386,-76.49219,-76.477629,-76.42943,-76.353668,-76.492938,-76.489859,-76.489859,-76.497611,-76.490219,-76.489859,-76.489859,-76.495006,-76.493448,-76.394997,-76.464609,-76.447619,-76.445413,-76.485114,-76.482668,-76.479887,-76.494979,-76.482941,-76.473526,-76.49958,-76.180314,-76.471352,-76.494891,-76.361697,-76.528654,-76.490347,-76.482953,-76.284331,-76.503039,-76.502955,-76.502955,-76.466978,-76.502955,-76.502955,-76.502955,-76.502936,-76.497885,-76.502936,-76.466978,-76.499421,-76.499421,-76.495148,-76.493308,-76.486156,-76.493049,-76.486399,-76.497429,-76.361697,-76.464609,-76.447619,-76.49914,-76.481804,-76.816907,-76.555292,-76.492938,-76.50152,-76.493448,-76.472805,-76.50152,-76.50152,-76.495006,-76.50152,-76.500537,-76.50152,-76.50152,-76.467471,-76.467471,-76.467471,-76.467471,-76.466978,-76.466978,-76.466978,-76.466978,-76.452571,-76.471978,-76.444611,-76.471884,-76.471978,-76.224669,-76.347124,-76.499408,-76.474209,-76.466978,-76.224669,-76.474209,-76.474209,-76.474209,-76.477589,-76.477589,-76.483531,-76.488886,-76.488936,-76.503018,-76.499863,-76.496329,-76.498195,-76.489001,-76.502285,-76.502115,-76.494891,-76.494534,-76.494544,-76.493401,-76.494534,-76.503039,-76.488488,-76.493401,-76.494544,-76.493401,-76.494961,-76.500639,-76.500639,-76.483531,-76.494559,-76.504177,-76.482953,-76.284331,-76.502955,-76.502955,-76.502955,-76.502955,-76.495148,-76.502955,-76.502936,-76.497885,-76.502936,-76.499421,-76.499421,-76.493308,-76.486156,-76.493049,-76.486399,-76.497429,-76.494979,-76.482941,-76.429542,-76.498785,-76.438912,-76.528605,-76.482941,-76.429542,-76.498785,-76.438912,-76.49958,-76.49958,-76.48702,-76.483945,-76.467471,-76.489859,-76.493049,-76.466978,-76.482248,-76.478497,-76.486907,-76.467471,-76.467471,-76.478222,-76.552323,-76.528654,-76.472805,-76.4966,-76.494679,-76.496197,-76.501302,-76.504547,-76.486907,-76.494559,-76.466978,-76.499953,-76.504048,-76.508912,-76.361697,-76.361697,-76.466978,-76.500887,-76.258029,-76.485959,-76.483178,-76.506719,-76.506719,-76.466978,-76.51969,-76.466978,-76.466978,-76.472805,-76.472805,-76.464609,-76.394997,-76.447619,-76.492819,-76.474209,-76.338018,-76.467989,-76.474209,-76.466978,-76.499408,-76.482953,-76.481322,-76.481322,-76.496788,-76.472495,-76.528325,-76.474209,-76.503949,-76.466978,-76.361697,-76.361697,-76.361697,-76.474209,-76.503031,-76.496975,-76.493142,-76.478286,-76.478286,-76.474209,-76.503018,-76.498582,-76.488936,-76.467471,-76.488886,-76.494221,-76.467471,-76.496329,-76.494221,-76.483531,-76.496254,-76.504601,-76.224669,-76.483531,-76.489273,-76.498754,-76.483945,-76.447781,-76.470583,-76.501302,-76.504547,-76.486907,-76.472805,-76.499953,-76.504048,-76.508912,-76.361697,-76.361697,-76.466978,-76.500887,-76.258029,-76.485959,-76.485959,-76.483178,-76.506719,-76.506719,-76.51969,-76.466978,-76.466978,-76.472805,-76.472805,-76.464609,-76.394997,-76.447619,-76.492819,-76.474209,-76.338018,-76.467989,-76.474209,-76.466978,-76.499408,-76.482953,-76.481322,-76.481322,-76.496788,-76.472495,-76.528325,-76.474209,-76.503949,-76.466978,-76.361697,-76.361697,-76.361697,-76.474209,-76.503031,-76.496975,-76.466978,-76.466978,-76.493142,-76.478286,-76.478286,-76.474209,-76.503018,-76.498582,-76.488936,-76.505933,-76.552323,-76.511472,-76.482941,-76.528605,-76.528581,-76.528605,-76.552323,-76.511472,-76.482941,-76.528605,-76.528581,-76.528605,-76.49958,-76.49958,-76.483129,-76.494544,-76.495485,-76.486647,-76.493448,-76.472805,-76.50102,-76.502285,-76.489998,-76.528605,-76.478286,-76.412422,-76.452571,-76.471978,-76.444611,-76.471884,-76.471978,-76.467471,-76.467471,-76.492215,-76.467471,-76.486907,-76.492372,-76.479462,-76.394997,-76.480398,-76.464609,-76.466978,-76.498958,-76.498309,-76.361697,-76.361697,-76.361697,-76.467471,-76.471352,-76.553607,-76.467471,-76.458631,-76.451632,-76.492215,-76.467471,-76.466978,-76.488192,-76.488192,-76.488192,-76.488192,-76.47535,-76.47535,-76.492195,-76.482953,-76.49914,-76.466978,-76.466978,-76.634081,-76.499088,-76.467471,-76.494698,-76.499088,-76.479887,-76.494221,-76.494221,-76.49032,-76.491789,-76.493142,-76.493142,-76.494698,-76.493142,-76.472805,-76.474209,-76.481804,-76.466978,-76.466978,-76.467484,-76.657184,-76.492198,-76.497055,-76.49392,-76.4777,-76.467471,-76.488413,-76.492198,-76.466978,-76.495485,-76.494942,-76.494816,-76.489705,-76.495283,-76.495283,-76.466978,-76.466978,-76.481442,-76.480453,-76.481021,-76.480453,-76.467471,-76.481021,-76.481021,-76.481021,-76.472805,-76.474209,-76.474209,-76.492215,-76.467471,-76.487447,-76.487447,-76.478286,-76.466978,-76.444611,-76.478286,-76.361697,-76.361697,-76.361697,-76.4777,-76.467471,-76.471352,-76.553607,-76.467471,-76.467471,-76.458631,-76.451632,-76.492215,-76.467471,-76.466978,-76.488192,-76.488192,-76.488192,-76.488192,-76.488413,-76.47535,-76.47535,-76.492195,-76.482953,-76.49914,-76.466978,-76.466978,-76.634081,-76.499088,-76.467471,-76.466978,-76.494698,-76.499088,-76.479887,-76.494221,-76.494221,-76.49032,-76.491789,-76.466978,-76.467484,-76.493142,-76.493142,-76.493142,-76.472805,-76.474209,-76.481804,-76.481804,-76.657184,-76.494698,-76.492198,-76.497055,-76.49392,-76.492198,-76.495485,-76.528581,-76.494942,-76.494816,-76.489705,-76.495283,-76.495283,-76.466978,-76.466978,-76.482941,-76.480453,-76.481021,-76.480453,-76.481021,-76.528605,-76.49958,-76.481021,-76.481021,-76.472805,-76.474209,-76.474209,-76.467471,-76.487447,-76.464379,-76.486907,-76.571219,-76.40974,-76.497611,-76.474209,-76.474209,-76.465467,-76.528581,-76.482941,-76.528605,-76.465467,-76.494544,-76.483121,-76.493401,-76.483749,-76.527514,-76.467471,-76.474209,-76.474209,-76.482248,-76.505942,-76.466978,-76.494003,-76.467471,-76.467471,-76.467471,-76.467471,-76.467471,-76.467471,-76.467471,-76.528581,-76.482248,-76.492304,-76.494891,-76.515687,-76.467471,-76.502285,-76.494534,-76.452571,-76.528654,-76.496197,-76.506878,-76.486907,-76.361697,-76.50152,-76.500537,-76.347124,-76.50152,-76.50152,-76.494679,-76.467471,-76.467471,-76.467471,-76.467471,-76.467471,-76.467471,-76.492938,-76.493448,-76.495006,-76.504547,-76.499421,-76.499421,-76.502936,-76.497885,-76.502955,-76.466978,-76.502955,-76.502936,-76.502955,-76.502955,-76.502955,-76.466978,-76.503039,-76.494003,-76.494003,-76.494003,-76.494003,-76.483129,-76.466978,-76.467471,-76.467471,-76.466978,-76.466978,-76.394997,-76.537947,-76.464609,-76.488932,-76.491162,-76.491405,-76.491405,-76.488769,-76.486647,-76.488401,-76.361697,-76.361697,-76.486258,-76.503018,-76.498309,-76.4966,-76.488936,-76.488886,-76.467471,-76.467471,-76.467471,-76.496975,-76.483531,-76.472808,-76.49914,-76.482953,-76.483531,-76.472805,-76.361697,-76.50152,-76.50152,-76.500537,-76.50152,-76.466978,-76.50152,-76.494679,-76.467471,-76.467471,-76.467471,-76.467471,-76.467471,-76.467471,-76.492938,-76.493448,-76.495006,-76.504547,-76.347124,-76.499421,-76.499421,-76.502936,-76.497885,-76.502955,-76.486907,-76.502955,-76.502936,-76.502955,-76.502955,-76.502955,-76.466978,-76.503039,-76.494003,-76.494003,-76.494003,-76.494003,-76.494003,-76.483129,-76.467471,-76.467471,-76.466978,-76.466978,-76.394997,-76.537947,-76.464609,-76.488932,-76.491162,-76.491405,-76.491405,-76.488769,-76.486647,-76.488401,-76.466978,-76.361697,-76.361697,-76.486258,-76.503018,-76.49914,-76.498309,-76.496197,-76.4966,-76.488936,-76.488886,-76.482953,-76.467471,-76.467471,-76.467471,-76.496975,-76.483531,-76.472808,-76.483531,-76.466978,-76.486647,-76.488401,-76.466978,-76.466978,-76.466978,-76.361697,-76.361697,-76.486258,-76.503018,-76.498309,-76.496197,-76.4966,-76.488936,-76.488886,-76.467471,-76.467471,-76.361697,-76.361697,-76.482668,-76.482668,-76.482668,-76.465467,-76.48574,-76.482941,-76.494979,-76.494003,-76.465467,-76.48574,-76.482941,-76.494979,-76.465467,-76.47101,-76.47101,-76.482941,-76.48702,-76.471884,-76.444611,-76.49914,-76.381565,-76.482953,-76.471978,-76.452571,-76.471978,-76.485231,-76.49914,-76.494891,-76.494534,-76.493188,-76.485114,-76.486258,-76.493448,-76.486647,-76.489572,-76.49914,-76.482953,-76.494979,-76.507892,-76.361697,-76.361697,-76.361697,-76.489241,-76.487681,-76.492148,-76.502955,-76.466978,-76.466978,-76.466978,-76.494979,-76.482941,-76.478286,-76.49958,-76.49958,-76.49958,-76.482953,-76.467249,-76.482953,-76.482953,-76.477565,-76.489218,-76.477565,-76.491658,-76.467471,-76.494679,-76.497079,-76.467471,-76.485959,-76.485959,-76.487447,-76.487447,-76.464609,-76.447619,-76.482953,-76.482953,-76.493401,-76.494534,-76.498195,-76.494544,-76.496329,-76.482953,-76.494961,-76.493401,-76.494534,-76.494534,-76.494544,-76.496329,-76.499863,-76.500639,-76.502285,-76.482953,-76.477565,-76.489218,-76.477565,-76.491658,-76.467471,-76.494679,-76.467471,-76.485959,-76.485959,-76.487447,-76.477565,-76.487447,-76.464609,-76.447619,-76.482953,-76.482953,-76.493401,-76.494534,-76.493401,-76.493142,-76.482953,-76.477565,-76.489218,-76.477565,-76.491658,-76.478286,-76.475249,-76.482953,-76.477565,-76.489218,-76.477565,-76.491658,-76.475249,-76.489218,-76.477565,-76.485654,-76.482953,-76.50152,-76.494891,-76.489001,-76.496329,-76.493401,-76.500639,-76.493401,-76.494534,-76.486907,-76.524516,-76.87419,-76.494961,-76.489001,-76.494544,-76.467471,-76.467471,-76.394997,-76.501464,-76.501464,-76.361697,-76.361697,-76.464609,-76.466978,-76.484209,-76.484209,-76.497611,-76.49914,-76.467471,-76.5561,-76.495381,-76.386659,-76.466978,-76.489844,-76.500905,-76.489844,-76.474209,-76.474209,-76.456595,-76.467471,-76.467471,-76.482941,-76.467471,-76.467471,-76.498812,-76.495463,-76.373525,-76.495463,-76.483653,-76.478286,-76.467471,-76.466978,-76.484228,-76.485037,-76.487928,-76.491034,-76.487365,-76.486069,-76.486069,-76.486084,-76.486084,-76.487927,-76.482668,-76.482668,-76.482668,-76.482941,-76.482941,-76.482941,-76.482941,-76.482941,-76.482941,-76.482941,-76.482941,-76.467471,-76.465467,-76.490928,-76.490928,-76.490928,-76.49958,-76.486488,-76.486488,-76.474209,-76.465467,-76.49958,-76.49958,-76.49958,-76.49958,-76.48702,-76.451632,-76.498008,-76.496329,-76.464609,-76.571219,-76.481804,-76.498582,-76.48975,-76.528654,-76.498785,-76.528605,-76.528605,-76.48702,-76.486647,-76.394997,-76.494544,-76.503018,-76.489001,-76.495283,-76.493401,-76.481021,-76.477629,-76.361697,-76.49817,-76.33975,-76.499408,-76.500958,-76.465467,-76.346907,-76.493448,-76.495006,-76.466978,-76.493448,-76.495006,-76.430371,-76.482953,-76.482953,-76.50145,-76.467471,-76.467471,-76.484705,-76.497611,-76.482953,-76.487193,-76.630977,-76.629679,-76.479462,-76.497359,-76.447619,-76.464609,-76.456595,-76.490976,-76.48929,-76.48929,-76.48929,-76.483178,-76.430371,-76.524516,-76.504002,-76.492938,-76.493448,-76.495006,-76.482953,-76.361697,-76.467471,-76.467471,-76.467471,-76.467471,-76.469755,-76.49914,-76.300975,-76.504177,-76.463955,-76.493448,-76.495006,-76.430371,-76.50145,-76.467471,-76.467471,-76.484705,-76.485114,-76.493448,-76.495006,-76.430371,-76.482953,-76.50145,-76.467471,-76.467471,-76.447619,-76.484705,-76.497611,-76.180305,-76.493448,-76.495006,-76.430371,-76.493448,-76.495006,-76.430371,-76.482953,-76.50145,-76.467471,-76.467471,-76.467471,-76.484705,-76.477565,-76.489218,-76.477565,-76.486907,-76.491658,-76.494679,-76.467471,-76.485959,-76.486907,-76.487447,-76.487447,-76.464609,-76.494544,-76.482953,-76.493401,-76.494534,-76.498195,-76.494544,-76.496329,-76.494544,-76.494961,-76.493401,-76.494534,-76.494534,-76.494544,-76.496329,-76.499863,-76.500639,-76.502285,-76.494961,-76.494559,-76.489001,-76.494891,-76.494534,-76.485035,-76.487994,-76.354004,-76.451632,-76.482941,-76.458631,-76.467471,-76.361697,-76.361697,-76.502557,-76.474209,-76.474209,-76.466978,-76.466978,-76.466978,-76.466978,-76.557466,-76.492488,-76.485114,-76.495283,-76.467471,-76.467471,-76.480398,-76.466978,-76.466978,-76.496355,-76.499271,-76.495283,-76.489705,-76.494816,-76.494942,-76.495485,-76.492198,-76.495341,-76.495341,-76.477565,-76.49392,-76.492198,-76.466978,-76.466978,-76.476997,-76.476997,-76.477565,-76.496977,-76.482668,-76.482668,-76.482668,-76.474209,-76.482941,-76.482941,-76.474209,-76.482941,-76.482941,-76.482941,-76.482941,-76.528605,-76.528581,-76.528654,-76.528605,-76.49958,-76.49958,-76.49958,-76.49958,-76.49958,-76.49958,-76.447366,-76.447366,-76.172,-76.467471,-76.502115,-76.180314,-76.361697,-76.502955,-76.467471,-76.467471,-76.687981,-76.494556,-76.496123,-76.47535,-76.554145,-76.47535,-76.492195,-76.630977,-76.630977,-76.630977,-76.496788,-76.488758,-76.371365,-76.498309,-76.493401,-76.482248,-76.484494,-76.630977,-76.361697,-76.490976,-76.492195,-76.630977,-76.630977,-76.554145,-76.496788,-76.488758,-76.467471,-76.483531,-76.500639,-76.528581,-76.182299,-76.49914,-76.447619,-76.464609,-76.49958,-76.456595,-76.467471,-76.467471,-76.467471,-76.467471,-76.469755,-76.483178,-76.482953,-76.493448,-76.495006,-76.430371,-76.50145,-76.467471,-76.486907,-76.482941,-76.484705,-76.497611,-76.630977,-76.629679,-76.479462,-76.497359,-76.490976,-76.48929,-76.48929,-76.48929,-76.430371,-76.524516,-76.504002,-76.492938,-76.493448,-76.495006,-76.495879,-76.495879,-76.501464,-76.502056,-76.361697,-76.482668,-76.474209,-76.447366,-76.172,-76.361697,-76.483531,-76.478286,-76.502115,-76.492938,-76.498195,-76.506719,-76.597982,-76.472805,-76.482668,-76.494221,-76.494221,-76.49032,-76.466978,-76.480398,-76.50152,-76.50152,-76.50152,-76.482941,-76.47158,-76.496109,-76.490671,-76.361697,-76.361697,-76.361697,-76.486907,-76.50625,-76.373564,-76.464609,-76.447619,-76.494679,-76.502955,-76.497885,-76.502955,-76.497885,-76.503039,-76.502955,-76.502955,-76.497885,-76.499953,-76.16198,-76.467471,-76.467471,-76.467471,-76.482953,-76.504048,-76.474209,-76.474209,-76.497215,-76.466978,-76.466978,-76.474209,-76.489798,-76.466978,-76.466978,-76.488638,-76.472023,-76.498242,-76.472805,-76.492938,-76.493448,-76.466978,-76.466978,-76.466978,-76.494221,-76.224669,-76.224669,-76.224669,-76.474209,-76.376512,-76.498987,-76.466978,-76.497079,-76.560848,-76.361697,-76.361697,-76.479887,-76.496975,-76.49032,-76.491789,-76.493142,-76.467471,-76.467471,-76.467471,-76.300975,-76.504177,-76.463955,-76.502955,-76.482668,-76.482668,-76.474209,-76.528605,-76.655993,-76.528605,-76.528605,-76.528581,-76.528581,-76.49958,-76.484209,-76.528605,-76.500639,-76.494003,-76.498119,-76.471179,-76.554145,-76.474209,-76.474209,-76.482953,-76.494534,-76.494559,-76.489001,-76.494534,-76.500869,-76.486907,-76.494544,-76.493401,-76.502285,-76.493401,-76.486907,-76.49175,-76.500639,-76.481442,-76.488488,-76.494961,-76.500639,-76.496329,-76.474209,-76.496329,-76.499863,-76.498195,-76.491658,-76.467471,-76.481021,-76.480453,-76.506719,-76.506719,-76.460704,-76.474209,-76.474209,-76.498242,-76.492195,-76.361697,-76.192333,-76.361697,-76.47535,-76.47535,-76.488413,-76.467471,-76.467471,-76.474209,-76.492198,-76.49392,-76.495341,-76.495341,-76.492198,-76.495485,-76.494942,-76.495006,-76.657184,-76.466978,-76.466978,-76.466978,-76.474209,-76.466978,-76.49914,-76.494003,-76.492938,-76.494003,-76.493448,-76.486907,-76.500869,-76.486907,-76.474209,-76.493142,-76.482941,-76.467471,-76.467471,-76.467471,-76.480398,-76.50152,-76.50152,-76.474209,-76.500537,-76.50152,-76.50152,-76.50152,-76.361697,-76.499953,-76.361697,-76.361697,-76.486907,-76.50625,-76.373564,-76.464609,-76.466978,-76.447619,-76.494679,-76.502955,-76.497885,-76.482953,-76.502955,-76.497885,-76.503039,-76.502955,-76.502955,-76.497885,-76.467471,-76.467471,-76.467471,-76.482953,-76.504048,-76.474209,-76.474209,-76.16198,-76.497215,-76.466978,-76.466978,-76.474209,-76.467471,-76.361697,-76.489798,-76.466978,-76.466978,-76.488638,-76.472023,-76.498242,-76.472805,-76.492938,-76.493448,-76.466978,-76.466978,-76.482953,-76.466978,-76.224669,-76.224669,-76.224669,-76.376512,-76.498987,-76.466978,-76.497079,-76.560848,-76.361697,-76.482248,-76.361697,-76.479887,-76.481442,-76.482668,-76.482668,-76.528605,-76.494003,-76.528605,-76.487069,-76.482941,-76.482941,-76.528605,-76.655993,-76.482941,-76.528605,-76.528605,-76.528581,-76.528581,-76.49958,-76.49958,-76.520591,-76.498864,-76.467471,-76.494534,-76.488936,-76.496329,-76.503386,-76.494003,-76.478497,-76.489572,-76.494559,-76.494559,-76.300218,-76.180314,-76.485654,-76.467471,-76.353668,-76.494534,-76.490432,-76.490928,-76.528605,-76.48702,-76.486647,-76.49958,-76.48702,-76.48702,-76.466978,-76.493401,-76.486647,-76.484411,-76.480453,-76.480453,-76.480453,-76.480453,-76.467471,-76.48791,-76.16996,-76.466978,-76.180314,-76.180305,-76.180314,-76.485114,-76.180314,-76.180314,-76.485114,-76.485114,-76.478596,-76.483129,-76.180314,-76.475249,-76.475249,-76.475249,-76.475249,-76.478902,-76.500869,-76.500869,-76.475249,-76.504177,-76.466978,-76.474209,-76.481464,-76.493142,-76.493142,-76.493142,-76.482953,-76.474209,-76.87419,-76.499863,-76.496329,-76.496329,-76.474209,-76.500639,-76.500639,-76.466978,-76.494961,-76.466978,-76.466978,-76.498195,-76.487447,-76.487447,-76.489001,-76.489001,-76.502285,-76.494534,-76.502115,-76.180024,-76.494891,-76.494534,-76.48929,-76.48929,-76.48929,-76.490976,-76.493401,-76.493401,-76.494544,-76.494544,-76.194979,-76.194979,-76.492318,-76.495283,-76.495283,-76.456595,-76.464609,-76.467471,-76.467471,-76.467471,-76.447619,-76.485959,-76.485959,-76.486907,-76.501153,-76.430371,-76.486907,-76.479462,-76.48742,-76.487447,-76.48742,-76.624078,-76.483178,-76.467471,-76.467471,-76.467471,-76.467471,-76.492938,-76.493448,-76.495006,-76.342232,-76.466978,-76.489218,-76.494679,-76.482941,-76.497611,-76.46256,-76.481322,-76.465777,-76.489838,-76.467003,-76.481322,-76.489838,-76.481322,-76.461889,-76.491863,-76.483945,-76.488758,-76.499204,-76.496788,-76.504601,-76.490019,-76.470583,-76.505933,-76.489838,-76.481322,-76.4777,-76.447781,-76.483945,-76.447781,-76.498754,-76.450143,-76.496254,-76.431468,-76.496254,-76.496788,-76.521722,-76.489273,-76.462633,-76.489838,-76.488543,-76.466978,-76.467471,-76.467484,-76.466978,-76.480228,-76.478298,-76.489705,-76.489705,-76.480453,-76.480453,-76.480453,-76.480453,-76.467471,-76.486647,-76.484411,-76.494961,-76.480453,-76.480453,-76.482668,-76.478222,-76.528605,-76.482941,-76.486488,-76.486488,-76.490928,-76.490928,-76.490928,-76.194979,-76.482248,-76.482248,-76.528605,-76.48702,-76.194979,-76.482248,-76.488936,-76.494534,-76.481464,-76.467471,-76.494202,-76.444003,-76.528605,-76.493188,-76.47535,-76.498309,-76.494534,-76.472805,-76.467471,-76.224669,-76.467471,-76.528581,-76.528605,-76.528605,-76.528605,-76.482953,-76.466978,-76.486647,-76.48791,-76.16996,-76.180314,-76.180314,-76.180305,-76.180314,-76.485114,-76.180314,-76.180314,-76.485114,-76.485114,-76.483129,-76.180314,-76.376512,-76.480453,-76.482953,-76.466978,-76.224669,-76.224669,-76.224669,-76.474209,-76.466978,-76.498987,-76.466978,-76.497079,-76.560848,-76.361697,-76.361697,-76.479887,-76.484209,-76.475249,-76.494544,-76.466978,-76.467471,-76.467471,-76.467471,-76.467471,-76.469755,-76.483178,-76.482953,-76.49914,-76.482953,-76.300975,-76.504177,-76.463955,-76.361697,-76.361697,-76.49392,-76.361697,-76.486907,-76.50625,-76.373564,-76.464609,-76.447619,-76.494679,-76.502955,-76.497885,-76.502955,-76.497885,-76.503039,-76.502955,-76.502955,-76.497885,-76.499953,-76.16198,-76.467471,-76.467471,-76.467471,-76.482953,-76.504048,-76.474209,-76.474209,-76.497215,-76.466978,-76.466978,-76.474209,-76.489798,-76.466978,-76.466978,-76.488638,-76.482668,-76.482668,-76.474209,-76.474209,-76.482941,-76.528605,-76.528605,-76.528581,-76.528581,-76.482941,-76.482941,-76.482941,-76.528605,-76.49958,-76.49958,-76.471375,-76.444611,-76.475249,-76.472805,-76.482953,-76.467471,-76.471978,-76.448793,-76.467471,-76.394187,-76.466978,-76.466978,-76.467471,-76.467471,-76.467471,-76.48742,-76.48742,-76.488012,-76.487951,-76.466978,-76.511472,-76.482941,-76.49914,-76.474209,-76.472023,-76.498242,-76.472805,-76.492938,-76.493448,-76.466978,-76.466978,-76.482953,-76.466978,-76.224669,-76.224669,-76.224669,-76.376512,-76.466978,-76.497079,-76.560848,-76.361697,-76.361697,-76.479887,-76.484209,-76.180314,-76.493401,-76.466978,-76.466978,-76.482953,-76.300975,-76.504177,-76.463955,-76.361697,-76.361697,-76.466978,-76.361697,-76.486907,-76.50625,-76.373564,-76.464609,-76.447619,-76.494679,-76.502955,-76.497885,-76.502955,-76.497885,-76.482953,-76.503039,-76.502955,-76.502955,-76.497885,-76.499953,-76.16198,-76.467471,-76.467471,-76.467471,-76.482953,-76.504048,-76.474209,-76.474209,-76.480453,-76.480453,-76.482668,-76.474209,-76.474209,-76.655993,-76.528605,-76.528605,-76.528581,-76.528581,-76.528581,-76.482941,-76.482941,-76.482941,-76.49958,-76.49958,-76.466978,-76.466978,-76.494559,-76.489572,-76.494559,-76.494202,-76.494556,-76.507892,-76.485114,-76.4813,-76.484494,-76.531696,-76.478286,-76.478286,-76.472805,-76.494202,-76.494556,-76.478497,-76.489572,-76.494559,-76.494559,-76.300218,-76.180314,-76.186834,-76.487365,-76.461889,-76.481804,-76.498008,-76.482668,-76.528654,-76.465467,-76.528605,-76.490928,-76.528605,-76.48702,-76.466978,-76.482953,-76.482953,-76.482941,-76.466978,-76.497215,-76.466978,-76.466978,-76.474209,-76.489798,-76.466978,-76.488638,-76.472023,-76.498242,-76.472805,-76.492938,-76.493448,-76.466978,-76.466978,-76.224669,-76.224669,-76.224669,-76.474209,-76.376512,-76.466978,-76.469755,-76.497079,-76.560848,-76.361697,-76.361697,-76.479887,-76.553679,-76.500433,-76.451632,-76.480453,-76.499421,-76.483178,-76.48791,-76.192333,-76.489798,-76.467471,-76.467471,-76.467471,-76.49914,-76.300975,-76.504177,-76.463955,-76.361697,-76.361697,-76.361697,-76.50625,-76.373564,-76.501879,-76.480453,-76.624078,-76.502955,-76.481021,-76.184849,-76.480228,-76.16198,-76.482668,-76.482668,-76.474209,-76.528605,-76.655993,-76.482941,-76.528581,-76.528605,-76.528605,-76.528581,-76.528581,-76.482941,-76.481464,-76.474209,-76.224669,-76.394997,-76.471375,-76.42943,-76.477629,-76.33975,-76.499408,-76.482953,-76.467471,-76.467471,-76.467471,-76.467471,-76.53759,-76.493448,-76.361697,-76.361697,-76.500668,-76.482248,-76.474209,-76.466978,-76.48791,-76.474209,-76.482248,-76.474209,-76.474209,-76.482941,-76.465467,-76.396482,-76.412422,-76.482248,-76.528654,-76.493448,-76.482953,-76.464609,-76.447619,-76.494679,-76.502955,-76.497885,-76.502955,-76.497885,-76.503039,-76.502955,-76.502955,-76.497885,-76.499953,-76.467471,-76.467471,-76.467471,-76.504048,-76.50152,-76.480453,-76.493308,-76.482941,-76.49958,-76.467471,-76.467471,-76.467471,-76.471978,-76.448793,-76.467471,-76.394187,-76.466978,-76.488488,-76.476997],null,null,null,{"interactive":true,"draggable":false,"keyboard":true,"title":"","alt":"","zIndexOffset":0,"opacity":1,"riseOnHover":false,"riseOffset":250},null,null,null,null,null,{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null]}],"limits":{"lat":[42.1070610000001,42.696194],"lng":[-76.87419,-76.16198]}},"evals":[],"jsHooks":[]}</script>

<!--/html_preserve-->

# Summary

1.  We can clean and prepare our data for analysis using the verbs of
    `dplyr`. These will take us remarkably far and help structure our
    thinking about writing code. Less looking up functions, more writing
    code.

2.  We use `ggplot2` to make beautiful data visualization with the data
    that we wrangle with `dplyr`. Setting up a *tidy* set of data allows
    us to pass this data frame, or summaries of it, to `ggplot2` to make
    all the plots that our hearts desire. Data visualization is a key
    part of exploratory data analysis\!

3.  When we have *spatial* data, the `sf` library gives us tools to use
    these data within our existing `dplyr` and `ggplot2` pipeline. We
    are just scratching the surface of the spatial analysis we can do
    with simple features data frames, but the most important thing is
    that most of the spatial stuff goes on behind the scenes and we can
    focus on what questions we want to answer with our data.

![](./etc/meme.jpg)
