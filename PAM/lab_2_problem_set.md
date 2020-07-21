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
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.0.1

    ## ── Attaching packages ──────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.1     ✓ dplyr   1.0.0
    ## ✓ tidyr   1.1.0     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## Warning: package 'tidyr' was built under R version 4.0.1

    ## Warning: package 'readr' was built under R version 4.0.1

    ## Warning: package 'forcats' was built under R version 4.0.1

    ## ── Conflicts ─────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(sf)
```

    ## Warning: package 'sf' was built under R version 4.0.2

    ## Linking to GEOS 3.8.1, GDAL 3.1.1, PROJ 6.3.1

``` r
library(lubridate)
```

    ## Warning: package 'lubridate' was built under R version 4.0.1

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
library(leaflet)
```

    ## Warning: package 'leaflet' was built under R version 4.0.2

``` r
library(scales)
```

    ## 
    ## Attaching package: 'scales'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     discard

    ## The following object is masked from 'package:readr':
    ## 
    ##     col_factor

``` r
library(Hmisc)
```

    ## Warning: package 'Hmisc' was built under R version 4.0.2

    ## Loading required package: lattice

    ## Loading required package: survival

    ## Loading required package: Formula

    ## Warning: package 'Formula' was built under R version 4.0.2

    ## 
    ## Attaching package: 'Hmisc'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     src, summarize

    ## The following objects are masked from 'package:base':
    ## 
    ##     format.pval, units

``` r
load("./input/ithaca_rentals.RData")
ls()
```

    ## [1] "scraped"

## Create a new data frame that is limited to 1 bedroom units.

``` r
oneBed <- filter(scraped, scraped_beds == "1BR")
```

## Mutate fields in `scraped` that are currently character but should be numeric as new columns.

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

``` r
scraped <- mutate(scraped,
                  clean_beds = parse_number(scraped_beds),
                  clean_baths = parse_number(scraped_baths),
                  clean_rent = parse_number(scraped_rent),
                  clean_sqft = parse_number(ifelse(str_detect(scraped_sqft, pattern = "available"), NA, scraped_sqft)),
                  clean_post_id = parse_number(post_id))
```

    ## Warning: 84 parsing failures.
    ##  row col expected   actual
    ##  296  -- a number sharedBa
    ##  367  -- a number sharedBa
    ##  454  -- a number sharedBa
    ##  975  -- a number sharedBa
    ## 1306  -- a number sharedBa
    ## .... ... ........ ........
    ## See problems(...) for more details.

    ## Warning: 213 parsing failures.
    ## row col expected actual
    ## 438  -- a number      -
    ## 529  -- a number      -
    ## 568  -- a number      -
    ## 584  -- a number      -
    ## 601  -- a number      -
    ## ... ... ........ ......
    ## See problems(...) for more details.

## Create a new data frame with listings that mention “affordable” in their title

``` r
scraped_affordable <- 
  filter(scraped, str_detect(listing_title, pattern = "affordable"))
summarise(scraped_affordable)
```

    ## Simple feature collection with 1 feature and 0 fields
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -76.63098 ymin: 42.34557 xmax: -76.32763 ymax: 42.51139
    ## geographic CRS: WGS 84
    ##                         geometry
    ## 1 MULTIPOINT ((-76.63098 42.3...

## Create a column in `scraped` indicating whether the rent asked is more than $800.

``` r
scraped <- mutate(scraped,
                  above_800 = clean_rent > 800)
table(scraped$above_800)
```

    ## 
    ## FALSE  TRUE 
    ##  1806 11347

## Summarize the average square footage for 1, 2 and 3 bedroom units.

``` r
scraped %>% 
  filter(!is.na(clean_beds), clean_beds < 4, clean_beds > 0, !is.na(clean_sqft)) %>%
  group_by(clean_beds) %>%
  summarise(avg_sqft = mean(clean_sqft))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## Simple feature collection with 3 features and 2 fields
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.66828 ymin: 42.10337 xmax: -76.16198 ymax: 42.7929
    ## geographic CRS: WGS 84
    ## # A tibble: 3 x 3
    ##   clean_beds avg_sqft                                                   geometry
    ##        <dbl>    <dbl>                                           <MULTIPOINT [°]>
    ## 1          1     683. ((-76.86736 42.38024), (-76.66191 42.54604), (-76.65838 4…
    ## 2          2     986. ((-76.8791 42.38874), (-76.81691 42.17695), (-76.81673 42…
    ## 3          3    1292. ((-78.66828 42.7929), (-76.66245 42.53932), (-76.66099 42…

## Create a summary statistic table with the minimum, maximum and average rent values for 1 bedroom units.

``` r
bed1_rent <- 
  scraped %>%
  filter(clean_beds == 1, !is.na(clean_beds)) %>%
  group_by(clean_beds) %>%
  summarise(min = min(clean_rent),
            max = max(clean_rent),
            avg = mean(clean_rent))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
