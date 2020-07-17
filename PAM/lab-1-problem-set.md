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

``` r
# I didn't set working directory in the coding blocks here because it was constantly giving me warnings
data <- read.csv("~/Desktop/PAM2070/lab-1-master/county_outcomes.csv")
```

## 2\. View your data by running at least 2 functions. Write 3-5 things you looked for to check your dataset to make sure it is ready for analysis

  - Checked the lab1 dictionary to understand what each column name
    means  
  - There are some missing values  
  - The data type for each column matches  
  - There are no special characters

<!-- end list -->

``` r
head(data)
```

    ##   state county kfr_black_female_n kfr_black_female_mean
    ## 1     1      1                499             0.3370029
    ## 2     1      3                731             0.3270324
    ## 3     1      5                610             0.3221120
    ## 4     1      7                151             0.3164948
    ## 5     1      9                 37             0.3878466
    ## 6     1     11                379             0.3360103
    ##   kfr_top20_black_female_n kfr_top20_black_female_mean married_black_female_n
    ## 1                      499                  0.02538370                    499
    ## 2                      731                  0.03640969                    731
    ## 3                      610                  0.01816107                    610
    ## 4                      151                  0.02011928                    151
    ## 5                       37                  0.10375054                     37
    ## 6                      379                  0.02487344                    379
    ##   married_black_female_mean has_dad_black_female_n has_dad_black_female_mean
    ## 1                0.14349747                    499                 0.6015866
    ## 2                0.14115496                    731                 0.5398907
    ## 3                0.15395957                    610                 0.5044702
    ## 4                0.07868294                    151                 0.5477804
    ## 5                0.21568334                     37                 0.6471440
    ## 6                0.07511233                    379                 0.4541282
    ##   teenbrth_black_female_n teenbrth_black_female_mean working_black_female_n
    ## 1                     499                  0.4064051                    499
    ## 2                     731                  0.4486833                    731
    ## 3                     610                  0.4797659                    610
    ## 4                     151                  0.4676586                    151
    ## 5                      37                  0.2951654                     37
    ## 6                     379                  0.4610021                    379
    ##   working_black_female_mean proginc_black_female_n proginc_black_female_mean
    ## 1                 0.8094116                     34               0.031459238
    ## 2                 0.7985712                     30               0.008912955
    ## 3                 0.7518048                     53               0.079300791
    ## 4                 0.7909327                     NA                        NA
    ## 5                 0.8672689                     NA                        NA
    ## 6                 0.8645315                     20               0.064241372
    ##   coll_black_female_n coll_black_female_mean wgflx_rk_black_female_n
    ## 1                  49              0.1307171                      25
    ## 2                  54              0.1013089                      23
    ## 3                  75              0.1788976                      41
    ## 4                  NA                     NA                      NA
    ## 5                  NA                     NA                      NA
    ## 6                  37              0.1956653                      NA
    ##   wgflx_rk_black_female_mean hours_wk_black_female_n hours_wk_black_female_mean
    ## 1                  0.3607492                      34                   24.77809
    ## 2                  0.4176473                      30                   17.77164
    ## 3                  0.3310189                      53                   24.00033
    ## 4                         NA                      NA                         NA
    ## 5                         NA                      NA                         NA
    ## 6                         NA                      20                   27.02543
    ##   kfr_top01_black_female_n kfr_top01_black_female_mean lpov_nbh_black_female_n
    ## 1                      499                -2.18881e-04                     493
    ## 2                      731                 4.21075e-04                     727
    ## 3                      610                 3.92855e-05                     603
    ## 4                      151                -3.47129e-05                     142
    ## 5                       37                -7.72191e-04                      37
    ## 6                      379                -5.33440e-04                     377
    ##   lpov_nbh_black_female_mean two_par_black_female_n two_par_black_female_mean
    ## 1                  0.3024271                    499                 0.3725994
    ## 2                  0.3859628                    731                 0.3520698
    ## 3                  0.1367161                    610                 0.2922313
    ## 4                  0.2736446                    151                 0.2417640
    ## 5                  0.3262941                     37                 0.5815055
    ## 6                  0.1679836                    379                 0.1565185
    ##   has_mom_black_female_n has_mom_black_female_mean staytract_black_female_n
    ## 1                    499                 0.7715488                      493
    ## 2                    731                 0.8121898                      727
    ## 3                    610                 0.7876412                      603
    ## 4                    151                 0.6953583                      142
    ## 5                     37                 0.9301078                       37
    ## 6                    379                 0.7022056                      377
    ##   staytract_black_female_mean staycz_black_female_n staycz_black_female_mean
    ## 1                   0.3432580                   493                0.7427520
    ## 2                   0.3295109                   727                0.7269986
    ## 3                   0.2764032                   603                0.5543153
    ## 4                   0.3889445                   142                0.6824083
    ## 5                   0.3990394                    37                0.7631363
    ## 6                   0.3639771                   377                0.5523812
    ##   stayhome_black_female_n stayhome_black_female_mean grad_black_female_n
    ## 1                     349                  0.1614352                  34
    ## 2                     508                  0.2038647                  30
    ## 3                     438                  0.1415806                  53
    ## 4                      96                  0.1287211                  NA
    ## 5                      28                  0.2123814                  NA
    ## 6                     245                  0.1934096                  20
    ##   grad_black_female_mean comcoll_black_female_n comcoll_black_female_mean
    ## 1            0.043826956                     49                 0.2500366
    ## 2            0.074622251                     54                 0.2796043
    ## 3            0.083450019                     75                 0.2808316
    ## 4                     NA                     NA                        NA
    ## 5                     NA                     NA                        NA
    ## 6            0.000700543                     37                 0.2329868
    ##   kfr_white_female_n kfr_white_female_mean kfr_top20_white_female_n
    ## 1               2087             0.5411218                     2087
    ## 2               5287             0.5375591                     5287
    ## 3                581             0.5463973                      581
    ## 4                629             0.4821281                      629
    ## 5               1965             0.5065322                     1965
    ## 6                 72             0.5562441                       72
    ##   kfr_top20_white_female_mean married_white_female_n married_white_female_mean
    ## 1                   0.2143468                   2087                 0.6197094
    ## 2                   0.2401845                   5287                 0.5731577
    ## 3                   0.2499897                    581                 0.6106224
    ## 4                   0.1840649                    629                 0.5776168
    ## 5                   0.1730855                   1965                 0.6332253
    ## 6                   0.1978930                     72                 0.6320218
    ##   has_dad_white_female_n has_dad_white_female_mean teenbrth_white_female_n
    ## 1                   2087                 0.8778337                    2087
    ## 2                   5287                 0.8680992                    5287
    ## 3                    581                 0.8726886                     581
    ## 4                    629                 0.8831371                     629
    ## 5                   1965                 0.8806818                    1965
    ## 6                     72                 0.8082621                      72
    ##   teenbrth_white_female_mean working_white_female_n working_white_female_mean
    ## 1                  0.2047406                   2087                 0.7032043
    ## 2                  0.1513141                   5287                 0.7210175
    ## 3                  0.1600926                    581                 0.7293015
    ## 4                  0.2367821                    629                 0.6668786
    ## 5                  0.2055057                   1965                 0.6885803
    ## 6                  0.1511925                     72                 0.7438880
    ##   proginc_white_female_n proginc_white_female_mean coll_white_female_n
    ## 1                    150               0.019965889                 259
    ## 2                    320               0.014753786                 589
    ## 3                     47              -0.001814687                  92
    ## 4                     36               0.056180786                  60
    ## 5                    136               0.051395629                 248
    ## 6                     NA                        NA                  NA
    ##   coll_white_female_mean wgflx_rk_white_female_n wgflx_rk_white_female_mean
    ## 1              0.3976148                     112                  0.4384069
    ## 2              0.4538785                     253                  0.4412201
    ## 3              0.3616273                      39                  0.4599935
    ## 4              0.2794043                      29                  0.3307022
    ## 5              0.2791088                     101                  0.3993678
    ## 6                     NA                      NA                         NA
    ##   hours_wk_white_female_n hours_wk_white_female_mean kfr_top01_white_female_n
    ## 1                     150                   26.14148                     2087
    ## 2                     320                   29.29389                     5287
    ## 3                      47                   28.19461                      581
    ## 4                      36                   24.58986                      629
    ## 5                     136                   25.86518                     1965
    ## 6                      NA                         NA                       72
    ##   kfr_top01_white_female_mean lpov_nbh_white_female_n
    ## 1                 0.010101736                    2085
    ## 2                 0.009854255                    5273
    ## 3                 0.011235390                     577
    ## 4                 0.006171383                     624
    ## 5                 0.003507186                    1956
    ## 6                 0.002319279                      70
    ##   lpov_nbh_white_female_mean two_par_white_female_n two_par_white_female_mean
    ## 1                  0.4579629                   2087                 0.8281418
    ## 2                  0.4832333                   5287                 0.8190607
    ## 3                  0.2212533                    581                 0.8255195
    ## 4                  0.5494944                    629                 0.8256499
    ## 5                  0.3001253                   1965                 0.8314126
    ## 6                  0.2236788                     72                 0.6793117
    ##   has_mom_white_female_n has_mom_white_female_mean staytract_white_female_n
    ## 1                   2087                 0.9502377                     2085
    ## 2                   5287                 0.9509650                     5272
    ## 3                    581                 0.9525763                      577
    ## 4                    629                 0.9429002                      624
    ## 5                   1965                 0.9508504                     1956
    ## 6                     72                 0.8718960                       70
    ##   staytract_white_female_mean staycz_white_female_n staycz_white_female_mean
    ## 1                   0.2222793                  2085                0.6287229
    ## 2                   0.2275070                  5272                0.6463658
    ## 3                   0.2292848                   577                0.4597006
    ## 4                   0.3649709                   624                0.6601784
    ## 5                   0.3371961                  1956                0.7308510
    ## 6                   0.2691680                    70                0.4210826
    ##   stayhome_white_female_n stayhome_white_female_mean grad_white_female_n
    ## 1                    1644                 0.10215876                 151
    ## 2                    4106                 0.11858124                 320
    ## 3                     444                 0.10005120                  47
    ## 4                     453                 0.09220186                  36
    ## 5                    1561                 0.09342776                 136
    ## 6                      58                 0.07062487                  NA
    ##   grad_white_female_mean comcoll_white_female_n comcoll_white_female_mean
    ## 1              0.1341936                    259                 0.4651985
    ## 2              0.1964568                    589                 0.5404248
    ## 3              0.1069830                     92                 0.5503567
    ## 4              0.1230950                     60                 0.3399843
    ## 5              0.1078817                    248                 0.4714469
    ## 6                     NA                     NA                        NA
    ##   kfr_black_male_n kfr_black_male_mean kfr_top20_black_male_n
    ## 1              501           0.3197301                    501
    ## 2              724           0.3171760                    724
    ## 3              546           0.3182782                    546
    ## 4              148           0.3222759                    148
    ## 5               23           0.3110270                     23
    ## 6              352           0.3316492                    352
    ##   kfr_top20_black_male_mean married_black_male_n married_black_male_mean
    ## 1                0.05082923                  501              0.17289400
    ## 2                0.04104660                  724              0.14960597
    ## 3                0.02109020                  546              0.16656384
    ## 4                0.06811018                  148              0.10745071
    ## 5                0.03096484                   23              0.24513482
    ## 6                0.03868859                  352              0.09829982
    ##   has_dad_black_male_n has_dad_black_male_mean working_black_male_n
    ## 1                  501               0.5562433                  501
    ## 2                  724               0.5744982                  724
    ## 3                  546               0.5133083                  546
    ## 4                  148               0.6605446                  148
    ## 5                   23               0.6457092                   23
    ## 6                  352               0.4854806                  352
    ##   working_black_male_mean proginc_black_male_n proginc_black_male_mean
    ## 1               0.6833996                   22            -0.003126869
    ## 2               0.7258124                   31             0.002310379
    ## 3               0.7412036                   38            -0.000892095
    ## 4               0.7279115                   NA                      NA
    ## 5               0.5964073                   NA                      NA
    ## 6               0.7554434                   NA                      NA
    ##   coll_black_male_n coll_black_male_mean wgflx_rk_black_male_n
    ## 1                35           0.01536041                    NA
    ## 2                62           0.05934100                    23
    ## 3                56           0.10276040                    28
    ## 4                NA                   NA                    NA
    ## 5                NA                   NA                    NA
    ## 6                26           0.15456890                    NA
    ##   wgflx_rk_black_male_mean hours_wk_black_male_n hours_wk_black_male_mean
    ## 1                       NA                    22                 31.70519
    ## 2                0.3234752                    31                 25.40028
    ## 3                0.2616695                    38                 26.93019
    ## 4                       NA                    NA                       NA
    ## 5                       NA                    NA                       NA
    ## 6                       NA                    NA                       NA
    ##   kfr_top01_black_male_n kfr_top01_black_male_mean lpov_nbh_black_male_n
    ## 1                    501               0.003489581                   496
    ## 2                    724               0.000887550                   706
    ## 3                    546              -0.000121050                   533
    ## 4                    148               0.000430059                   146
    ## 5                     23              -0.000822484                    23
    ## 6                    352               0.000985565                   344
    ##   lpov_nbh_black_male_mean two_par_black_male_n two_par_black_male_mean
    ## 1                0.2823114                  501               0.3206169
    ## 2                0.3234259                  724               0.3483063
    ## 3                0.1313246                  546               0.2815444
    ## 4                0.3192523                  148               0.2259883
    ## 5                0.2375583                   23               0.6197997
    ## 6                0.1324616                  352               0.2066428
    ##   has_mom_black_male_n has_mom_black_male_mean staytract_black_male_n
    ## 1                  501               0.7638857                    496
    ## 2                  724               0.7738641                    706
    ## 3                  546               0.7681767                    533
    ## 4                  148               0.5644517                    146
    ## 5                   23               0.9741192                     23
    ## 6                  352               0.7219737                    344
    ##   staytract_black_male_mean staycz_black_male_n staycz_black_male_mean
    ## 1                 0.3070916                 496              0.7030039
    ## 2                 0.4007861                 706              0.6860818
    ## 3                 0.3533748                 533              0.5038515
    ## 4                 0.4400987                 146              0.6205408
    ## 5                 0.2463635                  23              0.8063398
    ## 6                 0.4511756                 344              0.5545300
    ##   stayhome_black_male_n stayhome_black_male_mean grad_black_male_n
    ## 1                   319                0.1561606                22
    ## 2                   430                0.2415182                31
    ## 3                   336                0.2379562                38
    ## 4                    84                0.2573650                NA
    ## 5                    NA                       NA                NA
    ## 6                   211                0.2293600                NA
    ##   grad_black_male_mean comcoll_black_male_n comcoll_black_male_mean
    ## 1          0.001025045                   35               0.1272385
    ## 2         -0.000153515                   62               0.1534180
    ## 3          0.030987525                   56               0.1063079
    ## 4                   NA                   NA                      NA
    ## 5                   NA                   NA                      NA
    ## 6                   NA                   26               0.2226231
    ##   kfr_white_male_n kfr_white_male_mean kfr_top20_white_male_n
    ## 1             2201           0.5151268                   2201
    ## 2             5579           0.5203547                   5579
    ## 3              607           0.5326733                    607
    ## 4              621           0.4971510                    621
    ## 5             2073           0.4792837                   2073
    ## 6               84           0.6086445                     84
    ##   kfr_top20_white_male_mean married_white_male_n married_white_male_mean
    ## 1                 0.1784086                 2201               0.5386097
    ## 2                 0.2021365                 5579               0.5197803
    ## 3                 0.1867746                  607               0.5762481
    ## 4                 0.1533654                  621               0.5080302
    ## 5                 0.1422150                 2073               0.5444211
    ## 6                 0.3182237                   84               0.6039526
    ##   has_dad_white_male_n has_dad_white_male_mean working_white_male_n
    ## 1                 2201               0.8925397                 2201
    ## 2                 5579               0.8791022                 5579
    ## 3                  607               0.8874971                  607
    ## 4                  621               0.8768630                  621
    ## 5                 2073               0.8901614                 2073
    ## 6                   84               0.9448157                   84
    ##   working_white_male_mean proginc_white_male_n proginc_white_male_mean
    ## 1               0.8028179                  148             0.014396770
    ## 2               0.7858192                  315             0.004898071
    ## 3               0.8269619                   56            -0.002084669
    ## 4               0.7861869                   37             0.010387817
    ## 5               0.7752141                  161             0.003501745
    ## 6               0.8629166                   NA                      NA
    ##   coll_white_male_n coll_white_male_mean wgflx_rk_white_male_n
    ## 1               277            0.2706028                   135
    ## 2               551            0.3569658                   286
    ## 3                85            0.3753962                    55
    ## 4                65            0.1831585                    33
    ## 5               267            0.1930389                   134
    ## 6                NA                   NA                    NA
    ##   wgflx_rk_white_male_mean hours_wk_white_male_n hours_wk_white_male_mean
    ## 1                0.5347556                   148                 39.12163
    ## 2                0.5470207                   315                 38.08926
    ## 3                0.5190231                    56                 43.04591
    ## 4                0.5854828                    37                 40.12568
    ## 5                0.4911565                   161                 36.09464
    ## 6                       NA                    NA                       NA
    ##   kfr_top01_white_male_n kfr_top01_white_male_mean lpov_nbh_white_male_n
    ## 1                   2201               0.000922560                  2189
    ## 2                   5579               0.006115567                  5556
    ## 3                    607               0.001700792                   603
    ## 4                    621               0.000392777                   617
    ## 5                   2073               0.000600574                  2051
    ## 6                     84               0.000361527                    84
    ##   lpov_nbh_white_male_mean two_par_white_male_n two_par_white_male_mean
    ## 1                0.4666750                 2201               0.8383797
    ## 2                0.4916529                 5579               0.8188722
    ## 3                0.2471495                  607               0.8321276
    ## 4                0.5262320                  621               0.7968608
    ## 5                0.2900886                 2073               0.8355019
    ## 6                0.1701991                   84               0.7582690
    ##   has_mom_white_male_n has_mom_white_male_mean staytract_white_male_n
    ## 1                 2201               0.9459462                   2189
    ## 2                 5579               0.9398397                   5555
    ## 3                  607               0.9445655                    603
    ## 4                  621               0.9196059                    617
    ## 5                 2073               0.9453693                   2051
    ## 6                   84               0.8109918                     84
    ##   staytract_white_male_mean staycz_white_male_n staycz_white_male_mean
    ## 1                 0.2630494                2189              0.6332470
    ## 2                 0.2758445                5555              0.6594155
    ## 3                 0.2634630                 603              0.4538665
    ## 4                 0.4354838                 617              0.7042018
    ## 5                 0.3870730                2051              0.7588179
    ## 6                 0.4163300                  84              0.5761868
    ##   stayhome_white_male_n stayhome_white_male_mean grad_white_male_n
    ## 1                  1721                0.1147313               148
    ## 2                  4282                0.1426789               315
    ## 3                   488                0.1333125                56
    ## 4                   424                0.1334119                37
    ## 5                  1631                0.1531187               161
    ## 6                    62                0.2126591                NA
    ##   grad_white_male_mean comcoll_white_male_n comcoll_white_male_mean
    ## 1           0.09489232                  277               0.3427551
    ## 2           0.15116145                  551               0.4428757
    ## 3           0.11382077                   85               0.5801111
    ## 4           0.08569633                   65               0.2228084
    ## 5           0.03319882                  267               0.3725684
    ## 6                   NA                   NA                      NA
    ##   kid_white_male_n kid_white_female_n kid_black_male_n kid_black_female_n
    ## 1             4963               4657             1219               1201
    ## 2            14451              13556             2423               2296
    ## 3             1616               1485             2068               2017
    ## 4             1958               1877              695                644
    ## 5             5993               5556               89                 88
    ## 6              200                197             1292               1266

