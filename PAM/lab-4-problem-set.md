Lab 4 Problem Set
================

  - [Submission Instructions](#submission-instructions)
  - [Data Overview](#data-overview)
  - [Problem Set Questions](#problem-set-questions)
      - [1. Read in the crime data using the `renamefrom()` function.
        You will need to create a
        crosswalk.](#read-in-the-crime-data-using-the-renamefrom-function.-you-will-need-to-create-a-crosswalk.)
      - [2. Merge in the demographic data. Examine your variables.
        Correct the three variables that are incorrectly coded. You need
        to determine which variables these are by viewing your data and
        running the checks we learned in lab
        1.](#merge-in-the-demographic-data.-examine-your-variables.-correct-the-three-variables-that-are-incorrectly-coded.-you-need-to-determine-which-variables-these-are-by-viewing-your-data-and-running-the-checks-we-learned-in-lab-1.)
      - [3. Write a null and alternative hypothesis that you can
        feasibly answer with your data (e.g., crime rates (consider
        overall, index, violent, or property) are higher in counties
        with higher proportions of X). Your hypothesis should NOT be
        related to time; we will examine this
        later.](#write-a-null-and-alternative-hypothesis-that-you-can-feasibly-answer-with-your-data-e.g.-crime-rates-consider-overall-index-violent-or-property-are-higher-in-counties-with-higher-proportions-of-x.-your-hypothesis-should-not-be-related-to-time-we-will-examine-this-later.)
      - [4. Run a preliminary correlation for your hypothesis. Report on
        the strength of the relationship, the significance level, and
        whether the correlation supports your null or alternative
        hypothesis. (HINT: If you use a demographic variable that is
        reported as a count, you will need to turn this into a
        proportion. Also consider whether your variable makes sense on
        its
        own).](#run-a-preliminary-correlation-for-your-hypothesis.-report-on-the-strength-of-the-relationship-the-significance-level-and-whether-the-correlation-supports-your-null-or-alternative-hypothesis.-hint-if-you-use-a-demographic-variable-that-is-reported-as-a-count-you-will-need-to-turn-this-into-a-proportion.-also-consider-whether-your-variable-makes-sense-on-its-own.)
      - [5. Run a ttest for your hypothesis. In order to run a ttest,
        your independent variable will need to be binary (or coded as 0
        v 1). Recall we created indicators in lab 1. Write a rationale
        for why you split your variable the way you did. Report the
        means of your outcome for the two groups you created, and the
        significance level from the ttest. Compare your findings here to
        step 4. Speak to similarities and differences between the two
        tests.](#run-a-ttest-for-your-hypothesis.-in-order-to-run-a-ttest-your-independent-variable-will-need-to-be-binary-or-coded-as-0-v-1.-recall-we-created-indicators-in-lab-1.-write-a-rationale-for-why-you-split-your-variable-the-way-you-did.-report-the-means-of-your-outcome-for-the-two-groups-you-created-and-the-significance-level-from-the-ttest.-compare-your-findings-here-to-step-4.-speak-to-similarities-and-differences-between-the-two-tests.)
      - [6. What other variables do you think could explain the
        relationship you found in step 4? Write at least 2 other
        variables you think could attenuate (or weaken) your
        relationship and explain why. If necessary, recode the variables
        in this section. The way you code your variables will help you
        tell your story later on. Finally, thinking back to lab 4 write
        1 sentence about whether it make sense to use factors you use
        factors?](#what-other-variables-do-you-think-could-explain-the-relationship-you-found-in-step-4-write-at-least-2-other-variables-you-think-could-attenuate-or-weaken-your-relationship-and-explain-why.-if-necessary-recode-the-variables-in-this-section.-the-way-you-code-your-variables-will-help-you-tell-your-story-later-on.-finally-thinking-back-to-lab-4-write-1-sentence-about-whether-it-make-sense-to-use-factors-you-use-factors)
          - [Variable 1 - Education:](#variable-1---education)
          - [Variable 2 - Gender:](#variable-2---gender)
          - [Rationale of choosing the
            variables:](#rationale-of-choosing-the-variables)
      - [7. Create a graph/plot/map of your choice that examines your
        hypothesis from step 3/4. Replicate your graph/plot/map but this
        time adding in trends for the different groups you identified in
        step 6. Write 1-2 sentences briefly summarizing what you find.
        (HINT: Think about whether a line graph or a bar chart makes
        more sense for this exercise. Feel free to get creative here.
        You may add in a time dimension if you would like, though it is
        not
        necessary).](#create-a-graphplotmap-of-your-choice-that-examines-your-hypothesis-from-step-34.-replicate-your-graphplotmap-but-this-time-adding-in-trends-for-the-different-groups-you-identified-in-step-6.-write-1-2-sentences-briefly-summarizing-what-you-find.-hint-think-about-whether-a-line-graph-or-a-bar-chart-makes-more-sense-for-this-exercise.-feel-free-to-get-creative-here.-you-may-add-in-a-time-dimension-if-you-would-like-though-it-is-not-necessary.)
      - [8. Run three linear models. The first model should be the
        “naive” model that only examines the relationship between your
        outcome and independent variable (identified in step 4). Your
        second model should be your “control” model where you add in the
        groups you identified in step 6. Your final model is another
        “control” model where you add year to your model (add year by
        itself removing the groups from your second model). Write 3-4
        sentences interpreting the estimates between your naive and
        control models. Pay particular attention to estimates,
        significance, and your r-squared and compare between your
        models. Think hard about what your estimates actually mean. Your
        interpration of the estimates depend on how your outcome
        variable was
        coded.](#run-three-linear-models.-the-first-model-should-be-the-naive-model-that-only-examines-the-relationship-between-your-outcome-and-independent-variable-identified-in-step-4.-your-second-model-should-be-your-control-model-where-you-add-in-the-groups-you-identified-in-step-6.-your-final-model-is-another-control-model-where-you-add-year-to-your-model-add-year-by-itself-removing-the-groups-from-your-second-model.-write-3-4-sentences-interpreting-the-estimates-between-your-naive-and-control-models.-pay-particular-attention-to-estimates-significance-and-your-r-squared-and-compare-between-your-models.-think-hard-about-what-your-estimates-actually-mean.-your-interpration-of-the-estimates-depend-on-how-your-outcome-variable-was-coded.)
      - [9. Visualize your regressions by graphing the residuals from
        both your naive and control models in step 8. Write 3-4 setences
        explaining what the graphs show, paying particular attention to
        the interpretation of your confidence
        intervals.](#visualize-your-regressions-by-graphing-the-residuals-from-both-your-naive-and-control-models-in-step-8.-write-3-4-setences-explaining-what-the-graphs-show-paying-particular-attention-to-the-interpretation-of-your-confidence-intervals.)
      - [10. For a policy leader of your choice, explain your hypothesis
        and why it is important for them to consider. Next summarize
        your findings. Finally, recall that our data represents counties
        in New York State for the years 2016 to 2018. What other data
        would you like in order to better understand your hypotheses
        (e.g., time points, neighborhoods)? How would this data better
        help you answer the question you are interested in? Specifically
        speak to HOW this new data would allow you to isolate the
        relationship you’re interested in. Write 2-3
        paragraphs.](#for-a-policy-leader-of-your-choice-explain-your-hypothesis-and-why-it-is-important-for-them-to-consider.-next-summarize-your-findings.-finally-recall-that-our-data-represents-counties-in-new-york-state-for-the-years-2016-to-2018.-what-other-data-would-you-like-in-order-to-better-understand-your-hypotheses-e.g.-time-points-neighborhoods-how-would-this-data-better-help-you-answer-the-question-you-are-interested-in-specifically-speak-to-how-this-new-data-would-allow-you-to-isolate-the-relationship-youre-interested-in.-write-2-3-paragraphs.)

<br>

<hr>

<br>

# Submission Instructions

Download the lab-four-problem-set.rmd file from GitHub and code your
answers in that file. Rename the file lastname\_firstname\_lab1.md. You
must knit your .rmd as an .md. Upload your problem set through the
Assignments tab in Canvas by July 29th at 12PM. Remember that in an R
Markdown file writing in the white space will be read as text, so you
write responses to your questions in the white space.

# Data Overview

Our data represents crime rates by county in New York from 2016-2018.
Crime rates are reported using three categories: Index, Violent, and
Property Crimes. Data was collected from
<https://www.criminaljustice.ny.gov/crimnet/ojsa/countycrimestats.htm>.
We also have demographic information for each county collected from the
United States Census. Definitions for each variables are below.

Variables:

| Variable                                          | Description                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `gisjoin`                                         | GIS unique id that allows the user to merge data to a county GIS shapefile                                                                                                                                                                                                                                        |
| `year`                                            | Year the data was collected. Census data was collected between 2014-2018 and is presented as a weighted average, but we should think of all demographic data as coming from 2016.                                                                                                                                 |
| `county/countyname`                               | County name                                                                                                                                                                                                                                                                                                       |
| `countya/countfip`                                | County FIPS code                                                                                                                                                                                                                                                                                                  |
| `male`                                            | male represents the total number of individuals who identify as male overall and by the following age groups: under 18, 18 to 34 years of age, 35 to 64 years of age, and 65 or older. The total number of individuals who were surveyed to obtain these statistics are found in sex by age: total population     |
| `female`                                          | female represents the total number of individuals who identify as female overall and by the following age groups: under 18, 18 to 34 years of age, 35 to 64 years of age, and 65 or older. The total number of individuals who were surveyed to obtain these statistics are found in sex by age: total population |
| `race`                                            | Race represents the total number of individuals who identify as white, Black, Asian, American Indian, Nativan Hawaiian or other. The total number of individuals who were surveyed to obtain these statistics are found in Race: total population                                                                 |
| `education`                                       | Education represents the total number of individuals who have achieved a certain level of education as defined by HS degree or less, some college, and college or more. The total number of individuals who were surveyed to obtain these statistics are found in education: total population                     |
| `median household income`                         | The median household income                                                                                                                                                                                                                                                                                       |
| `proportion (un)employed in civilian labor force` | Of the civilian labor force, these are the proportions (0-1) of individuals who are either employed or unemployed. This does not include those serving in the armed forces or those that are not in the civilian labor force (e.g., individuals over 65)                                                          |
| `population`                                      | The total number of indivudals living in the county                                                                                                                                                                                                                                                               |
| `index crime`                                     | Index crimes include all counts of murder and nonnegligent homicide, rape, robbery, aggravated assualt, burglary, motor vehicle theft, larceny-theft, and arson                                                                                                                                                   |
| `violent crime`                                   | Violent crime is defined as an event where an offender or perpetrator uses or threatens to use force upon a victim                                                                                                                                                                                                |
| `property crime`                                  | Property crime is defined as an event where a victim’s property is stolen or destroyed without the use or threat of force against the victim. This is represented as an overall count of occurences and a rate per                                                                                                |
| `new york city`                                   | This is an indicator stating whether the county is in New York City                                                                                                                                                                                                                                               |

# Problem Set Questions

``` r
library(collapse)
```

    ## Warning: package 'collapse' was built under R version 4.0.2

    ## collapse 1.2.1, see ?`collapse-package` or ?`collapse-documentation`

    ## 
    ## Attaching package: 'collapse'

    ## The following object is masked from 'package:stats':
    ## 
    ##     D

``` r
require(doBy)
```

    ## Loading required package: doBy

    ## Warning: package 'doBy' was built under R version 4.0.2

``` r
library(visreg)
```

    ## Warning: package 'visreg' was built under R version 4.0.2

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.0.1

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.1     ✓ dplyr   1.0.0
    ## ✓ tidyr   1.1.0     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## Warning: package 'tidyr' was built under R version 4.0.1

    ## Warning: package 'readr' was built under R version 4.0.1

    ## Warning: package 'forcats' was built under R version 4.0.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter()   masks stats::filter()
    ## x dplyr::lag()      masks stats::lag()
    ## x dplyr::order_by() masks doBy::order_by()

``` r
library(crosswalkr) 
```

    ## Warning: package 'crosswalkr' was built under R version 4.0.2

``` r
library(zoo)
```

    ## Warning: package 'zoo' was built under R version 4.0.2

    ## 
    ## Attaching package: 'zoo'

    ## The following object is masked from 'package:collapse':
    ## 
    ##     is.regular

    ## The following objects are masked from 'package:base':
    ## 
    ##     as.Date, as.Date.numeric

``` r
library(randomForest) 
```

    ## Warning: package 'randomForest' was built under R version 4.0.2

    ## randomForest 4.6-14

    ## Type rfNews() to see new features/changes/bug fixes.

    ## 
    ## Attaching package: 'randomForest'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     margin

``` r
library(readxl)
```

    ## Warning: package 'readxl' was built under R version 4.0.1

## 1\. Read in the crime data using the `renamefrom()` function. You will need to create a crosswalk.

``` r
# load data
d2016 <- read_excel("problem-set-4-data/2016-county-index-rates.xlsx")
d2017 <- read_excel("problem-set-4-data/2017-county-index-rates.xlsx")
d2018 <- read_excel("problem-set-4-data/2018-county-index-rates.xlsx")

# create crosswalk 
c2016 <- colnames(d2016)
c2017 <- colnames(d2017)
c2018 <- colnames(d2018)
VarName <- c("GISJOIN", "Year", "CountyFIPS", "County", "Population", 
             "IC Count", "IC Rate", "VC Count", "VC Rate",
             "PC Count", "PC Rate", "New York City")
write.csv(cbind(VarName, c2016, c2017, c2018), "cw.csv")
cw <- read.csv("cw.csv")

# rename 
df2016 <- renamefrom(d2016, cw, c2016, VarName)
df2017 <- renamefrom(d2017, cw, c2017, VarName)
df2018 <- renamefrom(d2018, cw, c2018, VarName)

# bind 
df <- rbind(df2016, df2017, df2018)
```

## 2\. Merge in the demographic data. Examine your variables. Correct the three variables that are incorrectly coded. You need to determine which variables these are by viewing your data and running the checks we learned in lab 1.

``` r
# load data 
demographic <- read.csv("problem-set-4-data/ny_demographic_census.csv")
# view(demographic)

demographic <- 
  demographic %>% 
  # total race doesn't match 
  mutate(Race..Total.Population = 
           White + Black + American.Indian + Asian + 
           Native.Hawaiian + Other.Race) %>%
  # proportion doesn't make sense 
  mutate(Proportion.Employed.in.Civilian.Labor.Force = 
           ifelse(Proportion.Employed.in.Civilian.Labor.Force 
                  + Proportion.Unemployed.in.Civilian.Labor.Force == 1,
                  Proportion.Employed.in.Civilian.Labor.Force, NA))  %>%
  mutate(Proportion.Unemployed.in.Civilian.Labor.Force = 
           ifelse(Proportion.Employed.in.Civilian.Labor.Force 
                  + Proportion.Unemployed.in.Civilian.Labor.Force == 1,
                  Proportion.Unemployed.in.Civilian.Labor.Force, NA))

# merge
df <- left_join(df, demographic, by = "GISJOIN")
# delete useless columns 
df <- df[ , -which(names(df) %in% c("COUNTY","COUNTYA"))]
```

## 3\. Write a null and alternative hypothesis that you can feasibly answer with your data (e.g., crime rates (consider overall, index, violent, or property) are higher in counties with higher proportions of X). Your hypothesis should NOT be related to time; we will examine this later.

Null Hypothesis:  
There is no correlation between property crime rates and median
household income in the counties in New York Alternative Hypothesis:  
Property crime rates are higher in New York counties with lower median
household income

## 4\. Run a preliminary correlation for your hypothesis. Report on the strength of the relationship, the significance level, and whether the correlation supports your null or alternative hypothesis. (HINT: If you use a demographic variable that is reported as a count, you will need to turn this into a proportion. Also consider whether your variable makes sense on its own).

Because the p-value is small (p = 0.0083 \< 0.01), there is a good
evidence to reject the null hypothesis and conclude that there is an
association between property crime rate and medium household income. The
correlation coefficient of -0.19 suggests that there is a weak negative
relationship between property crime rate and medium household income:
the lower the median household income of a county is, the higher the
property violence rate is (though the correlation is small).

``` r
cor.test(df$Median.Household.Income, df$`PC Rate`, method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  df$Median.Household.Income and df$`PC Rate`
    ## t = -2.6672, df = 184, p-value = 0.00833
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.32771877 -0.05045809
    ## sample estimates:
    ##        cor 
    ## -0.1929368

## 5\. Run a ttest for your hypothesis. In order to run a ttest, your independent variable will need to be binary (or coded as 0 v 1). Recall we created indicators in lab 1. Write a rationale for why you split your variable the way you did. Report the means of your outcome for the two groups you created, and the significance level from the ttest. Compare your findings here to step 4. Speak to similarities and differences between the two tests.

I calculated the mean median household income in New York and divided
median household income into either “below mean income” or “above mean
income”. Mean income is a reasonable dividing line since it reflects the
overall income level in the state and divides the incomes roughly
evenly. Counties with a median household income above mean has a
property crime rate of 1354.655, which is 55.69 points below counties
with a median household income below mean (1413.192 ). However, the
difference in mean is not significant according to the large p-value
(0.47 \> 0.1). While Pearson’s product-moment correlation indicates a
weak yet significant correlation between median household income and
property crime rates, the student’s t-test suggests that there is no
significant difference as according to whether the median household
income is below or above the mean.

``` r
incomeMean <- mean(df$Median.Household.Income)
df$compareIncome <- 
  ifelse(df$Median.Household.Income > incomeMean, TRUE, FALSE)
df %>% group_by(compareIncome) %>% summarise(rate = mean(`PC Rate`))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 2 x 2
    ##   compareIncome  rate
    ##   <lgl>         <dbl>
    ## 1 FALSE         1413.
    ## 2 TRUE          1355.

``` r
pairwise.t.test(df$`PC Rate`, df$compareIncome,
                p.adjust.method = "BH")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  df$`PC Rate` and df$compareIncome 
    ## 
    ##      FALSE
    ## TRUE 0.47 
    ## 
    ## P value adjustment method: BH

``` r
# I also tried to split according to quantile
# quantile(df$Median.Household.Income)
# df <- df %>%
#  mutate(compareIncome = case_when(
#    (Median.Household.Income >= 3808 & Median.Household.Income <=52268) ~ 0,
#    (Median.Household.Income > 52268 & Median.Household.Income <=55890) ~ 1,
#    (Median.Household.Income > 55890 & Median.Household.Income <=63348) ~ 2,
#    (Median.Household.Income > 63348 & Median.Household.Income <=111240) ~ 3))
# df %>% group_by(compareIncome) %>% summarise(rate = mean(`PC Rate`))
# pairwise.t.test(df$`PC Rate`, df$compareIncome,
#                p.adjust.method = "BH")
```

## 6\. What other variables do you think could explain the relationship you found in step 4? Write at least 2 other variables you think could attenuate (or weaken) your relationship and explain why. If necessary, recode the variables in this section. The way you code your variables will help you tell your story later on. Finally, thinking back to lab 4 write 1 sentence about whether it make sense to use factors you use factors?

#### Variable 1 - Education:

Another factor that might influence property crime rate is education
level. High education level also might be a confounding variable in the
relationship between income and property crime rate since high income is
associated with high education level. As shown by the correlation test
below, there is a significant (p-value \< 2.2e-16), strong, positive
correlation between the “college or more” proportion and median income
level. In addition, the student t-test examines the difference in PC
rate between counties with “college or more” education proportion above
mean level and counties with “college or more” proportion below mean
level. The p-value of 0.0049 (\< 0.01) is a good evidence that the
difference is significant.

``` r
# Correlation test: 
# high education level is defined by the proportion of "college or more" in a given county 
df$HighEdu.Fraction <- df$College.or.More/df$Education..Total.Population
cor.test(df$Median.Household.Income, df$HighEdu.Fraction, method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  df$Median.Household.Income and df$HighEdu.Fraction
    ## t = 13.769, df = 184, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.6334126 0.7766468
    ## sample estimates:
    ##       cor 
    ## 0.7123701

``` r
# T-test: 
HighEdu.Fraction.Mean <- mean(df$HighEdu.Fraction)
df$compareHighEdu <- 
  ifelse(df$HighEdu.Fraction > HighEdu.Fraction.Mean, TRUE, FALSE)
df %>% group_by(compareHighEdu) %>% summarise(rate = mean(`PC Rate`))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 2 x 2
    ##   compareHighEdu  rate
    ##   <lgl>          <dbl>
    ## 1 FALSE          1311.
    ## 2 TRUE           1522.

``` r
pairwise.t.test(df$`PC Rate`, df$compareHighEdu,
                p.adjust.method = "BH")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  df$`PC Rate` and df$compareHighEdu 
    ## 
    ##      FALSE 
    ## TRUE 0.0049
    ## 
    ## P value adjustment method: BH

#### Variable 2 - Gender:

Running both the correlation test and t-test, it is reasonable to
conclude that counties with higher female population have a higher
property crime rate. In the correlation tests for male and female versus
PC rate, both correlations are significant indicated by the small
p-value (p-value = 0.000001148 \< 0.001), it is also interesting that
the correlation coefficient between male proportion and PC rate is
-0.348, opposite from 0.348, which is the correlation coefficient
between female proportion and PC rate. The T-test indicates that the PC
Rate in counties with higher female population proportion is higher than
PC Rate in counties with higher male population proportion.

``` r
# Male correlation test: 
df$male.Fraction <- df$Male..Total.Population/df$Sex.by.Age..Total.Population
cor.test(df$male.Fraction, df$`PC Rate`, method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  df$male.Fraction and df$`PC Rate`
    ## t = -5.0324, df = 184, p-value = 1.148e-06
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.4682703 -0.2146903
    ## sample estimates:
    ##        cor 
    ## -0.3478255

``` r
# Female correlation test: 
df$female.Fraction <- df$Female..Total.Population/df$Sex.by.Age..Total.Population
cor.test(df$female.Fraction, df$`PC Rate`, method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  df$female.Fraction and df$`PC Rate`
    ## t = 5.0324, df = 184, p-value = 1.148e-06
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.2146903 0.4682703
    ## sample estimates:
    ##       cor 
    ## 0.3478255

``` r
# T test: 
df$isFemale <- 
  ifelse(df$female.Fraction > df$male.Fraction, TRUE, FALSE)
df %>% group_by(isFemale) %>% summarise(rate = mean(`PC Rate`))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 2 x 2
    ##   isFemale  rate
    ##   <lgl>    <dbl>
    ## 1 FALSE    1191.
    ## 2 TRUE     1494.

``` r
pairwise.t.test(df$`PC Rate`, df$isFemale,
                p.adjust.method = "BH")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  df$`PC Rate` and df$isFemale 
    ## 
    ##      FALSE
    ## TRUE 1e-04
    ## 
    ## P value adjustment method: BH

#### Rationale of choosing the variables:

  - Poverty, education level, and gender are all factors that might
    influence crime rate according to various news sources and online
    reports.  
  - Medium Household Income: [Correlation between crime rate and
    poverty](https://www.arcgis.com/apps/MapJournal/index.html?appid=5508484140a84023a1e2d8b080e14d0a)
  - High Education Level: [Education and Public
    Safety](http://www.justicepolicy.org/images/upload/07-08_rep_educationandpublicsafety_ps-ac.pdf)  
  - Gender: [An analysis of gender differences in property crime arrest
    rates](https://digitalcommons.lsu.edu/gradschool_dissertations/1128/)
  - I thought of using employment proportion as a variable but most of
    the data in the column are invalid

## 7\. Create a graph/plot/map of your choice that examines your hypothesis from step 3/4. Replicate your graph/plot/map but this time adding in trends for the different groups you identified in step 6. Write 1-2 sentences briefly summarizing what you find. (HINT: Think about whether a line graph or a bar chart makes more sense for this exercise. Feel free to get creative here. You may add in a time dimension if you would like, though it is not necessary).

For PC Rate versus Median Household Income graph:  
PC Rate remains roughly constant for counties with median household
income below mean level. There is a decreasing trend in PC Rate for
counties with median household income above mean level.  
For PC Rate versus High Education Level graph:  
The y-intercept for counties with higher education proportion above mean
is higher. This is contrary to t-test in question 6, which is
interesting.  
For PC Rate versus Female population proportion:  
There is a moderate positive correlation between female population
proportion and property crime rate.

``` r
options(scipen=10000)
ggplot(df, 
       aes(x=Median.Household.Income, y=`PC Rate`, color = compareIncome)) + 
  geom_point() +
  geom_smooth(method = "lm")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](lab-4-problem-set_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
ggplot(df, 
       aes(x=HighEdu.Fraction, y=`PC Rate`, color = compareHighEdu)) + 
  geom_point() +
  geom_smooth(method = "lm")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](lab-4-problem-set_files/figure-gfm/unnamed-chunk-9-2.png)<!-- -->

``` r
ggplot(df, 
       aes(x=female.Fraction, y=`PC Rate`, color = isFemale)) + 
  geom_point() +
  geom_smooth(method = "lm")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](lab-4-problem-set_files/figure-gfm/unnamed-chunk-9-3.png)<!-- -->

## 8\. Run three linear models. The first model should be the “naive” model that only examines the relationship between your outcome and independent variable (identified in step 4). Your second model should be your “control” model where you add in the groups you identified in step 6. Your final model is another “control” model where you add year to your model (add year by itself removing the groups from your second model). Write 3-4 sentences interpreting the estimates between your naive and control models. Pay particular attention to estimates, significance, and your r-squared and compare between your models. Think hard about what your estimates actually mean. Your interpration of the estimates depend on how your outcome variable was coded.

In the naive model, the estimate is 1413.19, and having a higher median
household income will decrease the estimated PC rate by 58.54. However,
the R squared value of 0.002789 indicates that only 0.27% of the changes
are predicted by the regression, which is not very great. In addition,
the p-value of 0.474 (\> 0.1) indicates that the relationship between
household income level and property crime rate is largely due to
chance.  
Controlling for the confounding variables, the estimate is -4887.32. The
squared residual value of 0.1654 suggests that the control model is
performing better than the naive model. In the control group, household
income has a stronger influence on PC rate (-301.65). Having a higher
female population in a county has the strongest influence on PC rate,
increasing the rate by around 12175.25. The p-values for both household
income (p = 0.002164 \< 0.01) and female population (p = 0.0000187
\<0.001) are significant, while the correlation between high education
level and property crime rate (p = 0.080321 \> 0.05) is due to chance.  
Controlling for year gives a baseline of 215205.64. In this case, a
higher income level only decreases the property crime rate by 58.54,
with a p-value of 0.4686 \> 0.05 indicating there is no significant
correlation. Year does have a significant influence on property crime
rate as suggested by the p-value of 0.0190 \< 0.05: property crime rate
decreases over year (-106.00). While the squared residual is still
relatively low (0.03238), it is better than the naive model.

``` r
# Naive Model 
naive_lm <- lm(`PC Rate` ~ compareIncome, data = df)
summary(naive_lm) 
```

    ## 
    ## Call:
    ## lm(formula = `PC Rate` ~ compareIncome, data = df)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1157.79  -362.49   -56.01   296.92  1242.98 
    ## 
    ## Coefficients:
    ##                   Estimate Std. Error t value            Pr(>|t|)    
    ## (Intercept)        1413.19      43.97  32.143 <0.0000000000000002 ***
    ## compareIncomeTRUE   -58.54      81.60  -0.717               0.474    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 505.1 on 184 degrees of freedom
    ## Multiple R-squared:  0.002789,   Adjusted R-squared:  -0.00263 
    ## F-statistic: 0.5146 on 1 and 184 DF,  p-value: 0.474

``` r
# Control Model 
control_lm <- lm(`PC Rate` ~ 
                   compareIncome + 
                   female.Fraction + 
                   HighEdu.Fraction, 
                 data = df)
summary(control_lm) 
```

    ## 
    ## Call:
    ## lm(formula = `PC Rate` ~ compareIncome + female.Fraction + HighEdu.Fraction, 
    ##     data = df)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1161.20  -351.32   -39.62   317.92  1253.69 
    ## 
    ## Coefficients:
    ##                   Estimate Std. Error t value  Pr(>|t|)    
    ## (Intercept)       -4887.32    1334.56  -3.662  0.000328 ***
    ## compareIncomeTRUE  -301.65      96.95  -3.111  0.002164 ** 
    ## female.Fraction   12175.25    2769.91   4.396 0.0000187 ***
    ## HighEdu.Fraction    920.46     523.40   1.759  0.080321 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 464.7 on 182 degrees of freedom
    ## Multiple R-squared:  0.1654, Adjusted R-squared:  0.1516 
    ## F-statistic: 12.02 on 3 and 182 DF,  p-value: 0.0000003236

``` r
# Control for Year
control_year_lm <- lm(`PC Rate` ~ 
                   compareIncome + Year,data = df)
summary(control_year_lm) 
```

    ## 
    ## Call:
    ## lm(formula = `PC Rate` ~ compareIncome + Year, data = df)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1109.42  -369.31   -39.35   262.78  1301.95 
    ## 
    ## Coefficients:
    ##                    Estimate Std. Error t value Pr(>|t|)  
    ## (Intercept)       215205.64   90373.48   2.381   0.0183 *
    ## compareIncomeTRUE    -58.54      80.60  -0.726   0.4686  
    ## Year                -106.00      44.81  -2.366   0.0190 *
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 498.9 on 183 degrees of freedom
    ## Multiple R-squared:  0.03238,    Adjusted R-squared:  0.0218 
    ## F-statistic: 3.062 on 2 and 183 DF,  p-value: 0.0492

## 9\. Visualize your regressions by graphing the residuals from both your naive and control models in step 8. Write 3-4 setences explaining what the graphs show, paying particular attention to the interpretation of your confidence intervals.

All of the three regression graphs show that with a higher median
household income level, property crime rate decreases. For all three
models, the error bar towards the two extremes (when the income is at
lowest level and when the income is at highest level) is larger, there
is a lower confidence likely due to the small sample sizes at those
values. While both the naive model and control-for-year model presents a
weak negative correlation between county income level and PC rate, the
negative trend is stronger when female population and education level
are under control.

``` r
visreg(naive_lm, "compareIncome")
```

![](lab-4-problem-set_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
visreg(control_lm, "compareIncome")
```

![](lab-4-problem-set_files/figure-gfm/unnamed-chunk-11-2.png)<!-- -->

``` r
visreg(control_year_lm, "compareIncome")
```

![](lab-4-problem-set_files/figure-gfm/unnamed-chunk-11-3.png)<!-- -->

## 10\. For a policy leader of your choice, explain your hypothesis and why it is important for them to consider. Next summarize your findings. Finally, recall that our data represents counties in New York State for the years 2016 to 2018. What other data would you like in order to better understand your hypotheses (e.g., time points, neighborhoods)? How would this data better help you answer the question you are interested in? Specifically speak to HOW this new data would allow you to isolate the relationship you’re interested in. Write 2-3 paragraphs.

The hypothesis was “property crime rates are higher in New York counties
with lower median household income”. It is important to lower the
property crime rate so that citizens feel secure about their properties
living in a county. According to my analysis, it is true that median
household income in a county can influence property crime rate but the
association is negligible; instead, a stronger influencer of property
crime rate in a county is the female population proportion (which I am
not entirely sure why).  
To better test the relationship between income level and property crime
rate, a possible data set to investigate is a data set of several
counties (maybe from other states too since we need a larger sample
size) with similar male and female proportion, which will isolate income
level from gender, enabling us to directly associate it with property
crime rate.  
Another aspects is regarding individual household income level’s
association with individual’s likelihood of committing a property crime.
Further analysis should be conducted over a data set which contains each
criminal’s income level. While median household income of a county may
only reflects on the county’s general consumption level and living
standard, individual income level better reflects whether the individual
needs money or not. Therefore, such data set can present the variance
more clearly within a county/state.
