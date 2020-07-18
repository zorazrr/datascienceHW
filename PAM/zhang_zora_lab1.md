Lab 1 Problem Set
================

  - [Submission Instructions:](#submission-instructions)
  - [Part A: Reviewing the basics](#part-a-reviewing-the-basics)
      - [1. Import `county_outcomes.csv`. You should have 154 variables
        and 2,819
        observations](#import-county_outcomes.csv.-you-should-have-154-variables-and-2819-observations)
      - [2. View your data by running at least 2 functions. Write 3-5
        things you looked for to check your dataset to make sure it is
        ready for
        analysis](#view-your-data-by-running-at-least-2-functions.-write-3-5-things-you-looked-for-to-check-your-dataset-to-make-sure-it-is-ready-for-analysis)
      - [3. Compare mean income ranks between black females and white
        females for all counties in the United States (use
        `kfr_black_female_mean` and `kfr_white_female_mean`). Write 1-2
        sentences summarizing your finding. HINT: your dataset
        represents the United States. Therefore, when we ask you to
        compare the mean for all counties in the United States, we’re
        asking you to find the average for the entire dataset without
        subsetting.)](#compare-mean-income-ranks-between-black-females-and-white-females-for-all-counties-in-the-united-states-use-kfr_black_female_mean-and-kfr_white_female_mean.-write-1-2-sentences-summarizing-your-finding.-hint-your-dataset-represents-the-united-states.-therefore-when-we-ask-you-to-compare-the-mean-for-all-counties-in-the-united-states-were-asking-you-to-find-the-average-for-the-entire-dataset-without-subsetting.)
      - [4. Run a correlation between any two outcomes you would like
        (e.g. `kfr_black_male_mean` and `coll_black_male_mean`). Test
        for significance. Write 1-2 sentences summarizing your
        finding.](#run-a-correlation-between-any-two-outcomes-you-would-like-e.g.-kfr_black_male_mean-and-coll_black_male_mean.-test-for-significance.-write-1-2-sentences-summarizing-your-finding.)
      - [5. Next, run another correlation on the same outcome for a
        different group (e.g., black females). Write 1-2 sentences
        comparing your finding here to what you found in question
        4.](#next-run-another-correlation-on-the-same-outcome-for-a-different-group-e.g.-black-females.-write-1-2-sentences-comparing-your-finding-here-to-what-you-found-in-question-4.)
      - [6. Generate a new variable that is the national average of
        `kfr_white_female_mean` and call it `kfr_white_female_us_mean`.
        Store the new variable in the
        dataset.](#generate-a-new-variable-that-is-the-national-average-of-kfr_white_female_mean-and-call-it-kfr_white_female_us_mean.-store-the-new-variable-in-the-dataset.)
      - [7. Create an indicator variable that evaluates whether the mean
        income rank for white women in a county (hint: recall that every
        observation or row is a unique county) is below or above the
        United States average (hint: use what you created in question
        6). Write 1-2 sentences explaining your
        findings.](#create-an-indicator-variable-that-evaluates-whether-the-mean-income-rank-for-white-women-in-a-county-hint-recall-that-every-observation-or-row-is-a-unique-county-is-below-or-above-the-united-states-average-hint-use-what-you-created-in-question-6.-write-1-2-sentences-explaining-your-findings.)
      - [8. Summarize your new variable by reporting how many
        observations are equal to 0 or 1 (i.e., how many counties are
        below or above the national
        average).](#summarize-your-new-variable-by-reporting-how-many-observations-are-equal-to-0-or-1-i.e.-how-many-counties-are-below-or-above-the-national-average.)
      - [9. Merge `cty_covariates.csv` with
        `county_outcomes.csv`](#merge-cty_covariates.csv-with-county_outcomes.csv)
  - [Part B: Analyzing the Opportunity Insights
    data](#part-b-analyzing-the-opportunity-insights-data)
      - [1. Using what you’ve learned, examine differences in outcomes
        (e.g., household income, fraction working) by group (e.g,
        female/male or black/white) and explain your findings in 3-4
        sentences.](#using-what-youve-learned-examine-differences-in-outcomes-e.g.-household-income-fraction-working-by-group-e.g-femalemale-or-blackwhite-and-explain-your-findings-in-3-4-sentences.)
      - [2. How does the probability of reaching the top 1% of the
        national household income distribution (`kfr_top01`) differ by
        gender in a county of your choice. How does this compare to the
        national average? Explain your findings in 3-4
        sentences.](#how-does-the-probability-of-reaching-the-top-1-of-the-national-household-income-distribution-kfr_top01-differ-by-gender-in-a-county-of-your-choice.-how-does-this-compare-to-the-national-average-explain-your-findings-in-3-4-sentences.)
      - [3. Next, repeat question 2 but looking now for patterns by
        race. Explain what you find in 3-4
        sentences?](#next-repeat-question-2-but-looking-now-for-patterns-by-race.-explain-what-you-find-in-3-4-sentences)
  - [Part C: Sketching out your
    project](#part-c-sketching-out-your-project)
      - [1. Limiting your answer to either race or gender, are there any
        other outcomes that might help explain the relationship you
        explored in Section B Question 2 or 3 (e.g., do you think
        `kfr_top01_gender` or `kfr_top01_race` are correlated with other
        outcomes)? Read over all of the variables in the dataset and
        provide an intuitive explanation for why you think another
        outcome could be correlated or related to upward mobility by
        race or gender. Don’t run any code for this question; just think
        about the relationship. Please explain your hypothesis in 3-4
        sentences.](#limiting-your-answer-to-either-race-or-gender-are-there-any-other-outcomes-that-might-help-explain-the-relationship-you-explored-in-section-b-question-2-or-3-e.g.-do-you-think-kfr_top01_gender-or-kfr_top01_race-are-correlated-with-other-outcomes-read-over-all-of-the-variables-in-the-dataset-and-provide-an-intuitive-explanation-for-why-you-think-another-outcome-could-be-correlated-or-related-to-upward-mobility-by-race-or-gender.-dont-run-any-code-for-this-question-just-think-about-the-relationship.-please-explain-your-hypothesis-in-3-4-sentences.)
      - [2. Using the hypothesis you developed in Section C Question 1,
        provide correlational evidence to test your hypothesis. You are
        welcome to use outside data that are not included in
        `country_outcomes.csv`, but this is not required. The goal of
        this question is to understand what might explain the variation
        in upward mobility for certain groups of
        children.](#using-the-hypothesis-you-developed-in-section-c-question-1-provide-correlational-evidence-to-test-your-hypothesis.-you-are-welcome-to-use-outside-data-that-are-not-included-in-country_outcomes.csv-but-this-is-not-required.-the-goal-of-this-question-is-to-understand-what-might-explain-the-variation-in-upward-mobility-for-certain-groups-of-children.)
      - [3. Please consider the county you chose to examine in Section B
        and think about the mayor of that county. Identify one or two
        key lessons or takeaways that you might discuss with them about
        the determinants of economic opportunity (or the potential
        factors that are associated with individuals probability of
        reaching the top 1% of the national household income
        distribution). Mention any important caveats to your conclusions
        or any additional analyses you might want to conduct to prove
        your
        findings.](#please-consider-the-county-you-chose-to-examine-in-section-b-and-think-about-the-mayor-of-that-county.-identify-one-or-two-key-lessons-or-takeaways-that-you-might-discuss-with-them-about-the-determinants-of-economic-opportunity-or-the-potential-factors-that-are-associated-with-individuals-probability-of-reaching-the-top-1-of-the-national-household-income-distribution.-mention-any-important-caveats-to-your-conclusions-or-any-additional-analyses-you-might-want-to-conduct-to-prove-your-findings.)

<br>

<hr>

<br>

# Submission Instructions:

Download the lab-one-problem-set.rmd file from GitHub and code your
answers in that file. Rename the file netid\_ps1 and save as a .rmd.
Upload your problem set through the Assignments tab in Canvas by July
16th at 12PM. Remember that in an R Markdown file writing in the white
space will be read as text, so you write responses to your questions in
the white space.

# Part A: Reviewing the basics

The dataset we are working for this assignment is composed of a series
of outcomes for black females, black males, white females, and white
males by United States county. You will be asked to import and view the
data, as well as run a series of summary statistics to examine
relationships between these variables. Every variable will take two
forms: `outcome_race_gender_n`, which provides the number of
observations in that category, and `outcome_race_gender_mean`, which is
the average of that outcome for that specific group.

NOTE: the use of black/white, male/female is NOT inclusive of all of
races and genders. We limit the analysis to only these groups because of
sample size limitations and current limitations in the collection of
data. Additionally, we thank Opportunity Insights for access to their
class materials and datasets, which this assignment is based on.

Variables:

| Variable    | Description                                                                                                                                                                                                                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `kfr`       | Mean percentile rank (relative to other children born in the same year) in the national distribution of household income measured as mean earnings in 2014-15.                                                                                                                                   |
| `married`   | Fraction of children who file their federal income tax return as “married filing jointly” or “married filing separate” in 2015                                                                                                                                                                   |
| `has_dad`   | Fraction of children who have a male claimer in the year they are linked to parents                                                                                                                                                                                                              |
| `has_mom`   | Fraction of children who have a female claimer in the year they are linked to parents                                                                                                                                                                                                            |
| `two_par`   | Fraction of children claimed by two people in the year they are linked to parents                                                                                                                                                                                                                |
| `teenbrth`  | Fraction of women who grew up in the given tract who ever claimed a child who was born when they were between the ages of 13 and 19 as a dependent at any point                                                                                                                                  |
| `working`   | Fraction of children with positive W-2 earnings in 2015                                                                                                                                                                                                                                          |
| `proginc`   | Fraction of children who receive public assistance income (among children who received the ACS at age 30+)                                                                                                                                                                                       |
| `coll`      | Fraction of children who have a four year college degree (among children who received ACS or 2000 Census long form at age 25+)                                                                                                                                                                   |
| `grad`      | Fraction of children who have a graduate degree (among children who received the ACS or the 2000 long form at age 30+)                                                                                                                                                                           |
| `kfr_top01` | Probability of reaching the top 1% of the national household income distribution (among children born in the same year) in 2014-15                                                                                                                                                               |
| `lpov_nbh`  | Fraction children who grew up in a given tract and end up living in a tract with a poverty rate of less than 10% (according to tract-level Census 2000 data) in adulthood. Tracts where children live as adults are defined as the tract of the last non-missing address observed on tax returns |
| `staytract` | Fraction of individuals who live in one of their childhood Census tracts in adulthood                                                                                                                                                                                                            |
| `staycz`    | Fraction of children who live in one of their childhood commuting zones in adulthood                                                                                                                                                                                                             |
| `stayhome`  | Fraction of children who live at the same address as their parents in 2015                                                                                                                                                                                                                       |

## 1\. Import `county_outcomes.csv`. You should have 154 variables and 2,819 observations

> (1/1): Good

``` r
# I didn't set working directory in the coding blocks here because it was constantly giving me warnings
data <- read.csv("~/Desktop/PAM2070/lab-1-master/county_outcomes.csv")
```

## 2\. View your data by running at least 2 functions. Write 3-5 things you looked for to check your dataset to make sure it is ready for analysis

> (1/1): Good

  - Checked the lab1 dictionary to understand what each column name
    means  
  - There are some missing values  
  - The data type for each column matches  
  - There are no special characters

<!-- end list -->

``` r
head(data)
```

``` r
tail(data)
```

``` r
sapply(X = data, FUN = function(x) sum(is.na(x)))
```


## 3\. Compare mean income ranks between black females and white females for all counties in the United States (use `kfr_black_female_mean` and `kfr_white_female_mean`). Write 1-2 sentences summarizing your finding. HINT: your dataset represents the United States. Therefore, when we ask you to compare the mean for all counties in the United States, we’re asking you to find the average for the entire dataset without subsetting.)

> (3/3): Good 

  - In the US, the mean of the counties’ mean income ranks of white
    female is higher than that of black female.

<!-- end list -->

``` r
mean(data$kfr_black_female_mean, na.rm = TRUE)
```

    ## [1] 0.3745849

``` r
mean(data$kfr_white_female_mean, na.rm = TRUE)
```

    ## [1] 0.5540307

``` r
print("We probably should account for n ↓↓↓")
```

    ## [1] "We probably should account for n ↓↓↓"

``` r
sum (data$kfr_black_female_mean * data$kfr_black_female_n, na.rm = TRUE)/
  sum(data$kfr_black_female_n, na.rm = TRUE)
```

    ## [1] 0.3785796

``` r
sum(data$kfr_white_female_mean * data$kfr_white_female_n, na.rm = TRUE)/
  sum(data$kfr_white_female_n, na.rm = TRUE)
```

    ## [1] 0.5763125

## 4\. Run a correlation between any two outcomes you would like (e.g. `kfr_black_male_mean` and `coll_black_male_mean`). Test for significance. Write 1-2 sentences summarizing your finding.

> (3/3): Excellent 

  - Because the p-value is small (p-value \< 2.2e-16), we are able to
    reject the null hypothesis and conclude that there is a significant
    correlation between the fraction of black male who have a four year
    college degree and mean percentile rank in the national distribution
    of household income for black males.  
  - Correlation coefficient of 0.51 indicates a moderate positive
    correlation: the higher the fraction is in a county, the higher the
    mean percentile rank is.

<!-- end list -->

``` r
cor.test(data$coll_black_male_mean, 
         data$kfr_black_male_mean,
         method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data$coll_black_male_mean and data$kfr_black_male_mean
    ## t = 16.162, df = 726, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.458869 0.565893
    ## sample estimates:
    ##       cor 
    ## 0.5143811

## 5\. Next, run another correlation on the same outcome for a different group (e.g., black females). Write 1-2 sentences comparing your finding here to what you found in question 4.

> (3/3): Excellent 

  - The p-value is also very small (p-value \< 2.2e-16), we are able to
    reject the null hypothesis and conclude that there is a significant
    association between the fraction of black females who went to
    college and mean percentile rank in the national distribution of
    household income for black females.  
  - The correlation coefficient of 0.64 is higher comparing to the
    correlation coefficient from question 4, indicating that, in the US
    counties, the positive association between college degree and income
    rank for black females is stronger than that of black males.

<!-- end list -->

``` r
cor.test(data$coll_black_female_mean, 
         data$kfr_black_female_mean,
         method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data$coll_black_female_mean and data$kfr_black_female_mean
    ## t = 22.954, df = 771, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.5932812 0.6772296
    ## sample estimates:
    ##       cor 
    ## 0.6371412

## 6\. Generate a new variable that is the national average of `kfr_white_female_mean` and call it `kfr_white_female_us_mean`. Store the new variable in the dataset.

> (3/3): Good

``` r
print(mean(data$kfr_white_female_mean, na.rm = TRUE))
```

    ## [1] 0.5540307

``` r
data$kfr_white_female_us_mean <- mean(data$kfr_white_female_mean, na.rm = TRUE)
```

## 7\. Create an indicator variable that evaluates whether the mean income rank for white women in a county (hint: recall that every observation or row is a unique county) is below or above the United States average (hint: use what you created in question 6). Write 1-2 sentences explaining your findings.

> (3/3): Good

  - The national average of `kfr_white_female_mean` is at 0.554, which
    is roughly in the middle and normal. Therefore, it is reasonable to
    infer that in question 8, the answer is roughly half-half.

<!-- end list -->

``` r
data$kfr_white_female_above_mean <- 
  (data$kfr_white_female_mean > data$kfr_white_female_us_mean)
```

## 8\. Summarize your new variable by reporting how many observations are equal to 0 or 1 (i.e., how many counties are below or above the national average).

> (3/3): Good

``` r
print(paste("Below average:", 
            length(which(data$kfr_white_female_above_mean == FALSE))))
```

    ## [1] "Below average: 1467"

``` r
print(paste("Above average:", 
            length(which(data$kfr_white_female_above_mean == TRUE))))
```

    ## [1] "Above average: 1311"

## 9\. Merge `cty_covariates.csv` with `county_outcomes.csv`

> (3/3): Good

Please answer: \* What variable did you merge on? + state and county  
\* How did you determine whether your merge was successful? + In the new
merged dataset, there are 3221 obs of 187 variables, which indicates a
combination of cty\_covariates (2819 obs of 156 variables) and
county\_outcomes (3221 obs of 35 variables)

``` r
data2 <- read.csv("~/Desktop/PAM2070/lab-1-master/cty_covariates.csv")
merged <- merge(data, data2, all = TRUE)
```

<br>

<hr>

<br>

# Part B: Analyzing the Opportunity Insights data

Now we are going to ask you to use your new data skills to answer some
higher order questions. You can do this\! Read the questions and think
about how to apply the tools you’ve learned to answer them. Please use
the “county\_outcomes.csv” for this section. You will have the
opportunity to use your merged dataset in section 3, if you would like
to.

## 1\. Using what you’ve learned, examine differences in outcomes (e.g., household income, fraction working) by group (e.g, female/male or black/white) and explain your findings in 3-4 sentences.

HINT: you can examine whatever differences you would like, such as
differences in mean, etc.

> (4/4): Good

  - The explanation comes after this chunk with the data frame

<!-- end list -->

``` r
# Total fraction of black females and males working 
bworking <- 
  (sum(data$working_black_female_mean 
    * data$working_black_female_n
    , na.rm = TRUE) + 
  sum(data$working_black_male_mean 
    * data$working_black_male_n
    , na.rm = TRUE))/ 
  (sum(data$working_black_female_n
      , na.rm = TRUE) + 
  sum(data$working_black_male_n
      , na.rm = TRUE))
# Total fraction of white females and males working 
wworking <- 
(sum(data$working_white_female_mean 
    * data$working_white_female_n
    , na.rm = TRUE) + 
  sum(data$working_white_male_mean 
    * data$working_white_male_n
    , na.rm = TRUE))/ 
  (sum(data$working_white_female_n
      , na.rm = TRUE) + 
  sum(data$working_white_male_n
      , na.rm = TRUE))
# Total fraction of black females and males earning a graduate degree
bgraduate <- 
(sum(data$grad_black_female_mean 
    * data$grad_black_female_n
    , na.rm = TRUE) + 
  sum(data$grad_black_male_mean 
    * data$grad_black_male_n
    , na.rm = TRUE))/ 
  (sum(data$grad_black_female_n
      , na.rm = TRUE) + 
  sum(data$grad_black_male_n
      , na.rm = TRUE))
# Total fraction of white females and males earning a graduate degree
wgraduate <-
(sum(data$grad_white_female_mean 
    * data$grad_white_female_n
    , na.rm = TRUE) + 
  sum(data$grad_white_male_mean 
    * data$grad_white_male_n
    , na.rm = TRUE))/ 
  (sum(data$grad_white_female_n
      , na.rm = TRUE) + 
  sum(data$grad_white_male_n
      , na.rm = TRUE))
# Mean probability of black females and males reaching top 20% income
btop <-
(sum(data$kfr_top20_black_female_mean 
    * data$kfr_top20_black_female_n 
    , na.rm = TRUE) + 
  sum(data$kfr_top20_black_male_mean 
    * data$kfr_top20_black_male_n
    , na.rm = TRUE))/ 
  (sum(data$kfr_top20_black_female_n 
      , na.rm = TRUE) + 
  sum(data$kfr_top20_black_male_n
      , na.rm = TRUE))
# Mean probability of white females and males reaching top 20% income
wtop <-
(sum(data$kfr_top20_white_female_mean 
    * data$kfr_top20_white_female_n 
    , na.rm = TRUE) + 
  sum(data$kfr_top20_white_male_mean 
    * data$kfr_top20_white_male_n
    , na.rm = TRUE))/ 
  (sum(data$kfr_top20_white_female_n 
      , na.rm = TRUE) + 
  sum(data$kfr_top20_white_male_n
      , na.rm = TRUE))
B1.data <- data.frame(c(bworking, wworking),c(bgraduate, wgraduate), c(btop, wtop))
rownames(B1.data) <- c("Black", "White")
colnames(B1.data) <- c("Fraction working", "Fraction graduate", "Probability top20%")
print(B1.data)
```

    ##       Fraction working Fraction graduate Probability top20%
    ## Black        0.7708635        0.08674101          0.0593834
    ## White        0.7909072        0.15223533          0.2603621

  - The fraction of black people working (77.09%) working is slightly
    lower than the fraction of white people working (79.09%).  
  - A higher fraction of whites (15.22%) earn graduate degree than
    blacks (8.67%).  
  - Whites are more likely to reach top 20% of the national household
    income distribution than blacks.

<!-- end list -->

``` r
# just out of curiosity, running a t-test here
t.test(data$grad_black_female_mean + data$grad_black_male_mean
       ,data$grad_white_female_mean + data$grad_white_male_mean)
```

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  data$grad_black_female_mean + data$grad_black_male_mean and data$grad_white_female_mean + data$grad_white_male_mean
    ## t = -17.474, df = 901.26, p-value < 2.2e-16
    ## alternative hypothesis: true difference in means is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.08159893 -0.06512025
    ## sample estimates:
    ## mean of x mean of y 
    ## 0.1568915 0.2302511

## 2\. How does the probability of reaching the top 1% of the national household income distribution (`kfr_top01`) differ by gender in a county of your choice. How does this compare to the national average? Explain your findings in 3-4 sentences.

HINT: To answer this you will need to create two new variables that
average 1) `black_female` and `white_female` and 2) `black_male` and
`white_male`. You could also try to get creative and think about how you
could use the count ’\_ n" variables to adjust your means before
creating your new variables, though this is not required. You will also
need to think about how to subset your data to limit to a single county.

> (3.5/4): Good, but remember you have to subset on both county and state since county 7 could appear in multiple states 

  - The explanation comes after this chunk with the data frame

<!-- end list -->

``` r
county7 <- subset(data, county == 7, select = c(kfr_top01_black_female_mean,
                                                kfr_top01_black_female_n,
                                                kfr_top01_black_male_mean,
                                                kfr_top01_black_male_n,
                                                kfr_top01_white_female_mean, 
                                                kfr_top01_white_female_n,
                                                kfr_top01_white_male_mean,
                                                kfr_top01_white_male_n))

countyFemale <- 
  mean(c(county7$kfr_top01_black_female_mean, county7$kfr_top01_white_female_mean),na.rm = TRUE)
countyMale <-
  mean(c(county7$kfr_top01_black_male_mean, county7$kfr_top01_white_male_mean),na.rm = TRUE)
usFemale <-
  mean(c(data$kfr_top01_black_female_mean, data$kfr_top01_white_female_mean),na.rm = TRUE)
usMale <-
  mean(c(data$kfr_top01_black_male_mean, data$kfr_top01_white_male_mean),na.rm = TRUE)
B2.data <- data.frame(c(countyFemale, countyMale),c(usFemale, usMale))
rownames(B2.data) <- c("Female", "Male")
colnames(B2.data) <- c("County 7", "National")
print(B2.data)
```

    ##           County 7    National
    ## Female 0.007018963 0.006897131
    ## Male   0.004486331 0.005148204

  - (The probability of reaching the top 1% of the national household
    income distribution is referred to as kfr\_top01 here.)  
  - In county7, the kfr\_top01 for females is higher than the kfr\_top01
    by 0.3 percentage point.
  - In the US, the kfr\_top01 for females is higher than the kfr\_top01
    for males by 0.1 percentage point.  
  - In general, males are more likely to reach top 1% in income
    comparing to females.

## 3\. Next, repeat question 2 but looking now for patterns by race. Explain what you find in 3-4 sentences?

> (4/4): Good (again don't forget to fix subsetting) 

``` r
county7 <- subset(data, county == 7, select = c(kfr_top01_black_female_mean,
                                                kfr_top01_black_female_n,
                                                kfr_top01_black_male_mean,
                                                kfr_top01_black_male_n,
                                                kfr_top01_white_female_mean, 
                                                kfr_top01_white_female_n,
                                                kfr_top01_white_male_mean,
                                                kfr_top01_white_male_n))

countyBlack <- 
  mean(c(county7$kfr_top01_black_female_mean, county7$kfr_top01_black_male_mean), na.rm = TRUE)
countyWhite <-
  mean(c(county7$kfr_top01_white_male_mean, county7$kfr_top01_white_female_mean), na.rm = TRUE)
usBlack <-
  mean(c(data$kfr_top01_black_female_mean, data$kfr_top01_black_male_mean), na.rm = TRUE)
usWhite<-
  mean(c(data$kfr_top01_white_male_mean, data$kfr_top01_white_female_mean), na.rm = TRUE)
B3.data <- data.frame(c(countyBlack, countyWhite),c(usBlack, usWhite))
rownames(B3.data) <- c("Black", "White")
colnames(B3.data) <- c("County 7", "National")
print(B3.data)
```

    ##          County 7    National
    ## Black 0.000227351 0.001413005
    ## White 0.008252186 0.008484266

  - (The probability of reaching the top 1% of the national household
    income distribution is refered to as kfr\_top01 here.)  
  - In county7, the kfr\_top01 for whites is higher than the kfr\_top01
    for blacks by 0.8 percentage point.  
  - In the US, the kfr\_top01 for whites is higher than the kfr\_top01
    for blacks by 0.7 percentage point.  
  - In general, white people have a greater possibility of reaching top
    1% in income comparing to black people.

<br>

<hr>

<br>

# Part C: Sketching out your project

## 1\. Limiting your answer to either race or gender, are there any other outcomes that might help explain the relationship you explored in Section B Question 2 or 3 (e.g., do you think `kfr_top01_gender` or `kfr_top01_race` are correlated with other outcomes)? Read over all of the variables in the dataset and provide an intuitive explanation for why you think another outcome could be correlated or related to upward mobility by race or gender. Don’t run any code for this question; just think about the relationship. Please explain your hypothesis in 3-4 sentences.

> (5/5): Great explanations

The following factors may have effect on reaching top 1%:  
Education (fraction having 4-year college degree, fraction having a
graduate degree)  
\- Higher education may result in an increased upward mobility since a
skilled-biased technological change favor the people with higher skills,
which is brought by education  
Mean percentile rank in income  
\- The original income itself may have a positive effect on mobility as
people with more income can pay for more opportunities  
Percentage of children staying in tract/move tract  
\- Moving to higher tract can have a positive impact on reaching top
1%  
Teen birth  
\- Having a child between the age of 13 and 19 can cause a distraction
of effort in advancing earnings, which will negatively effect top 1%
probability

## 2\. Using the hypothesis you developed in Section C Question 1, provide correlational evidence to test your hypothesis. You are welcome to use outside data that are not included in `country_outcomes.csv`, but this is not required. The goal of this question is to understand what might explain the variation in upward mobility for certain groups of children.

> (5/5): Great

In this chunk of code, we specifically look at female population in the
US.  
As shown by both the Pearson’s product-moment correlation and the
scatter plot, there is a moderate, significant positive association
(correlation coefficient of 0.62 and p-value \< 2.2e-16) between the
fraction of females earning a graduate degree and the probability of
females earning a top 1% income in a given county.

``` r
# Relationship between education level & upward mobility in females
# correlation test 
cor.test(data$grad_black_female_mean +  data$grad_white_female_mean, 
         data$kfr_top01_black_female_mean + data$kfr_top01_white_female_mean,
         method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data$grad_black_female_mean + data$grad_white_female_mean and data$kfr_top01_black_female_mean + data$kfr_top01_white_female_mean
    ## t = 18.713, df = 563, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.5656504 0.6676303
    ## sample estimates:
    ##       cor 
    ## 0.6192449

``` r
# visualizing the relationship
plot(data$grad_black_female_mean +  data$grad_white_female_mean, 
     data$kfr_top01_black_female_mean + data$kfr_top01_white_female_mean, 
     main="Graduate Degree Fraction's Relationship with Mobility",
   xlab="graduate degree fraction", ylab="top 1% probability", pch=19)
```

![](lab-1-problem-set_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->
The analysis below further shows that: comparing to the white
population, black population in the US have both a lower probability in
reaching top 1% income and a lower fraction earning graduate degree.

``` r
# This is not correlational analysis but just putting it here as reference
bTop <- mean(c(data$kfr_top01_black_female_mean, data$kfr_top01_black_male_mean), na.rm = TRUE)
wTop <- mean(c(data$kfr_top01_white_female_mean, data$kfr_top01_white_male_mean), na.rm = TRUE)
bGrad <- mean(c(data$grad_black_female_mean, data$grad_black_male_mean), na.rm = TRUE)
wGrad <- mean(c(data$grad_white_female_mean, data$grad_white_male_mean), na.rm = TRUE)
C2.data <- data.frame(c(bTop, wTop),c(bGrad, wGrad))
rownames(C2.data) <- c("Black", "White")
colnames(C2.data) <- c("Top 1%", "Grad Degree")
print(C2.data)
```

    ##            Top 1% Grad Degree
    ## Black 0.001413005  0.07792624
    ## White 0.008484266  0.11489610

In this chunk of code, we specifically look at white population in the
US.  
As shown by the Pearson’s product, there is a negative association
between the fraction of children staying in tract and the probability of
them earning a top 1% income. The small p-value (p-value \< 2.2e-16)
also indicates that the association is significant. However, a
correlation coefficient of -0.317 indicates that the moving tracts’
limited association with upward mobility.

``` r
# Relationship between tract changing & upward mobility in white people
# correlation test 
cor.test(data$staytract_white_male_mean +  data$staytract_white_female_mean, 
         data$kfr_top01_white_male_mean + data$kfr_top01_white_female_mean,
         method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data$staytract_white_male_mean + data$staytract_white_female_mean and data$kfr_top01_white_male_mean + data$kfr_top01_white_female_mean
    ## t = -17.606, df = 2769, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.3503914 -0.2834074
    ## sample estimates:
    ##        cor 
    ## -0.3172951

``` r
# visualizing the relationship
plot(data$staytract_white_male_mean +  data$staytract_white_female_mean, 
     data$kfr_top01_white_male_mean + data$kfr_top01_white_female_mean,
     main="Tract Relationship with Mobility",
   xlab="stay-tract fraction", ylab="top 1% probability", pch=19)
```

![](lab-1-problem-set_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

Mean income level and probability of reaching top 1% income have a
significant positive (p-value \< 2.2e-16) correlation, with a
correlation coefficient of 0.564 (for females in the US).

``` r
# Relationship between mean income level & upward mobility in black females
# correlation test 
cor.test(c(data$kfr_white_female_mean, data$kfr_black_female_mean), 
         c(data$kfr_top01_white_female_mean, data$kfr_top01_black_female_mean),
         method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  c(data$kfr_white_female_mean, data$kfr_black_female_mean) and c(data$kfr_top01_white_female_mean, data$kfr_top01_black_female_mean)
    ## t = 44.578, df = 4258, p-value < 2.2e-16
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.5432606 0.5842225
    ## sample estimates:
    ##       cor 
    ## 0.5640885

``` r
# visualizing the relationship
plot(c(data$kfr_white_female_mean, data$kfr_black_female_mean),
     c(data$kfr_top01_white_female_mean, data$kfr_top01_black_female_mean),
     main="Mean Income Level Relationship with Mobility",
   xlab="mean income level", ylab="top 1% probability", pch=19)
```

![](lab-1-problem-set_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

In this chunk of code, we specifically look at black female population
in the US.  
The correlation coefficient of -0.19 suggests that an increase teen
birth fraction correlates with a decrease in top 1% income probability,
but the effect is not huge.

``` r
# Relationship between teen birth & upward mobility in black females
# correlation test 
cor.test(data$teenbrth_black_female_mean, 
         data$kfr_top01_black_female_mean,
         method = "pearson")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  data$teenbrth_black_female_mean and data$kfr_top01_black_female_mean
    ## t = -7.6127, df = 1480, p-value = 4.757e-14
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.2426395 -0.1446275
    ## sample estimates:
    ##        cor 
    ## -0.1941179

``` r
# visualizing the relationship
plot(data$teenbrth_black_female_mean,  
     data$kfr_top01_black_female_mean,
     main="Teen Birth Relationship with Mobility",
   xlab="teen birth fraction", ylab="top 1% probability", pch=19)
```

![](lab-1-problem-set_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

In conclusion, two most significant factors contributing to an increase
in individuals’ probability of reaching the top 1% of the national
household income distribution are education level and general income
level, both presenting a positive correlation.

## 3\. Please consider the county you chose to examine in Section B and think about the mayor of that county. Identify one or two key lessons or takeaways that you might discuss with them about the determinants of economic opportunity (or the potential factors that are associated with individuals probability of reaching the top 1% of the national household income distribution). Mention any important caveats to your conclusions or any additional analyses you might want to conduct to prove your findings.

> (5/5): Great synthesis and explanation

In county 7, whites have a higher upward mobility than blacks, and
females have a higher upward mobility than males, both of which have a
difference higher than national level. According to the correlation
analysis, there are two potential factors that are associated with
individuals probability of reaching the top 1% of the national household
income distribution: education level and income level. Therefore, the
discrepancy can be lowered by increasing the educational opportunity for
blacks and males in the county or by raising the general income level of
the two groups. That is to say, more educational opportunities and
programs can be offered to the two groups to raise their skills to gain
more valuable jobs, which in turn will also raise the general income
level. In addition, incentives (such as honorary awards and prize) to
encourage the groups in getting a graduate degree can be provided ro
raise education levels and thereby increasing mobility.  
Additional research and experiments could be done to examine a causal
relationship since the analysis done in this study is primarily on
correlations. In other words, we were unable to conclude whether
education is the cause of a higher upward mobility. Therefore, some
observational studies that control for other factors (such as race,
gender, income level, region) can be done to examine whether a higher
education level means a higher upward mobility.