``` r
tail(data)
```

    ##      state county kfr_black_female_n kfr_black_female_mean
    ## 2814    50     17                 NA                    NA
    ## 2815    50     19                 NA                    NA
    ## 2816    50     21                 NA                    NA
    ## 2817    50     23                 NA                    NA
    ## 2818    50     25                 NA                    NA
    ## 2819    50     27                 NA                    NA
    ##      kfr_top20_black_female_n kfr_top20_black_female_mean
    ## 2814                       NA                          NA
    ## 2815                       NA                          NA
    ## 2816                       NA                          NA
    ## 2817                       NA                          NA
    ## 2818                       NA                          NA
    ## 2819                       NA                          NA
    ##      married_black_female_n married_black_female_mean has_dad_black_female_n
    ## 2814                     NA                        NA                     NA
    ## 2815                     NA                        NA                     NA
    ## 2816                     NA                        NA                     NA
    ## 2817                     NA                        NA                     NA
    ## 2818                     NA                        NA                     NA
    ## 2819                     NA                        NA                     NA
    ##      has_dad_black_female_mean teenbrth_black_female_n
    ## 2814                        NA                      NA
    ## 2815                        NA                      NA
    ## 2816                        NA                      NA
    ## 2817                        NA                      NA
    ## 2818                        NA                      NA
    ## 2819                        NA                      NA
    ##      teenbrth_black_female_mean working_black_female_n
    ## 2814                         NA                     NA
    ## 2815                         NA                     NA
    ## 2816                         NA                     NA
    ## 2817                         NA                     NA
    ## 2818                         NA                     NA
    ## 2819                         NA                     NA
    ##      working_black_female_mean proginc_black_female_n proginc_black_female_mean
    ## 2814                        NA                     NA                        NA
    ## 2815                        NA                     NA                        NA
    ## 2816                        NA                     NA                        NA
    ## 2817                        NA                     NA                        NA
    ## 2818                        NA                     NA                        NA
    ## 2819                        NA                     NA                        NA
    ##      coll_black_female_n coll_black_female_mean wgflx_rk_black_female_n
    ## 2814                  NA                     NA                      NA
    ## 2815                  NA                     NA                      NA
    ## 2816                  NA                     NA                      NA
    ## 2817                  NA                     NA                      NA
    ## 2818                  NA                     NA                      NA
    ## 2819                  NA                     NA                      NA
    ##      wgflx_rk_black_female_mean hours_wk_black_female_n
    ## 2814                         NA                      NA
    ## 2815                         NA                      NA
    ## 2816                         NA                      NA
    ## 2817                         NA                      NA
    ## 2818                         NA                      NA
    ## 2819                         NA                      NA
    ##      hours_wk_black_female_mean kfr_top01_black_female_n
    ## 2814                         NA                       NA
    ## 2815                         NA                       NA
    ## 2816                         NA                       NA
    ## 2817                         NA                       NA
    ## 2818                         NA                       NA
    ## 2819                         NA                       NA
    ##      kfr_top01_black_female_mean lpov_nbh_black_female_n
    ## 2814                          NA                      NA
    ## 2815                          NA                      NA
    ## 2816                          NA                      NA
    ## 2817                          NA                      NA
    ## 2818                          NA                      NA
    ## 2819                          NA                      NA
    ##      lpov_nbh_black_female_mean two_par_black_female_n
    ## 2814                         NA                     NA
    ## 2815                         NA                     NA
    ## 2816                         NA                     NA
    ## 2817                         NA                     NA
    ## 2818                         NA                     NA
    ## 2819                         NA                     NA
    ##      two_par_black_female_mean has_mom_black_female_n has_mom_black_female_mean
    ## 2814                        NA                     NA                        NA
    ## 2815                        NA                     NA                        NA
    ## 2816                        NA                     NA                        NA
    ## 2817                        NA                     NA                        NA
    ## 2818                        NA                     NA                        NA
    ## 2819                        NA                     NA                        NA
    ##      staytract_black_female_n staytract_black_female_mean staycz_black_female_n
    ## 2814                       NA                          NA                    NA
    ## 2815                       NA                          NA                    NA
    ## 2816                       NA                          NA                    NA
    ## 2817                       NA                          NA                    NA
    ## 2818                       NA                          NA                    NA
    ## 2819                       NA                          NA                    NA
    ##      staycz_black_female_mean stayhome_black_female_n
    ## 2814                       NA                      NA
    ## 2815                       NA                      NA
    ## 2816                       NA                      NA
    ## 2817                       NA                      NA
    ## 2818                       NA                      NA
    ## 2819                       NA                      NA
    ##      stayhome_black_female_mean grad_black_female_n grad_black_female_mean
    ## 2814                         NA                  NA                     NA
    ## 2815                         NA                  NA                     NA
    ## 2816                         NA                  NA                     NA
    ## 2817                         NA                  NA                     NA
    ## 2818                         NA                  NA                     NA
    ## 2819                         NA                  NA                     NA
    ##      comcoll_black_female_n comcoll_black_female_mean kfr_white_female_n
    ## 2814                     NA                        NA               1037
    ## 2815                     NA                        NA                903
    ## 2816                     NA                        NA               2356
    ## 2817                     NA                        NA               2197
    ## 2818                     NA                        NA               1541
    ## 2819                     NA                        NA               2060
    ##      kfr_white_female_mean kfr_top20_white_female_n kfr_top20_white_female_mean
    ## 2814             0.5324748                     1037                   0.1988746
    ## 2815             0.5215180                      903                   0.1636214
    ## 2816             0.5599781                     2356                   0.2450233
    ## 2817             0.5782040                     2197                   0.2539123
    ## 2818             0.5314927                     1541                   0.2075918
    ## 2819             0.5722886                     2060                   0.2478273
    ##      married_white_female_n married_white_female_mean has_dad_white_female_n
    ## 2814                   1037                 0.5420299                   1037
    ## 2815                    903                 0.5292800                    903
    ## 2816                   2356                 0.5189429                   2356
    ## 2817                   2197                 0.5466577                   2197
    ## 2818                   1541                 0.5177766                   1541
    ## 2819                   2060                 0.5597084                   2060
    ##      has_dad_white_female_mean teenbrth_white_female_n
    ## 2814                 0.8727352                    1037
    ## 2815                 0.8561329                     903
    ## 2816                 0.8703737                    2356
    ## 2817                 0.8534603                    2197
    ## 2818                 0.8245710                    1541
    ## 2819                 0.8648429                    2060
    ##      teenbrth_white_female_mean working_white_female_n
    ## 2814                 0.10554752                   1037
    ## 2815                 0.12245324                    903
    ## 2816                 0.08194553                   2356
    ## 2817                 0.07723494                   2197
    ## 2818                 0.09163146                   1541
    ## 2819                 0.08796901                   2060
    ##      working_white_female_mean proginc_white_female_n proginc_white_female_mean
    ## 2814                 0.7701079                    124                0.05664094
    ## 2815                 0.7867867                    104                0.03756126
    ## 2816                 0.8142434                    221                0.04216443
    ## 2817                 0.8023031                    207                0.02980646
    ## 2818                 0.7614551                    157                0.03648491
    ## 2819                 0.7975169                    188                0.01007994
    ##      coll_white_female_n coll_white_female_mean wgflx_rk_white_female_n
    ## 2814                 207              0.3842975                     111
    ## 2815                 176              0.3662832                      91
    ## 2816                 327              0.4952888                     192
    ## 2817                 340              0.5084562                     174
    ## 2818                 243              0.4372796                     136
    ## 2819                 302              0.5330764                     162
    ##      wgflx_rk_white_female_mean hours_wk_white_female_n
    ## 2814                  0.4527129                     124
    ## 2815                  0.4323548                     104
    ## 2816                  0.4729097                     221
    ## 2817                  0.5199810                     207
    ## 2818                  0.3872043                     157
    ## 2819                  0.5000178                     188
    ##      hours_wk_white_female_mean kfr_top01_white_female_n
    ## 2814                   33.48925                     1037
    ## 2815                   31.29498                      903
    ## 2816                   33.61614                     2356
    ## 2817                   31.51968                     2197
    ## 2818                   27.21236                     1541
    ## 2819                   31.95932                     2060
    ##      kfr_top01_white_female_mean lpov_nbh_white_female_n
    ## 2814                 0.011815351                    1031
    ## 2815                 0.005099951                     897
    ## 2816                 0.010196937                    2346
    ## 2817                 0.019026604                    2188
    ## 2818                 0.009654013                    1531
    ## 2819                 0.013043866                    2049
    ##      lpov_nbh_white_female_mean two_par_white_female_n
    ## 2814                  0.6264788                   1037
    ## 2815                  0.3736326                    903
    ## 2816                  0.4449688                   2356
    ## 2817                  0.5858178                   2197
    ## 2818                  0.5492389                   1541
    ## 2819                  0.5036354                   2060
    ##      two_par_white_female_mean has_mom_white_female_n has_mom_white_female_mean
    ## 2814                 0.7874695                   1037                 0.9146241
    ## 2815                 0.8018438                    903                 0.9456981
    ## 2816                 0.8177322                   2356                 0.9472474
    ## 2817                 0.7995415                   2197                 0.9460388
    ## 2818                 0.7734556                   1541                 0.9488310
    ## 2819                 0.8034069                   2060                 0.9385783
    ##      staytract_white_female_n staytract_white_female_mean staycz_white_female_n
    ## 2814                     1031                   0.2421834                  1031
    ## 2815                      897                   0.1960038                   897
    ## 2816                     2346                   0.1866992                  2346
    ## 2817                     2188                   0.1765708                  2188
    ## 2818                     1531                   0.2173916                  1531
    ## 2819                     2049                   0.2126397                  2049
    ##      staycz_white_female_mean stayhome_white_female_n
    ## 2814                0.5611290                     742
    ## 2815                0.5523427                     590
    ## 2816                0.5493041                    1835
    ## 2817                0.4711045                    1685
    ## 2818                0.4846494                    1162
    ## 2819                0.4993287                    1522
    ##      stayhome_white_female_mean grad_white_female_n grad_white_female_mean
    ## 2814                 0.08352072                 124              0.1588434
    ## 2815                 0.08502518                 105              0.1068799
    ## 2816                 0.08593177                 221              0.1442232
    ## 2817                 0.09472448                 207              0.2357684
    ## 2818                 0.08883507                 157              0.1586343
    ## 2819                 0.11457939                 188              0.2663886
    ##      comcoll_white_female_n comcoll_white_female_mean kfr_black_male_n
    ## 2814                    207                 0.4920928               NA
    ## 2815                    176                 0.4791395               NA
    ## 2816                    327                 0.5920262               NA
    ## 2817                    340                 0.6067827               NA
    ## 2818                    243                 0.5183414               23
    ## 2819                    302                 0.6152407               NA
    ##      kfr_black_male_mean kfr_top20_black_male_n kfr_top20_black_male_mean
    ## 2814                  NA                     NA                        NA
    ## 2815                  NA                     NA                        NA
    ## 2816                  NA                     NA                        NA
    ## 2817                  NA                     NA                        NA
    ## 2818           0.3605041                     23                0.01156763
    ## 2819                  NA                     NA                        NA
    ##      married_black_male_n married_black_male_mean has_dad_black_male_n
    ## 2814                   NA                      NA                   NA
    ## 2815                   NA                      NA                   NA
    ## 2816                   NA                      NA                   NA
    ## 2817                   NA                      NA                   NA
    ## 2818                   23               0.2236117                   23
    ## 2819                   NA                      NA                   NA
    ##      has_dad_black_male_mean working_black_male_n working_black_male_mean
    ## 2814                      NA                   NA                      NA
    ## 2815                      NA                   NA                      NA
    ## 2816                      NA                   NA                      NA
    ## 2817                      NA                   NA                      NA
    ## 2818               0.6848758                   23               0.9153199
    ## 2819                      NA                   NA                      NA
    ##      proginc_black_male_n proginc_black_male_mean coll_black_male_n
    ## 2814                   NA                      NA                NA
    ## 2815                   NA                      NA                NA
    ## 2816                   NA                      NA                NA
    ## 2817                   NA                      NA                NA
    ## 2818                   NA                      NA                NA
    ## 2819                   NA                      NA                NA
    ##      coll_black_male_mean wgflx_rk_black_male_n wgflx_rk_black_male_mean
    ## 2814                   NA                    NA                       NA
    ## 2815                   NA                    NA                       NA
    ## 2816                   NA                    NA                       NA
    ## 2817                   NA                    NA                       NA
    ## 2818                   NA                    NA                       NA
    ## 2819                   NA                    NA                       NA
    ##      hours_wk_black_male_n hours_wk_black_male_mean kfr_top01_black_male_n
    ## 2814                    NA                       NA                     NA
    ## 2815                    NA                       NA                     NA
    ## 2816                    NA                       NA                     NA
    ## 2817                    NA                       NA                     NA
    ## 2818                    NA                       NA                     23
    ## 2819                    NA                       NA                     NA
    ##      kfr_top01_black_male_mean lpov_nbh_black_male_n lpov_nbh_black_male_mean
    ## 2814                        NA                    NA                       NA
    ## 2815                        NA                    NA                       NA
    ## 2816                        NA                    NA                       NA
    ## 2817                        NA                    NA                       NA
    ## 2818                0.00150115                    23                0.1676332
    ## 2819                        NA                    NA                       NA
    ##      two_par_black_male_n two_par_black_male_mean has_mom_black_male_n
    ## 2814                   NA                      NA                   NA
    ## 2815                   NA                      NA                   NA
    ## 2816                   NA                      NA                   NA
    ## 2817                   NA                      NA                   NA
    ## 2818                   23               0.3867316                   23
    ## 2819                   NA                      NA                   NA
    ##      has_mom_black_male_mean staytract_black_male_n staytract_black_male_mean
    ## 2814                      NA                     NA                        NA
    ## 2815                      NA                     NA                        NA
    ## 2816                      NA                     NA                        NA
    ## 2817                      NA                     NA                        NA
    ## 2818               0.7116455                     23                 0.1787606
    ## 2819                      NA                     NA                        NA
    ##      staycz_black_male_n staycz_black_male_mean stayhome_black_male_n
    ## 2814                  NA                     NA                    NA
    ## 2815                  NA                     NA                    NA
    ## 2816                  NA                     NA                    NA
    ## 2817                  NA                     NA                    NA
    ## 2818                  23                0.25162                    NA
    ## 2819                  NA                     NA                    NA
    ##      stayhome_black_male_mean grad_black_male_n grad_black_male_mean
    ## 2814                       NA                NA                   NA
    ## 2815                       NA                NA                   NA
    ## 2816                       NA                NA                   NA
    ## 2817                       NA                NA                   NA
    ## 2818                       NA                NA                   NA
    ## 2819                       NA                NA                   NA
    ##      comcoll_black_male_n comcoll_black_male_mean kfr_white_male_n
    ## 2814                   NA                      NA             1079
    ## 2815                   NA                      NA              941
    ## 2816                   NA                      NA             2394
    ## 2817                   NA                      NA             2171
    ## 2818                   NA                      NA             1610
    ## 2819                   NA                      NA             2108
    ##      kfr_white_male_mean kfr_top20_white_male_n kfr_top20_white_male_mean
    ## 2814           0.5153648                   1079                 0.1798689
    ## 2815           0.5258226                    941                 0.1621206
    ## 2816           0.5362619                   2394                 0.2127826
    ## 2817           0.5549493                   2171                 0.2341078
    ## 2818           0.5133812                   1610                 0.1826976
    ## 2819           0.5492907                   2108                 0.2241150
    ##      married_white_male_n married_white_male_mean has_dad_white_male_n
    ## 2814                 1079               0.4688559                 1079
    ## 2815                  941               0.4755339                  941
    ## 2816                 2394               0.4591118                 2394
    ## 2817                 2171               0.4817652                 2171
    ## 2818                 1610               0.4552836                 1610
    ## 2819                 2108               0.4886234                 2108
    ##      has_dad_white_male_mean working_white_male_n working_white_male_mean
    ## 2814               0.8995825                 1079               0.7912149
    ## 2815               0.8701408                  941               0.8192702
    ## 2816               0.8709954                 2394               0.8422195
    ## 2817               0.8665357                 2171               0.8440699
    ## 2818               0.8614088                 1610               0.7895304
    ## 2819               0.8498433                 2108               0.8323625
    ##      proginc_white_male_n proginc_white_male_mean coll_white_male_n
    ## 2814                  115              0.02230349               191
    ## 2815                  104              0.00152628               168
    ## 2816                  214              0.01062916               327
    ## 2817                  200              0.03220903               320
    ## 2818                  125              0.01475138               227
    ## 2819                  200              0.01215777               318
    ##      coll_white_male_mean wgflx_rk_white_male_n wgflx_rk_white_male_mean
    ## 2814            0.2825236                   108                0.4679845
    ## 2815            0.2246198                    98                0.4416624
    ## 2816            0.3112832                   197                0.5070745
    ## 2817            0.4035427                   184                0.4995531
    ## 2818            0.2811945                   111                0.4471393
    ## 2819            0.3830658                   183                0.4956303
    ##      hours_wk_white_male_n hours_wk_white_male_mean kfr_top01_white_male_n
    ## 2814                   115                 35.70341                   1079
    ## 2815                   104                 41.13918                    941
    ## 2816                   214                 39.55125                   2394
    ## 2817                   200                 36.87412                   2171
    ## 2818                   125                 36.09508                   1610
    ## 2819                   200                 39.33804                   2108
    ##      kfr_top01_white_male_mean lpov_nbh_white_male_n lpov_nbh_white_male_mean
    ## 2814               0.010378419                  1073                0.6411805
    ## 2815               0.004805379                   938                0.3646076
    ## 2816               0.011236452                  2382                0.4590614
    ## 2817               0.006832889                  2160                0.5746311
    ## 2818               0.008905591                  1597                0.5679185
    ## 2819               0.013452246                  2095                0.5021509
    ##      two_par_white_male_n two_par_white_male_mean has_mom_white_male_n
    ## 2814                 1079               0.8368725                 1079
    ## 2815                  941               0.8206397                  941
    ## 2816                 2394               0.8159419                 2394
    ## 2817                 2171               0.8126117                 2171
    ## 2818                 1610               0.7849408                 1610
    ## 2819                 2108               0.7830672                 2108
    ##      has_mom_white_male_mean staytract_white_male_n staytract_white_male_mean
    ## 2814               0.9371291                   1073                 0.3044748
    ## 2815               0.9503607                    938                 0.2808748
    ## 2816               0.9449711                   2382                 0.2543827
    ## 2817               0.9461506                   2160                 0.2362534
    ## 2818               0.9234899                   1597                 0.2523014
    ## 2819               0.9331535                   2095                 0.2574826
    ##      staycz_white_male_n staycz_white_male_mean stayhome_white_male_n
    ## 2814                1073              0.6024863                   768
    ## 2815                 938              0.5676731                   612
    ## 2816                2382              0.5807922                  1845
    ## 2817                2160              0.5101184                  1688
    ## 2818                1597              0.5020658                  1198
    ## 2819                2095              0.5451321                  1559
    ##      stayhome_white_male_mean grad_white_male_n grad_white_male_mean
    ## 2814                0.1197646               115           0.03934613
    ## 2815                0.1024093               104           0.04227418
    ## 2816                0.1348389               214           0.11414912
    ## 2817                0.1194551               201           0.09090429
    ## 2818                0.1214179               126           0.05986797
    ## 2819                0.1260882               201           0.15658593
    ##      comcoll_white_male_n comcoll_white_male_mean kid_white_male_n
    ## 2814                  191               0.4001381             3607
    ## 2815                  168               0.3201279             3304
    ## 2816                  327               0.3899698             7296
    ## 2817                  320               0.4899429             6555
    ## 2818                  227               0.3572921             5058
    ## 2819                  318               0.4457925             6564
    ##      kid_white_female_n kid_black_male_n kid_black_female_n
    ## 2814               3366               19                  5
    ## 2815               2992               21                 23
    ## 2816               6964               32                 29
    ## 2817               6379               51                 45
    ## 2818               4757               25                 37
    ## 2819               6220               36                 31

