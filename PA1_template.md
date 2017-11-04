# Reproducible Research: Peer Assessment 1

## Introduction

It is now possible to collect a large amount of data about personal movement using activity monitoring devices such as a Fitbit, Nike Fuelband, or Jawbone Up. These type of devices are part of the “quantified self” movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. But these data remain under-utilized both because the raw data are hard to obtain and there is a lack of statistical methods and software for processing and interpreting the data.

This assignment makes use of data from a personal activity monitoring device. This device collects data at 5 minute intervals through out the day. The data consists of two months of data from an anonymous individual collected during the months of October and November, 2012 and include the number of steps taken in 5 minute intervals each day.

The data for this assignment can be downloaded from the course web site:

* Dataset: Activity monitoring data [52K]

The variables included in this dataset are:

* steps: Number of steps taking in a 5-minute interval (missing values are coded as 𝙽𝙰)
* date: The date on which the measurement was taken in YYYY-MM-DD format
* interval: Identifier for the 5-minute interval in which measurement was taken

The dataset is stored in a comma-separated-value (CSV) file and there are a total of 17,568 observations in this dataset.



## Loading and preprocessing the data

1. Load the data (i.e. 𝚛𝚎𝚊𝚍.𝚌𝚜𝚟())


```r
## Loading the data from the CSV file
activity_data <- read.csv("./activity.csv", sep = ",", header = TRUE)

# Quick look at the data
str(activity_data)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Factor w/ 61 levels "2012-10-01","2012-10-02",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

2. Process/transform the data (if necessary) into a format suitable for your analysis


```r
# Convert Date variable to Date class
activity_data$date <- as.Date(as.character(activity_data$date), "%Y-%m-%d")

# Quick look at the data after formatting
str(activity_data)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Date, format: "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

## What is mean total number of steps taken per day?

For this part of the assignment, you can ignore the missing values in the dataset.

1. Calculate the total number of steps taken per day


```r
with(activity_data, plot(date, steps))
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)<!-- -->


```r
# Creation of Plot1.png (image shown above)
png(file = "Plot1.png", width = 480, height = 480, units = 'px', bg = "white")
with(activity_data, plot(date, steps))
dev.off()
```

```
## quartz_off_screen 
##                 2
```


```r
steps_per_day <- aggregate(steps ~ date, activity_data, sum)
steps_per_day
```

```
##          date steps
## 1  2012-10-02   126
## 2  2012-10-03 11352
## 3  2012-10-04 12116
## 4  2012-10-05 13294
## 5  2012-10-06 15420
## 6  2012-10-07 11015
## 7  2012-10-09 12811
## 8  2012-10-10  9900
## 9  2012-10-11 10304
## 10 2012-10-12 17382
## 11 2012-10-13 12426
## 12 2012-10-14 15098
## 13 2012-10-15 10139
## 14 2012-10-16 15084
## 15 2012-10-17 13452
## 16 2012-10-18 10056
## 17 2012-10-19 11829
## 18 2012-10-20 10395
## 19 2012-10-21  8821
## 20 2012-10-22 13460
## 21 2012-10-23  8918
## 22 2012-10-24  8355
## 23 2012-10-25  2492
## 24 2012-10-26  6778
## 25 2012-10-27 10119
## 26 2012-10-28 11458
## 27 2012-10-29  5018
## 28 2012-10-30  9819
## 29 2012-10-31 15414
## 30 2012-11-02 10600
## 31 2012-11-03 10571
## 32 2012-11-05 10439
## 33 2012-11-06  8334
## 34 2012-11-07 12883
## 35 2012-11-08  3219
## 36 2012-11-11 12608
## 37 2012-11-12 10765
## 38 2012-11-13  7336
## 39 2012-11-15    41
## 40 2012-11-16  5441
## 41 2012-11-17 14339
## 42 2012-11-18 15110
## 43 2012-11-19  8841
## 44 2012-11-20  4472
## 45 2012-11-21 12787
## 46 2012-11-22 20427
## 47 2012-11-23 21194
## 48 2012-11-24 14478
## 49 2012-11-25 11834
## 50 2012-11-26 11162
## 51 2012-11-27 13646
## 52 2012-11-28 10183
## 53 2012-11-29  7047
```

2. If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day.


```r
hist(steps_per_day$steps, breaks = 15, xlab = "Steps per day", 
     main = "Histogram of steps per day", col = "green")
```

![](PA1_template_files/figure-html/unnamed-chunk-6-1.png)<!-- -->


```r
# Creation of Plot2.png (histogram shown above)
png(file = "Plot2.png", width = 480, height = 480, units = 'px', bg = "white")
hist(steps_per_day$steps, breaks = 15, xlab = "Steps per day", 
     main = "Histogram of steps per day", col = "green")