bed1_rent
```

    ## Simple feature collection with 1 feature and 4 fields
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.90302 ymin: 42.10706 xmax: -76.17315 ymax: 42.93978
    ## geographic CRS: WGS 84
    ## # A tibble: 1 x 5
    ##   clean_beds   min   max   avg                                          geometry
    ##        <dbl> <dbl> <dbl> <dbl>                                  <MULTIPOINT [°]>
    ## 1          1     1  2400 1088. ((-78.90302 42.93978), (-76.86736 42.38024), (-7…

## Create a summary table for the proportion of 1, 2 and 3 bedroom units with rents below Fair Market Rent levels set by the Department of Housing and Urban Development.

You will want to consult
[this](https://www.rentdata.org/ithaca-ny-msa/2018) site for the FMR
values. Hint: you could use `case_when()` to create a FMR column with
each bedroom size’s FMR value and then `mutate()` another column
flagging if the row’s rent was greater than or less than the FMR.

``` r
scraped <- mutate(scraped, 
                  FMR = case_when(
                    clean_beds == 1 ~ 978,
                    clean_beds == 2 ~ 1164,
                    clean_beds == 3 ~ 1495)) 
scraped <- mutate(scraped, 
                  compare_FMR = case_when(
                    clean_rent > FMR ~ "above",
                    clean_rent < FMR ~ "below"))
bed_FMR <- 
  scraped %>%
  filter(!is.na(clean_beds), clean_beds < 4, clean_beds > 0, !is.na(compare_FMR)) %>%
  group_by(clean_beds) %>%
  summarise(below_FMR = percent(sum(compare_FMR == "below")/length(compare_FMR)),
            above_FMR = percent(sum(compare_FMR == "above")/length(compare_FMR)))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
bed_FMR
```

    ## Simple feature collection with 3 features and 3 fields
    ## geometry type:  MULTIPOINT
    ## dimension:      XY
    ## bbox:           xmin: -78.90302 ymin: 42.10337 xmax: -76.03615 ymax: 42.93978
    ## geographic CRS: WGS 84
    ## # A tibble: 3 x 4
    ##   clean_beds below_FMR above_FMR                                        geometry
    ##        <dbl> <chr>     <chr>                                    <MULTIPOINT [°]>
    ## 1          1 30%       70%       ((-78.90302 42.93978), (-76.86736 42.38024), (…
    ## 2          2 15%       85%       ((-76.8791 42.38874), (-76.87419 42.38192), (-…
    ## 3          3 32%       68%       ((-78.66828 42.7929), (-76.66245 42.53932), (-…

## If housing assistance allows households to rent units up to the FMR level, how much choice would you say they have on the rental markes? What policy proposals, if any, would you propose given the evidence you’ve generated using current rental listings?

30% of the 1-bedroom units, 15% of the 2-bedroom units, and 32% of the
3-bedroom units are available according to the housing assistance. Since
there are less than 50% of the rental units available, the choice is
very limited on the rental market. To give households more choices, a
policy in regulating rental prices should be formulated to keep most of
the rental units, especially 2-bedroom units, below the Fair Market Rent
levels. Rental units with prices slightly higher than the FMR should be
encouraged to lower their prices.

<br>

<hr>

<br>

# Hands-on Task 2: Making some plots of the Craigslist data

## Create and interpret a scatterplot of square footage by rent asked for 2 bedroom listings using `ggplot()`.

There is a moderate positive linear relationship between rent and square
footage in listings with 2 bedroom. The higher the square footage is,
the higher the rent is, with a few outliers at a square footage of 3000.

``` r
twoBeds_sqft_rent <- 
  scraped %>% 
  filter (!is.na(clean_rent), 
          !is.na(clean_sqft), 
          str_detect(listing_title, regex("2 bedroom", ignore_case = TRUE))) %>%
  select(clean_rent, clean_sqft)
