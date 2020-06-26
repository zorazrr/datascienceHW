# Introduction to R Homework  
Zora Zhang, lesson 1  

### Question 1  
a. create a vector that includes all the integer from 20 to 40  
```{r}
> vec <- 20:40
> vec
 [1] 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40
```
b. what is the integer whose index is 10  
```{r}
> vec[10]
[1] 29
```
c. what are the integers whose indexes are 5, 7, 9  
```{r}
> vec[c(5, 7, 9)]
[1] 24 26 28
```
d. what are the integers whose value is bigger than 25  
```{r}
> vec[vec>25]
 [1] 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40
```
e. what are the mean and standard deviation of this vector  
```{r}
> mean(vec)
[1] 30
> sd(vec)
[1] 6.204837
```
### Question 2  
a. create a data frame  
```{r}
> fruits <- c("apple", "banana", "pear", "strawberry", "blueberry", "peach")
> prices <- c(2, 1, 2, 6, 10, 5)
> sales <- c(70, 90, 100, 50, 60, 80)
> df <- data.frame(fruits, prices, sales, row.names = seq(1,6))
> df
      fruits prices sales
1      apple      2    70
2     banana      1    90
3       pear      2   100
4 strawberry      6    50
5  blueberry     10    60
6      peach      5    80
```
b. what is the dimension of this data frame  
```{r}
> dim(df)
[1] 6 3
```
c. what are the data types of each column  
```{r}
> str(df)
'data.frame':	6 obs. of  3 variables:
 $ fruits: chr  "apple" "banana" "pear" "strawberry" ...
 $ prices: num  2 1 2 6 10 5
 $ sales : num  70 90 100 50 60 80
## note for myself: apply(df, 2, class) -> this does not work
```
d. whose price is bigger than or equal to 4  
```{r}
> df[df$prices >= 4,]$fruits
[1] "strawberry" "blueberry"  "peach" 
```
e. whose sale is between 50 to 80  
```{r}
> df[df$sales<80 & df$sales>50,]$fruits
[1] "apple"     "blueberry"
```
f. save this data frame as csv  
```{r}
> write.csv(df, file="df.csv", row.names = FALSE)
> read.csv("df.csv")
      fruits prices sales
1      apple      2    70
2     banana      1    90
3       pear      2   100
4 strawberry      6    50
5  blueberry     10    60
6      peach      5    80
```