dev.off()
```

```
## quartz_off_screen 
##                 2
```

3. Calculate and report the mean and median of the total number of steps taken per day


```r
sprintf("The mean total number of steps per day is: %f", mean(steps_per_day$steps))
```

```
## [1] "The mean total number of steps per day is: 10766.188679"
```

```r
sprintf("The median total number of steps per day is: %f", median(steps_per_day$steps))
```

```
## [1] "The median total number of steps per day is: 10765.000000"
```

## What is the average daily activity pattern?

1. Make a time series plot (i.e. 𝚝𝚢𝚙𝚎 = "𝚕") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
avg_steps_per_interval <- aggregate(steps ~ interval, activity_data, mean)
head(avg_steps_per_interval, 15)
```

```
##    interval     steps
## 1         0 1.7169811
## 2         5 0.3396226
## 3        10 0.1320755
## 4        15 0.1509434
## 5        20 0.0754717
## 6        25 2.0943396
## 7        30 0.5283019
## 8        35 0.8679245
## 9        40 0.0000000
## 10       45 1.4716981
## 11       50 0.3018868
## 12       55 0.1320755
## 13      100 0.3207547
## 14      105 0.6792453
## 15      110 0.1509434
```


```r
# Plot
plot(avg_steps_per_interval$interval, avg_steps_per_interval$steps, type = "l",
     xlab = "Interval", ylab = "Average number of steps", main = "Average number of steps per interval")
```

![](PA1_template_files/figure-html/unnamed-chunk-10-1.png)<!-- -->


```r
# Creation of Plot3.png (plot shown above)
png(file = "Plot3.png", width = 480, height = 480, units = 'px', bg = "white")
plot(avg_steps_per_interval$interval, avg_steps_per_interval$steps, type = "l",
     xlab = "Interval", ylab = "Average number of steps", main = "Average number of steps per interval")
dev.off()
```

```
## quartz_off_screen 
##                 2
```

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
sprintf("The 5-minute interval with the highest average number of steps is: %d",
        avg_steps_per_interval$interval[which.max(avg_steps_per_interval$steps)])
```

```
## [1] "The 5-minute interval with the highest average number of steps is: 835"
```

## Imputing missing values

Note that there are a number of days/intervals where there are missing values (coded as 𝙽𝙰). The presence of missing days may introduce bias into some calculations or summaries of the data.

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with 𝙽𝙰s)


```r
sprintf("The total number of missing values is: %d", sum(is.na(activity_data$steps)))
```

```
## [1] "The total number of missing values is: 2304"
```

2. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.


```r
temp <- numeric()

for (i in 1:length(activity_data$steps)) {
      if (is.na(activity_data$steps[i]) == TRUE) {
              temp <- append(temp, avg_steps_per_interval$steps[match(activity_data$interval[i], 
                      avg_steps_per_interval$interval, nomatch = 0)])
      }
      else {
              temp <- append(temp, activity_data$steps[i])
      }
}

plot(temp)
```

![](PA1_template_files/figure-html/unnamed-chunk-14-1.png)<!-- -->


```r
# Creation of Plot4.png (plot shown above)
png(file = "Plot4.png", width = 480, height = 480, units = 'px', bg = "white")
plot(temp)
dev.off()
```

```
## quartz_off_screen 
##                 2
```

3. Create a new dataset that is equal to the original dataset but with the missing data filled in.


```r
activity_data2 <- data.frame(steps = temp, date = activity_data$date, interval = activity_data$interval)

str(activity_data2)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : num  1.717 0.3396 0.1321 0.1509 0.0755 ...
##  $ date    : Date, format: "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?


```r
steps_per_day2 <- aggregate(steps ~ date, activity_data2, sum)
steps_per_day2
```

```
##          date    steps
## 1  2012-10-01 10766.19
## 2  2012-10-02   126.00
## 3  2012-10-03 11352.00
## 4  2012-10-04 12116.00
## 5  2012-10-05 13294.00
## 6  2012-10-06 15420.00
## 7  2012-10-07 11015.00
## 8  2012-10-08 10766.19
## 9  2012-10-09 12811.00
## 10 2012-10-10  9900.00
## 11 2012-10-11 10304.00
## 12 2012-10-12 17382.00
## 13 2012-10-13 12426.00
## 14 2012-10-14 15098.00
## 15 2012-10-15 10139.00
## 16 2012-10-16 15084.00
## 17 2012-10-17 13452.00
## 18 2012-10-18 10056.00
## 19 2012-10-19 11829.00
## 20 2012-10-20 10395.00
## 21 2012-10-21  8821.00
## 22 2012-10-22 13460.00
## 23 2012-10-23  8918.00
## 24 2012-10-24  8355.00
## 25 2012-10-25  2492.00
## 26 2012-10-26  6778.00
## 27 2012-10-27 10119.00
## 28 2012-10-28 11458.00
## 29 2012-10-29  5018.00
## 30 2012-10-30  9819.00
## 31 2012-10-31 15414.00
## 32 2012-11-01 10766.19
## 33 2012-11-02 10600.00
## 34 2012-11-03 10571.00
## 35 2012-11-04 10766.19
## 36 2012-11-05 10439.00
## 37 2012-11-06  8334.00
## 38 2012-11-07 12883.00
## 39 2012-11-08  3219.00
## 40 2012-11-09 10766.19
## 41 2012-11-10 10766.19
## 42 2012-11-11 12608.00
## 43 2012-11-12 10765.00
## 44 2012-11-13  7336.00
## 45 2012-11-14 10766.19
## 46 2012-11-15    41.00
## 47 2012-11-16  5441.00
## 48 2012-11-17 14339.00
## 49 2012-11-18 15110.00
## 50 2012-11-19  8841.00
## 51 2012-11-20  4472.00
## 52 2012-11-21 12787.00
## 53 2012-11-22 20427.00
## 54 2012-11-23 21194.00
## 55 2012-11-24 14478.00
## 56 2012-11-25 11834.00
## 57 2012-11-26 11162.00
## 58 2012-11-27 13646.00
## 59 2012-11-28 10183.00
## 60 2012-11-29  7047.00
## 61 2012-11-30 10766.19
```