``` r
sapply(X = data, FUN = function(x) sum(is.na(x)))
```

    ##                       state                      county 
    ##                           0                           0 
    ##          kfr_black_female_n       kfr_black_female_mean 
    ##                        1337                        1337 
    ##    kfr_top20_black_female_n kfr_top20_black_female_mean 
    ##                        1337                        1337 
    ##      married_black_female_n   married_black_female_mean 
    ##                        1337                        1337 
    ##      has_dad_black_female_n   has_dad_black_female_mean 
    ##                        1337                        1337 
    ##     teenbrth_black_female_n  teenbrth_black_female_mean 
    ##                        1337                        1337 
    ##      working_black_female_n   working_black_female_mean 
    ##                        1337                        1337 
    ##      proginc_black_female_n   proginc_black_female_mean 
    ##                        2230                        2230 
    ##         coll_black_female_n      coll_black_female_mean 
    ##                        2046                        2046 
    ##     wgflx_rk_black_female_n  wgflx_rk_black_female_mean 
    ##                        2323                        2323 
    ##     hours_wk_black_female_n  hours_wk_black_female_mean 
    ##                        2230                        2230 
    ##    kfr_top01_black_female_n kfr_top01_black_female_mean 
    ##                        1337                        1337 
    ##     lpov_nbh_black_female_n  lpov_nbh_black_female_mean 
    ##                        1340                        1340 
    ##      two_par_black_female_n   two_par_black_female_mean 
    ##                        1337                        1337 
    ##      has_mom_black_female_n   has_mom_black_female_mean 
    ##                        1337                        1337 
    ##    staytract_black_female_n staytract_black_female_mean 
    ##                        1340                        1340 
    ##       staycz_black_female_n    staycz_black_female_mean 
    ##                        1340                        1340 
    ##     stayhome_black_female_n  stayhome_black_female_mean 
    ##                        1432                        1432 
    ##         grad_black_female_n      grad_black_female_mean 
    ##                        2229                        2229 
    ##      comcoll_black_female_n   comcoll_black_female_mean 
    ##                        2046                        2046 
    ##          kfr_white_female_n       kfr_white_female_mean 
    ##                          41                          41 
    ##    kfr_top20_white_female_n kfr_top20_white_female_mean 
    ##                          41                          41 
    ##      married_white_female_n   married_white_female_mean 
    ##                          41                          41 
    ##      has_dad_white_female_n   has_dad_white_female_mean 
    ##                          41                          41 
    ##     teenbrth_white_female_n  teenbrth_white_female_mean 
    ##                          41                          41 
    ##      working_white_female_n   working_white_female_mean 
    ##                          41                          41 
    ##      proginc_white_female_n   proginc_white_female_mean 
    ##                         432                         432 
    ##         coll_white_female_n      coll_white_female_mean 
    ##                         272                         272 
    ##     wgflx_rk_white_female_n  wgflx_rk_white_female_mean 
    ##                         552                         552 
    ##     hours_wk_white_female_n  hours_wk_white_female_mean 
    ##                         432                         432 
    ##    kfr_top01_white_female_n kfr_top01_white_female_mean 
    ##                          41                          41 
    ##     lpov_nbh_white_female_n  lpov_nbh_white_female_mean 
    ##                          42                          42 
    ##      two_par_white_female_n   two_par_white_female_mean 
    ##                          41                          41 
    ##      has_mom_white_female_n   has_mom_white_female_mean 
    ##                          41                          41 
    ##    staytract_white_female_n staytract_white_female_mean 
    ##                          42                          42 
    ##       staycz_white_female_n    staycz_white_female_mean 
    ##                          42                          42 
    ##     stayhome_white_female_n  stayhome_white_female_mean 
    ##                          70                          70 
    ##         grad_white_female_n      grad_white_female_mean 
    ##                         432                         432 
    ##      comcoll_white_female_n   comcoll_white_female_mean 
    ##                         272                         272 
    ##            kfr_black_male_n         kfr_black_male_mean 
    ##                        1328                        1328 
    ##      kfr_top20_black_male_n   kfr_top20_black_male_mean 
    ##                        1328                        1328 
    ##        married_black_male_n     married_black_male_mean 
    ##                        1328                        1328 
    ##        has_dad_black_male_n     has_dad_black_male_mean 
    ##                        1328                        1328 
    ##        working_black_male_n     working_black_male_mean 
    ##                        1328                        1328 
    ##        proginc_black_male_n     proginc_black_male_mean 
    ##                        2264                        2264 
    ##           coll_black_male_n        coll_black_male_mean 
    ##                        2091                        2091 
    ##       wgflx_rk_black_male_n    wgflx_rk_black_male_mean 
    ##                        2393                        2393 
    ##       hours_wk_black_male_n    hours_wk_black_male_mean 
    ##                        2264                        2264 
    ##      kfr_top01_black_male_n   kfr_top01_black_male_mean 
    ##                        1328                        1328 
    ##       lpov_nbh_black_male_n    lpov_nbh_black_male_mean 
    ##                        1334                        1334 
    ##        two_par_black_male_n     two_par_black_male_mean 
    ##                        1328                        1328 
    ##        has_mom_black_male_n     has_mom_black_male_mean 
    ##                        1328                        1328 
    ##      staytract_black_male_n   staytract_black_male_mean 
    ##                        1334                        1334 
    ##         staycz_black_male_n      staycz_black_male_mean 
    ##                        1334                        1334 
    ##       stayhome_black_male_n    stayhome_black_male_mean 
    ##                        1453                        1453 
    ##           grad_black_male_n        grad_black_male_mean 
    ##                        2263                        2263 
    ##        comcoll_black_male_n     comcoll_black_male_mean 
    ##                        2091                        2091 
    ##            kfr_white_male_n         kfr_white_male_mean 
    ##                          35                          35 
    ##      kfr_top20_white_male_n   kfr_top20_white_male_mean 
    ##                          35                          35 
    ##        married_white_male_n     married_white_male_mean 
    ##                          35                          35 
    ##        has_dad_white_male_n     has_dad_white_male_mean 
    ##                          35                          35 
    ##        working_white_male_n     working_white_male_mean 
    ##                          35                          35 
    ##        proginc_white_male_n     proginc_white_male_mean 
    ##                         451                         451 
    ##           coll_white_male_n        coll_white_male_mean 
    ##                         262                         262 
    ##       wgflx_rk_white_male_n    wgflx_rk_white_male_mean 
    ##                         494                         494 
    ##       hours_wk_white_male_n    hours_wk_white_male_mean 
    ##                         451                         451 
    ##      kfr_top01_white_male_n   kfr_top01_white_male_mean 
    ##                          35                          35 
    ##       lpov_nbh_white_male_n    lpov_nbh_white_male_mean 
    ##                          35                          35 
    ##        two_par_white_male_n     two_par_white_male_mean 
    ##                          35                          35 
    ##        has_mom_white_male_n     has_mom_white_male_mean 
    ##                          35                          35 
    ##      staytract_white_male_n   staytract_white_male_mean 
    ##                          35                          35 
    ##         staycz_white_male_n      staycz_white_male_mean 
    ##                          35                          35 
    ##       stayhome_white_male_n    stayhome_white_male_mean 
    ##                          71                          71 
    ##           grad_white_male_n        grad_white_male_mean 
    ##                         450                         450 
    ##        comcoll_white_male_n     comcoll_white_male_mean 
    ##                         262                         262 
    ##            kid_white_male_n          kid_white_female_n 
    ##                           3                           3 
    ##            kid_black_male_n          kid_black_female_n 
    ##                           3                           3

