# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

```r
data <-read.csv("activity.csv",na.strings = "NA",sep=",")
bad<- is.na(data$steps)

complete <- data[!bad,]
print(head(complete))
```

```
##     steps       date interval
## 289     0 2012-10-02        0
## 290     0 2012-10-02        5
## 291     0 2012-10-02       10
## 292     0 2012-10-02       15
## 293     0 2012-10-02       20
## 294     0 2012-10-02       25
```


## What is mean total number of steps taken per day?

```r
library(datasets)
x <- data.frame(Category=complete$date, 
                  Frequency=complete$steps)
  xSummary <- aggregate(x$Frequency, by=list(Category=x$Category), FUN=sum)

hist(xSummary$x,xlab="total number of steps taken each day",main="")
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 

```r
dev.off()
```

```
## null device 
##           1
```

```r
# Mean Number of steps:
mean(complete$steps)
```

```
## [1] 37.3826
```

```r
# Median Number of Steps:
median(complete$steps)
```

```
## [1] 0
```
## What is the average daily activity pattern?

```r
day_act <-data.frame(Category=complete$interval, 
                  Frequency=complete$steps)
xAvg <- aggregate(day_act$Frequency, by=list(Category=day_act$Category), FUN=mean)


 plot(xAvg$Category,
       xAvg$x,        
       type="l",
       col="black", 
       xlab="5 minute interval", 
       ylab="Avg Steps", 
       main="Frequency of Steps per 5 minute interval")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 

```r
  dev.off()
```

```
## null device 
##           1
```

```r
hold<- xAvg[which.max(xAvg$x), ]

#interval with max steps:
hold$Category
```

```
## [1] 835
```
## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?