```r
# Original histogram
hist(steps_per_day$steps, breaks = 15, xlab = "Steps per day", 
     main = "Histogram of steps per day", col = "green", ylim = c(0,25))

# New histogram
hist(steps_per_day2$steps, breaks = 15, xlab = "(Tweaked) steps per day", 
     main = "Histogram of (tweaked) steps per day", add = T, col = rgb(1, 0, 0, 0.5))
```

![](PA1_template_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

```r
sprintf("The mean total number of steps per day is: %f", mean(steps_per_day2$steps))
```

```
## [1] "The mean total number of steps per day is: 10766.188679"
```

```r
sprintf("The median total number of steps per day is: %f", median(steps_per_day2$steps))
```

```
## [1] "The median total number of steps per day is: 10766.188679"
```

As it can be seen above, the tweaked data adds more data around the average bin of steps. However, the data overlays very well in any other case.


```r
# Creation of Plot5.png (combined histogram shown above)
png(file = "Plot5.png", width = 480, height = 480, units = 'px', bg = "white")

# Original histogram
hist(steps_per_day$steps, breaks = 15, xlab = "Steps per day", 
     main = "Histogram of steps per day", col = "green", ylim = c(0,25))

# New histogram
hist(steps_per_day2$steps, breaks = 15, xlab = "(Tweaked) steps per day", 
     main = "Histogram of (tweaked) steps per day", add = T, col = rgb(1, 0, 0, 0.5))

dev.off()
```

```
## quartz_off_screen 
##                 2
```

## Are there differences in activity patterns between weekdays and weekends?

For this part the 𝚠𝚎𝚎𝚔𝚍𝚊𝚢𝚜() function may be of some help here. Use the dataset with the filled-in missing values for this part.

1. Create a new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.


```r
activity_data2$day_type <- weekdays(activity_data2$date)

table(activity_data2$day_type)
```

```
## 
##    Friday    Monday  Saturday    Sunday  Thursday   Tuesday Wednesday 
##      2592      2592      2304      2304      2592      2592      2592
```


```r
# Converting the days into weekday or weekend one
for (i in 1:length(activity_data2$day_type)) {
      if (activity_data2$day_type[i] %in% c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")) {
              activity_data2$day_type[i] <- "weekday"
      }
      else {
              activity_data2$day_type[i] <- "weekend"
      }
}

activity_data2$day_type <- as.factor(activity_data2$day_type)

table(activity_data2$day_type)
```

```
## 
## weekday weekend 
##   12960    4608
```

The if-statement has worked well. Before there were 2304 Saturdays and Sundays and now there are 4608 weekend days. The same can be said about the weekdays.

2. Make a panel plot containing a time series plot (i.e. 𝚝𝚢𝚙𝚎 = "𝚕") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.


```r
library(lattice)

avg_steps_per_interval2 <- aggregate(steps ~ interval + day_type, activity_data2, mean)

# Line plot of average steps per interval split by week days & weekend days
xyplot(steps ~ interval | day_type, data = avg_steps_per_interval2, type = "l", main="",
   xlab = "Interval", ylab = "Number of steps", layout = c(1,2))
```

![](PA1_template_files/figure-html/unnamed-chunk-21-1.png)<!-- -->

Your plot will look different from the one above because you will be using the activity monitor data. Note that the above plot was made using the lattice system but you can make the same version of the plot using any plotting system you choose.


```r
# Creation of Plot6.png (final plot shown above)
png(file = "Plot6.png", width = 480, height = 480, units = 'px', bg = "white")

xyplot(steps ~ interval | day_type, data = avg_steps_per_interval2, type = "l", main="",
   xlab = "Interval", ylab = "Number of steps", layout = c(1,2))

dev.off()
```

```
## quartz_off_screen 
##                 2
```