## 3\. Compare mean income ranks between black females and white females for all counties in the United States (use `kfr_black_female_mean` and `kfr_white_female_mean`). Write 1-2 sentences summarizing your finding. HINT: your dataset represents the United States. Therefore, when we ask you to compare the mean for all counties in the United States, we’re asking you to find the average for the entire dataset without subsetting.)

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

``` r
print(mean(data$kfr_white_female_mean, na.rm = TRUE))
```

    ## [1] 0.5540307

``` r
data$kfr_white_female_us_mean <- mean(data$kfr_white_female_mean, na.rm = TRUE)
```

## 7\. Create an indicator variable that evaluates whether the mean income rank for white women in a county (hint: recall that every observation or row is a unique county) is below or above the United States average (hint: use what you created in question 6). Write 1-2 sentences explaining your findings.

  - The national average of `kfr_white_female_mean` is at 0.554, which
    is roughly in the middle and normal. Therefore, it is reasonable to
    infer that in question 8, the answer is roughly half-half.

<!-- end list -->

``` r
data$kfr_white_female_above_mean <- 
  (data$kfr_white_female_mean > data$kfr_white_female_us_mean)
```

## 8\. Summarize your new variable by reporting how many observations are equal to 0 or 1 (i.e., how many counties are below or above the national average).

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
