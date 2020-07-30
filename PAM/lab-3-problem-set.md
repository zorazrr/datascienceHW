Lab 3 Problem Set
================

  - [Hands-on Task 1: Prepare county-level COVID-19 cases
    data](#hands-on-task-1-prepare-county-level-covid-19-cases-data)
      - [Load the county-level COVID-19 cases
        data](#load-the-county-level-covid-19-cases-data)
      - [Join county-level COVID-19 cases data frame with county IDs
        data
        crosswalk](#join-county-level-covid-19-cases-data-frame-with-county-ids-data-crosswalk)
      - [Create/prepare a date variable for the county-level COVID-19
        cases data
        frame](#createprepare-a-date-variable-for-the-county-level-covid-19-cases-data-frame)
      - [Create a data frame that is limited to counties in the state of
        New
        York](#create-a-data-frame-that-is-limited-to-counties-in-the-state-of-new-york)
      - [Create a map showing the rate of total COVID-19 cases by county
        in **New York State** on **June 29,
        2020**](#create-a-map-showing-the-rate-of-total-covid-19-cases-by-county-in-new-york-state-on-june-29-2020)
      - [Identify the 5 largest counties in New York State based on 2019
        population](#identify-the-5-largest-counties-in-new-york-state-based-on-2019-population)
      - [Plot time series of COVID-19 case rate over time for the 5
        largest counties in New York
        State](#plot-time-series-of-covid-19-case-rate-over-time-for-the-5-largest-counties-in-new-york-state)
      - [Plot time series of COVID-19 **NEW** case rate over time for
        the 5 largest counties in New York
        State](#plot-time-series-of-covid-19-new-case-rate-over-time-for-the-5-largest-counties-in-new-york-state)
  - [Hands-on Task 2: Prepare daily county-level spending
    data](#hands-on-task-2-prepare-daily-county-level-spending-data)
      - [Load the spending data](#load-the-spending-data)
      - [Join spending data with county IDs data
        crosswalk](#join-spending-data-with-county-ids-data-crosswalk)
      - [Create/prepare a date variable for the county-level spending
        data
        frame](#createprepare-a-date-variable-for-the-county-level-spending-data-frame)
      - [Create a spending data frame that is limited to counties in the
        state of New
        York](#create-a-spending-data-frame-that-is-limited-to-counties-in-the-state-of-new-york)
      - [Create a map showing all spending relative to January by county
        in New York State on June 29, 2020 (use the variable for *all
        merchant category
        codes*)](#create-a-map-showing-all-spending-relative-to-january-by-county-in-new-york-state-on-june-29-2020-use-the-variable-for-all-merchant-category-codes)
      - [Plot time series of ALL spending changes over time (relative to
        January) for the 5 largest counties in New York
        State](#plot-time-series-of-all-spending-changes-over-time-relative-to-january-for-the-5-largest-counties-in-new-york-state)
  - [Hands-on Task 3: Correlation](#hands-on-task-3-correlation)
      - [Join the county-level COVID-cases data frame with the spending
        data
        frame](#join-the-county-level-covid-cases-data-frame-with-the-spending-data-frame)
      - [Estimate the correlation between the NEW case rates and
        spending
        changes](#estimate-the-correlation-between-the-new-case-rates-and-spending-changes)
      - [Estimate the correlation between NEW confirmed case COUNTS and
        spending
        changes](#estimate-the-correlation-between-new-confirmed-case-counts-and-spending-changes)

In this problem set you will open, process, and analyze the county-level
COVID-19 cases dataset. You will then open, process, and analyze the
county-level credit card spending data. Lastly, you will explore the
relationship between spending and COVID-19.

# Hands-on Task 1: Prepare county-level COVID-19 cases data

## Load the county-level COVID-19 cases data

Go to the [Economic Tracker GitHub data
repository](https://github.com/Opportunitylab/EconomicTracker/tree/main/data)
and find the county-level COVID-19 cases dataset. Then read in the raw
.CSV file by using the URL of the page containing the data. You may need
to refer to the data dictionary to get more information about each
available dataset.

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.0.1

    ## ── Attaching packages ─────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.1     ✓ dplyr   1.0.0
    ## ✓ tidyr   1.1.0     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## Warning: package 'tidyr' was built under R version 4.0.1

    ## Warning: package 'readr' was built under R version 4.0.1

    ## Warning: package 'forcats' was built under R version 4.0.1

    ## ── Conflicts ────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(sf) 
```

    ## Warning: package 'sf' was built under R version 4.0.2

    ## Linking to GEOS 3.8.1, GDAL 3.1.1, PROJ 6.3.1

``` r
library(tidycensus)
```

    ## Warning: package 'tidycensus' was built under R version 4.0.2

``` r
url <- "https://raw.githubusercontent.com/OpportunityInsights/EconomicTracker/main/data/COVID%20Cases%20-%20County%20-%20Daily.csv"
covid_cases <- read.csv(url, na.strings = c('', '.', 'NA'))
```

## Join county-level COVID-19 cases data frame with county IDs data crosswalk

Go to the [Economic Tracker GitHub data
repository](https://github.com/Opportunitylab/EconomicTracker/tree/main/data)
and find the county geographic ID crosswalk dataset. Then read in the
raw .CSV file by using the URL of the page containing the data. You may
need to refer to the data dictionary to get more information about each
available dataset.

Load the county ID crosswalk:

``` r
geo_url <- "https://raw.githubusercontent.com/OpportunityInsights/EconomicTracker/main/data/GeoIDs%20-%20County.csv"
geo_id <- read.csv(geo_url)
```

Join the county-level COVID-19 cases data frame with the county
geographic ID crosswalk data frame (you may need to look for the
matching ID that will allow you to link the two data frames):

``` r
covid_cases <- left_join(covid_cases, geo_id,
                         by = 'countyfips')
```

## Create/prepare a date variable for the county-level COVID-19 cases data frame

``` r
covid_cases <- covid_cases %>%
  mutate(date = as.Date(paste(year, month, day, sep = '-'), '%Y-%m-%d'))
```

## Create a data frame that is limited to counties in the state of New York

``` r
covid_NY <- filter(covid_cases, statename == "New York")
```

## Create a map showing the rate of total COVID-19 cases by county in **New York State** on **June 29, 2020**

### Obtain **county-level** geometries for New York State

Remember you can use this guide of how to use `tidycensus`:
<https://walker-data.com/tidycensus/articles/basic-usage.html#working-with-acs-data-1>.
You can also refer to the lab and/or videos for instructions on how to
use it.

You must obtain an API key to request data through the `tidycensus()`
package (please refer to the lab and/or videos for details on how to do
this).

``` r
library(tidycensus)
census_api_key("7ed0f6ce1181eb8bd9a3063d11e87b978c7fcaa2", install = TRUE, overwrite = TRUE) 
```

    ## Your original .Renviron will be backed up and stored in your R HOME directory if needed.

    ## Your API key has been stored in your .Renviron and can be accessed by Sys.getenv("CENSUS_API_KEY"). 
    ## To use now, restart R or run `readRenviron("~/.Renviron")`

    ## [1] "7ed0f6ce1181eb8bd9a3063d11e87b978c7fcaa2"

``` r
# the information from the nearest year does not work for me, so I'm using 2017 data
acs5_2017_vars <- load_variables(2017, "acs5", cache = TRUE)
county_num <- get_acs(geography = "county",
                     variables = 'B06012_001', year = 2017, geometry = TRUE)
```

    ## Getting data from the 2013-2017 5-year ACS

    ## Downloading feature geometry from the Census website.  To cache shapefiles for use in future sessions, set `options(tigris_use_cache = TRUE)`.

    ##   |                                                                              |                                                                      |   0%  |                                                                              |                                                                      |   1%  |                                                                              |=                                                                     |   1%  |                                                                              |=                                                                     |   2%  |                                                                              |==                                                                    |   2%  |                                                                              |==                                                                    |   3%  |                                                                              |==                                                                    |   4%  |                                                                              |===                                                                   |   4%  |                                                                              |===                                                                   |   5%  |                                                                              |====                                                                  |   5%  |                                                                              |====                                                                  |   6%  |                                                                              |=====                                                                 |   7%  |                                                                              |=====                                                                 |   8%  |                                                                              |======                                                                |   8%  |                                                                              |======                                                                |   9%  |                                                                              |=======                                                               |   9%  |                                                                              |=======                                                               |  10%  |                                                                              |=======                                                               |  11%  |                                                                              |========                                                              |  11%  |                                                                              |========                                                              |  12%  |                                                                              |=========                                                             |  12%  |                                                                              |=========                                                             |  13%  |                                                                              |=========                                                             |  14%  |                                                                              |==========                                                            |  14%  |                                                                              |==========                                                            |  15%  |                                                                              |===========                                                           |  15%  |                                                                              |===========                                                           |  16%  |                                                                              |============                                                          |  16%  |                                                                              |============                                                          |  17%  |                                                                              |============                                                          |  18%  |                                                                              |=============                                                         |  18%  |                                                                              |=============                                                         |  19%  |                                                                              |==============                                                        |  19%  |                                                                              |==============                                                        |  20%  |                                                                              |==============                                                        |  21%  |                                                                              |===============                                                       |  21%  |                                                                              |===============                                                       |  22%  |                                                                              |================                                                      |  22%  |                                                                              |================                                                      |  23%  |                                                                              |================                                                      |  24%  |                                                                              |=================                                                     |  24%  |                                                                              |=================                                                     |  25%  |                                                                              |==================                                                    |  25%  |                                                                              |==================                                                    |  26%  |                                                                              |===================                                                   |  26%  |                                                                              |===================                                                   |  27%  |                                                                              |===================                                                   |  28%  |                                                                              |====================                                                  |  28%  |                                                                              |====================                                                  |  29%  |                                                                              |=====================                                                 |  29%  |                                                                              |=====================                                                 |  30%  |                                                                              |=====================                                                 |  31%  |                                                                              |======================                                                |  31%  |                                                                              |======================                                                |  32%  |                                                                              |=======================                                               |  32%  |                                                                              |=======================                                               |  33%  |                                                                              |=======================                                               |  34%  |                                                                              |========================                                              |  34%  |                                                                              |========================                                              |  35%  |                                                                              |=========================                                             |  35%  |                                                                              |=========================                                             |  36%  |                                                                              |==========================                                            |  36%  |                                                                              |==========================                                            |  37%  |                                                                              |==========================                                            |  38%  |                                                                              |===========================                                           |  38%  |                                                                              |===========================                                           |  39%  |                                                                              |============================                                          |  39%  |                                                                              |============================                                          |  40%  |                                                                              |============================                                          |  41%  |                                                                              |=============================                                         |  41%  |                                                                              |=============================                                         |  42%  |                                                                              |==============================                                        |  42%  |                                                                              |==============================                                        |  43%  |                                                                              |==============================                                        |  44%  |                                                                              |===============================                                       |  44%  |                                                                              |===============================                                       |  45%  |                                                                              |================================                                      |  45%  |                                                                              |================================                                      |  46%  |                                                                              |=================================                                     |  47%  |                                                                              |=================================                                     |  48%  |                                                                              |==================================                                    |  48%  |                                                                              |==================================                                    |  49%  |                                                                              |===================================                                   |  49%  |                                                                              |===================================                                   |  50%  |                                                                              |===================================                                   |  51%  |                                                                              |====================================                                  |  51%  |                                                                              |====================================                                  |  52%  |                                                                              |=====================================                                 |  52%  |                                                                              |=====================================                                 |  53%  |                                                                              |=====================================                                 |  54%  |                                                                              |======================================                                |  54%  |                                                                              |======================================                                |  55%  |                                                                              |=======================================                               |  55%  |                                                                              |=======================================                               |  56%  |                                                                              |========================================                              |  57%  |                                                                              |========================================                              |  58%  |                                                                              |=========================================                             |  58%  |                                                                              |=========================================                             |  59%  |                                                                              |==========================================                            |  59%  |                                                                              |==========================================                            |  60%  |                                                                              |==========================================                            |  61%  |                                                                              |===========================================                           |  61%  |                                                                              |===========================================                           |  62%  |                                                                              |============================================                          |  62%  |                                                                              |============================================                          |  63%  |                                                                              |============================================                          |  64%  |                                                                              |=============================================                         |  64%  |                                                                              |=============================================                         |  65%  |                                                                              |==============================================                        |  65%  |                                                                              |==============================================                        |  66%  |                                                                              |===============================================                       |  66%  |                                                                              |===============================================                       |  67%  |                                                                              |===============================================                       |  68%  |                                                                              |================================================                      |  68%  |                                                                              |================================================                      |  69%  |                                                                              |=================================================                     |  69%  |                                                                              |=================================================                     |  70%  |                                                                              |=================================================                     |  71%  |                                                                              |==================================================                    |  71%  |                                                                              |==================================================                    |  72%  |                                                                              |===================================================                   |  72%  |                                                                              |===================================================                   |  73%  |                                                                              |====================================================                  |  74%  |                                                                              |====================================================                  |  75%  |                                                                              |=====================================================                 |  75%  |                                                                              |=====================================================                 |  76%  |                                                                              |======================================================                |  76%  |                                                                              |======================================================                |  77%  |                                                                              |======================================================                |  78%  |                                                                              |=======================================================               |  78%  |                                                                              |=======================================================               |  79%  |                                                                              |========================================================              |  79%  |                                                                              |========================================================              |  80%  |                                                                              |========================================================              |  81%  |                                                                              |=========================================================             |  81%  |                                                                              |=========================================================             |  82%  |                                                                              |==========================================================            |  82%  |                                                                              |==========================================================            |  83%  |                                                                              |==========================================================            |  84%  |                                                                              |===========================================================           |  84%  |                                                                              |===========================================================           |  85%  |                                                                              |============================================================          |  85%  |                                                                              |============================================================          |  86%  |                                                                              |=============================================================         |  87%  |                                                                              |=============================================================         |  88%  |                                                                              |==============================================================        |  88%  |                                                                              |==============================================================        |  89%  |                                                                              |===============================================================       |  89%  |                                                                              |===============================================================       |  90%  |                                                                              |===============================================================       |  91%  |                                                                              |================================================================      |  91%  |                                                                              |================================================================      |  92%  |                                                                              |=================================================================     |  92%  |                                                                              |=================================================================     |  93%  |                                                                              |=================================================================     |  94%  |                                                                              |==================================================================    |  94%  |                                                                              |==================================================================    |  95%  |                                                                              |===================================================================   |  95%  |                                                                              |===================================================================   |  96%  |                                                                              |====================================================================  |  97%  |                                                                              |====================================================================  |  98%  |                                                                              |===================================================================== |  98%  |                                                                              |===================================================================== |  99%  |                                                                              |======================================================================|  99%  |                                                                              |======================================================================| 100%

### Make the county ID column in the geometries data frame compatible with the county-level COVID cases data frame

Convert the `GEOID` variable/column into numeric format. Make sure to
use the `as.numeric()` function.

``` r
NY_geo <- 
  county_num %>%
  filter(str_detect(NAME, pattern = "New York")) %>%
  select(GEOID, NAME, geometry) %>%
  mutate(GEOID = as.numeric(GEOID))
```

### Use the COVID-19 cases data frame and create a data frame that only includes the June 29, 2020 observations in New York State

``` r
covid_NY_June_29 <- covid_cases %>%
  filter(date == '2020-06-29' & statename == "New York")
```

### Join the June 29, 2020 county-level COVID-19 cases data frame with the county-level geography data frame

Note, that your `inner_join()` or `left_join()` must call the county
geometry data frame as the first argument and the COVID-cases data frame
as the second argument. Otherwise, the new data frame will not properly
maintain the geometries column for mapping.

``` r
covid_NY_June_29 <- left_join(NY_geo, covid_NY_June_29,
                              by = c('GEOID' = 'countyfips'))
```

### Create a map of the total COVID-19 case rate by county in New York State on June 29, 2020

``` r
covid_NY_June_29 %>%
  ggplot() + 
  geom_sf(aes(fill = case_rate) , color = 'gray') + 
  coord_sf(crs = 5070) +
  ggtitle("COVID cases by county in New York on June 29, 2020") + 
  scale_fill_viridis_c()
```

![](lab_3_problem_set_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

### Describe the map you just made and any interesting facts you can learn from it

Most counties in New York have a case rate lower than 1000. Some
counties have a case rate at around 1500. However, the west part of New
York State has a significantly higher covid case rate of around 3000.
The highest case rate of more than 4000 is seen at Rockland County
(shown by color yellow).

## Identify the 5 largest counties in New York State based on 2019 population

5 largest counties: Kings, Queens, New York, Suffolk, Bronx

``` r
NY_pop_rank <- covid_NY %>%
  group_by(countyname) %>%
  summarize(county_pop2019 = max(county_pop2019)) %>%
  arrange(desc(county_pop2019))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
head(NY_pop_rank)
```

    ## # A tibble: 6 x 2
    ##   countyname county_pop2019
    ##   <chr>               <int>
    ## 1 Kings             2559903
    ## 2 Queens            2253858
    ## 3 New York          1628706
    ## 4 Suffolk           1476601
    ## 5 Bronx             1418207
    ## 6 Nassau            1356924

## Plot time series of COVID-19 case rate over time for the 5 largest counties in New York State

For the rest of this assignment focus on the COVID cases data set
**across all of 2020** (NOT JUST June 29, 2020)

``` r
covid_NY %>%
  filter(countyname %in% c('Kings', 'Queens', 'New York', 'Suffolk', 'Bronx')) %>%
  ggplot(aes(x = date, y = case_rate, color = countyname)) +
  geom_line() +
  labs(x = "Date", 
       y = 'Confirmed COVID-19 cases per 100,000 people', 
       color = "County") +
  scale_y_continuous(labels = function(y) format(y, scientific=FALSE))
```

    ## Warning: Removed 160 row(s) containing missing values (geom_path).

![](lab_3_problem_set_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

### Describe the plot you just made and any interesting facts you can learn from it

The curves are identical: increasing at a high rate from March to June
and becoming more flattened at around July. Among the 5 counties, Bronx
county has the highest covid-19 case rate throughout the months and New
York has the lowest case rate. There is no correspondance between case
rate and total population.

## Plot time series of COVID-19 **NEW** case rate over time for the 5 largest counties in New York State

For the rest of this assignment focus on the COVID cases data set across
all time (NOT JUST June 29, 2020)

``` r
covid_NY %>%
  filter(countyname %in% c('Kings', 'Queens', 'New York', 'Suffolk', 'Bronx')) %>%
  ggplot(aes(x = date, y = new_case_rate, color = countyname)) +
  geom_line() +
  labs(x = "Date", 
       y = 'Confirmed new COVID-19 cases', 
       color = "County") +
  scale_y_continuous(labels = function(y) format(y, scientific=FALSE))
```

    ## Warning: Removed 194 row(s) containing missing values (geom_path).

![](lab_3_problem_set_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

### Describe the plot you just made and any interesting facts you can learn from it

There is no covid-19 infection at the start of March. However, the new
confirmed covid-19 cases increase rapidly through March, reaching a peak
at the start of April, and start to decrease after the peak. Among the 5
counties, Bronx has the highest new case rate while New York has the
lowest New case rate.

# Hands-on Task 2: Prepare daily county-level spending data

Here you will work with county-level spending data from Affinity
Solutions. You can read more about these data at the [Opportunity Lab
Economic Tracker GitHub
repository](https://github.com/Opportunitylab/EconomicTracker).

## Load the spending data

Go to the [Economic Tracker GitHub data
repository](https://github.com/Opportunitylab/EconomicTracker/tree/main/data)
and find county-level Affinity spending dataset. Then read in the raw
.CSV file by using the URL of the page containing the data. You may need
to refer to the data dictionary to get more information about each
available dataset.

``` r
spending_url <- "https://raw.githubusercontent.com/OpportunityInsights/EconomicTracker/21d25fc0ecab0c49e8657a5fb4dc84ae72c86cf0/data/Affinity%20-%20County%20-%20Daily.csv"
options(scipen=999)
spending <- read.csv(spending_url)
```

## Join spending data with county IDs data crosswalk

Join the county ID crosswalk data frame onto the spending data frame.
You already obtained this data frame in Hands-on Task 1 (again, you may
need to look at the two data frames to find the county ID required for
joining):

``` r
geo_spending <- left_join(spending, geo_id,
                          by = 'countyfips')
```

## Create/prepare a date variable for the county-level spending data frame

``` r
geo_spending <- geo_spending %>%
  mutate(date = as.Date(paste(year, month, day, sep = '-'), '%Y-%m-%d'))
```

## Create a spending data frame that is limited to counties in the state of New York

``` r
NY_spending <- filter(geo_spending, stateabbrev == "NY")
```

## Create a map showing all spending relative to January by county in New York State on June 29, 2020 (use the variable for *all merchant category codes*)

Carefully read the definition of the variables in the spending dataset

### Create a spending data frame with only the June 29, 2020 observations in New York State

``` r
spending_NY_June_29 <- 
  NY_spending %>%
  filter(date == '2020-06-29')
```

### Join the June 29, 2020 county-level spending data frame with the county-level geography data frame that was created in Hands-on Task 1

Note, that your `inner_join()` or `left_join()` must call the county
geometry data frame as the first argument and the spending data frame as
the second argument. Otherwise, the new data frame will not properly
maintain the geometries column for mapping.

``` r
spending_joined <- 
  left_join(NY_geo, spending_NY_June_29, 
            by = c('GEOID' ='countyfips'))
```

### Create a map of spending changes by county in New York State on June 29, 2020

Note: some counties will not have spending data

``` r
spending_joined %>%
  ggplot() + 
  geom_sf(aes(fill = spend_all) , color = 'gray') + 
  coord_sf(crs = 5070) +
  ggtitle("Spending by county in New York on June 29, 2020") + 
  scale_fill_viridis_c()
```

![](lab_3_problem_set_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

### Describe the map you just made and any interesting facts you can learn from it

There are a lot of missing values. Most seasonally adjusted credit/debit
card spendings relative to January 4-31 2020 in all merchant category
codes (MCC) in New York State are around -0.1 \~ -0.2. Only around 3
counties have a spending change greater than 0.

## Plot time series of ALL spending changes over time (relative to January) for the 5 largest counties in New York State

``` r
NY_spending %>%
  filter(countyname %in% c('Kings', 'Queens', 'New York', 'Suffolk', 'Bronx')) %>%
  ggplot(aes(x = date, y = spend_all, color = countyname)) +
  geom_line() +
  labs(x = "Date", 
       y = 'Spending', 
       color = "County") +
  scale_y_continuous(labels = function(y) format(y, scientific=FALSE))
```

![](lab_3_problem_set_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

### Describe the plot you just made and any interesting facts you can learn from it

The spending remains relatively constant at February and drops
significantly at mid-March. This corresponds to when the COVID-19
started and the quarantine started. The spending gradually started to
recover in April but still remained at a low level. By July, some
counties (such as Bronx and Suffolk) have reached a similar spending
level as before quarantine while some counties (such as Queens) still
have a low spending level.

# Hands-on Task 3: Correlation

## Join the county-level COVID-cases data frame with the spending data frame

You will need to join these data frames based on county ID and date.

``` r
NY_covid_spending <-
  left_join(NY_spending, covid_NY, 
            by = c("date", "countyfips", "countyname")) %>%
  select(countyfips, countyname, new_case_rate, 
         spend_all, date, county_pop2019 = county_pop2019.x)
# just wanted to sort out the information that is going to be used
```

## Estimate the correlation between the NEW case rates and spending changes

``` r
cor.test(NY_covid_spending$new_case_rate, NY_covid_spending$spend_all)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  NY_covid_spending$new_case_rate and NY_covid_spending$spend_all
    ## t = -39.761, df = 6522, p-value < 0.00000000000000022
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.4610370 -0.4219689
    ## sample estimates:
    ##        cor 
    ## -0.4417123

### Interpret the correlation you just estimated (please use simple words to describe the relationship)

The correlation coefficient of -0.44 indicates that there is a moderate
negative association between new case rates and spending change. The
small p-value indicates that the relationship is significant. The higher
the new case rate is, the lower the spending change is.

### Does this correlation estimate tell the same overall story that the time series plots of new case rates and spending changes tell you? Why?

Yes, they tell a similar overall story that new case rate has a negative
effect on spending change. The negative correlation is expected since
the new case rate increases when the spending decreases in the time
series plot. Put it more visually: the two time series graphs are
upside-down. When the new case rate is high, people are less likely to
spend money. When the case rate starts to decrease, people are more
likely to spend money.

## Estimate the correlation between NEW confirmed case COUNTS and spending changes

First, you need to use and repurpose the formula we developed in Lab 3
to estimate case counts from the case rate and the 2019 population size.
\[Case Rate = \frac{NumberOfCases*100,000}{Estimated Population}\]
\[\frac{Case Rate * Estimated Population}{100,000} = NumberOfCases\]

``` r
NY_covid_spending <- NY_covid_spending %>%
  mutate(new_case_count = (new_case_rate * county_pop2019)/100000)
```

Now, you can calculate the correlation between the NEW confirmed case
counts and spending changes

``` r
cor.test(NY_covid_spending$new_case_count, NY_covid_spending$spend_all)
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  NY_covid_spending$new_case_count and NY_covid_spending$spend_all
    ## t = -31.002, df = 6522, p-value < 0.00000000000000022
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.3793465 -0.3370439
    ## sample estimates:
    ##        cor 
    ## -0.3583791

### Interpret the correlation you just estimated (please use simple words to describe the relationship)

There is a moderate negative association (-0.36) between new confirmed
case counts and spending changes. The small p-value also supports that
the relationship is significant. With more new confirmed cases, people
are less likely to spend money.

### Is the correlation between spending and case COUNTS the same as the relationship between spending and case RATES? Why?

While case rate gives a proportion, case count gives a number. The two
correlations are similar as the two correlations both display a negative
association. Because a high case count also means a high case rate (the
two parameters are positively associated), when the two increase, the
spending decreases. On the other hand, the new count case rate may
better represent the pandemic situation in a specific county since it is
based on total population and therefore more representative. This
potentially explains why the correlation between case rates is higher
than the correlation between case counts.
