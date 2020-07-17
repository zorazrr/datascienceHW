Statistics Homework
===================

Lesson 3.1

One-Sample T-Test
-----------------

-   Test whether the mean value of height is 68

<!-- -->

    set.seed(0)
    heights = rnorm(n = 100, mean = 70, sd = 1)
    t.test(heights, mu = 68, alternative = "two.sided")

    ## 
    ##  One Sample t-test
    ## 
    ## data:  heights
    ## t = 22.916, df = 99, p-value < 2.2e-16
    ## alternative hypothesis: true mean is not equal to 68
    ## 95 percent confidence interval:
    ##  69.84753 70.19781
    ## sample estimates:
    ## mean of x 
    ##  70.02267

Two-Sample T-Test
-----------------

-   Test whether mean values of SAT spring and fall are the same

<!-- -->

    set.seed(0)
    SAT.Spring = rnorm(100, 1550, 200) 
    SAT.Fall = rnorm(80, 1500, 210)
    t.test(SAT.Spring, SAT.Fall, alternative = "two.sided")

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  SAT.Spring and SAT.Fall
    ## t = 2.5376, df = 154.92, p-value = 0.01215
    ## alternative hypothesis: true difference in means is not equal to 0
    ## 95 percent confidence interval:
    ##   16.44063 131.97461
    ## sample estimates:
    ## mean of x mean of y 
    ##  1554.534  1480.326

F-Test
------

-   Test whether variances of SAT spring and fall are the same

<!-- -->

    set.seed(0)
    SAT.Spring = rnorm(100, 1550, 200) 
    SAT.Fall = rnorm(80, 1500, 210)
    var.test(SAT.Spring, SAT.Fall, alternative = "two.sided")

    ## 
    ##  F test to compare two variances
    ## 
    ## data:  SAT.Spring and SAT.Fall
    ## F = 0.71666, num df = 99, denom df = 79, p-value = 0.1161
    ## alternative hypothesis: true ratio of variances is not equal to 1
    ## 95 percent confidence interval:
    ##  0.4680916 1.0862459
    ## sample estimates:
    ## ratio of variances 
    ##          0.7166649

One-Way ANOVA
-------------

-   Test whether the mean values of the weight loss of different
    categories of diet are the same

<!-- -->

    set.seed(0)
    Low.Calorie = rnorm(200, 10, 1) #Randomly generating weight loss measurements
    Low.Carb = rnorm(200, 8.5, 1)   #for various diet types.
    Low.Fat = rnorm(200, 8, 1)
    Control = rnorm(200, 0, 1)

    Weight.Loss = c(Low.Calorie, Low.Carb, Low.Fat, Control) #Combining data into
    Category = c(rep("Low Calorie", 200),                    #different consolidated
                 rep("Low Carb", 200),                       #vectors.
                 rep("Low Fat", 200),
                 rep("Control", 200))
    summary(aov(Weight.Loss ~ Category))

    ##              Df Sum Sq Mean Sq F value Pr(>F)    
    ## Category      3  12061    4020    4202 <2e-16 ***
    ## Residuals   796    762       1                   
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

X^2 Test of Independence
------------------------

-   Test whether the attendance and grade variables are independent of
    one another

<!-- -->

    quiz.data = matrix(c(44, 21, 12, 18), nrow = 2, ncol = 2, byrow = TRUE)
    dimnames(quiz.data) = list(Attendance = c("Present", "Absent"),
                               Grade = c("Pass", "Fail"))
    chisq.test(quiz.data)

    ## 
    ##  Pearson's Chi-squared test with Yates' continuity correction
    ## 
    ## data:  quiz.data
    ## X-squared = 5.4106, df = 1, p-value = 0.02001