ggplot(twoBeds_sqft_rent, aes(x = clean_sqft, y = clean_rent)) + 
  geom_point() + 
  geom_smooth(method='lm', formula= y~x) + 
  labs(x = "Square footage", y = "Rent")
```

![](lab_2_problem_set_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

## Create and interpret a bar chart of average square footage by bedroom size using `ggplot()`.

In general, the higher the bedroom number is, the higher the average
square footage is.

``` r
bed_avg_sqft <-
  scraped %>%
  select(clean_beds, clean_sqft) %>%
  filter(!is.na(clean_beds), !is.na(clean_sqft)) %>%
  group_by(clean_beds) %>%
  summarise(mean = mean(clean_sqft))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
ggplot(bed_avg_sqft, aes(x = clean_beds, y = mean)) +
  geom_bar(stat = "identity") + 
  labs(x = "Bedroom size", y = "Square footage")
```

![](lab_2_problem_set_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

## Create and interpret a histogram of square footage using `ggplot()`.

The distribution of square footage is right skewed with a center at
around 800 (most units have a square footage of approximately 800. The
square footage range from 180 to 4800. There are several outliers at
around 4800 and a gap at around 2700.

``` r
ggplot(scraped, aes(x = clean_sqft)) +
  geom_histogram() + 
  labs(x = "Square footage", y = "Count")
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 5738 rows containing non-finite values (stat_bin).

![](lab_2_problem_set_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

## Create and interpret a ggplot of your choice using the listing data that incorporates the color aesthetic.

As square footage increases, rent also increases. In addition, most
units have a bathroom number at the lower end (around 1 and 2) , as
square footage and rent increase, the number of bathrooms also increase
(there are some exceptions in the middle range of the square footage).

``` r
ggplot(scraped, aes(x = clean_sqft, y = clean_rent, color = clean_baths)) + 
  geom_point() + 
  labs(x = "Square footage", y = "Rent", color = "Number of bathrooms") + 
  scale_color_gradientn(colors = c("#07123b", "#64b1e8", "#e3f3ff"))
```

    ## Warning: Removed 5738 rows containing missing values (geom_point).

![](lab_2_problem_set_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

<br>

<hr>

<br>

# Hands-on Task 3: Correlation

## Estimate the correlation between square footage and rent overall and interpret this statistic.

There is a strong positive correlation between square footage and rent
as indicated by the large correlation coefficient (0.74). In other
words, rent increases with square footage. In addition, a small p-value
(p-value \< 2.2e-16) indicates that the correlation is significant.

``` r
cor.test(scraped$clean_sqft, scraped$clean_rent, method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  scraped$clean_sqft and scraped$clean_rent
    ## t = 94.928, df = 7413, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.7302645 0.7508170
    ## sample estimates:
    ##      cor 
    ## 0.740714

<br>

<hr>

<br>

# Hands-on Task 4: Make a map

## Create a map of 2 bedroom units listed in May with `ggplot()` or `leaflet()`

``` r
twoBeds <- scraped %>% 
  filter(clean_beds == 2)
twoBeds <- st_set_crs(twoBeds, "EPSG:4326")
ggplot(twoBeds) +
  geom_sf()
```

![](lab_2_problem_set_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
# The leaflet code is here but I am commenting it out since otherwise it won't let me knit to a markdown file with the html output
#leaflet(twoBeds) %>%
#  addTiles() %>%
#  addMarkers()
```

## Create a map of 1 bedroom units listed in May that have a rent asked that is below Fair Market Rent with `ggplot()` or `leaflet()`

``` r
oneBed_May <- scraped %>% 
  filter(clean_beds == 1, 
         compare_FMR == "below", 
         listing_date >= "2020-05-01", 
         listing_date < "2020-06-01")
oneBed_May <- st_set_crs(oneBed_May, "EPSG:4326")
ggplot(oneBed_May) +
  geom_sf()
```

![](lab_2_problem_set_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

``` r
# The leaflet code is here but I am commenting it out since otherwise it won't let me knit to a markdown file with the html output
#leaflet(oneBed_May) %>%
#  addTiles() %>%
#  addMarkers()
```
