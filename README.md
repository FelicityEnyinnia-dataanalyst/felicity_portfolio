# Playing it Smart: Data-Driven Insights for a Wellness Tech Company

### Project Overview

This data analysis project is being completed as part of the Google Data Analytics Capstone Project. In this simulation, I am acting as a junior data analyst on the marketing analytics team at Bellabeat. Bellabeat is a high-tech company that manufactures health-focused smart devices. The Chief Creative Officer (CCO) of Bellabeat has tasked me with analyzing smart device data available on Kaggle to identify opportunities for the company's growth.
The primary objective is to uncover insights about how Bellabeat consumers are using their smart devices to support their fitness journeys. My findings from this analysis will form the basis of data-driven recommendations that I will present to the CCO, which will help Bellabeat optimize its product offerings and marketing strategies to better meet consumer needs and expand its market presence.

### Data Sources

FitBit Fitness Tracker Data [Download here](https://www.kaggle.com/datasets/arashnic/fitbit): This public dataset, sourced from Kaggle, contains personal fitness tracking data from 30 Fitbit users. It captures a variety of metrics, including:
- Daily Steps: Records of users' daily step counts.
- Sleep Patterns: Information on sleep duration and quality.
- Calories Burned: Daily caloric expenditure.
- Heart Rate: Heart rate monitoring data.
   
### Tools

- Excel 
- R Programming Language - Data Claening, Analysis and Visualization.
I mostly utilized R in this data analysis. However, Excel was useful in previewing the dataset after I downloded it from Kaggle.

### Load Relevant R Packages

- install.packages("tidyverse")
- library(tidyverse)
- install.packages("readr")
- library(readr)
- install.packages("here")
- library(here)
- install.packages("skimr")
- library(skimr)
- install.packages("janitor")
- library(janitor)
- install.packages("tidyr")
- library(tidyr)
- install.packages("dplyr")
- library(dplyr)

### Import Data Set into RStudio

The dataset for this analysis is downloaded from Kaggle.Rather than using the readr package to import the dataset directly from Kaggle into R, I downloaded the dataset to my laptop and thereafter, uploaded and imported into RStudio using the following codes:

```R
dailyActivity_merged <- read.csv("Fitabase Data 3.12.16-4.11.16/dailyActivity_merged.csv")
hourly_steps <- read.csv("Fitabase Data 3.12.16-4.11.16/hourlySteps_merged.csv")
daily_sleep <- read.csv("Fitabase Data 3.12.16-4.11.16/daily_sleep_merged.csv")
heartrate_seconds <- read.csv("Fitabase Data 3.12.16-4.11.16/heartrate_seconds_merged.csv")
```

### Preview Data set

Before I preview the structure and organisation of the datasets, I want to rename the "dailyActivity_merged" as 

```R
daily_activity1 <- dailyActivity_merged
```

```R
str(daily_activity1)
head(hourly_steps)
glimpse(daily_sleep)
colnames(heartrate_seconds)
```

- Outcome of Our Data Preview Function

``` R

'data.frame':	457 obs. of  15 variables:
 $ Id                      : num  1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
 $ ActivityDate            : chr  "3/25/2016" "3/26/2016" "3/27/2016" "3/28/2016" ...
 $ TotalSteps              : int  11004 17609 12736 13231 12041 10970 12256 12262 11248 10016 ...
 $ TotalDistance           : num  7.11 11.55 8.53 8.93 7.85 ...
 $ TrackerDistance         : num  7.11 11.55 8.53 8.93 7.85 ...
 $ LoggedActivitiesDistance: num  0 0 0 0 0 0 0 0 0 0 ...
 $ VeryActiveDistance      : num  2.57 6.92 4.66 3.19 2.16 ...
 $ ModeratelyActiveDistance: num  0.46 0.73 0.16 0.79 1.09 ...
 $ LightActiveDistance     : num  4.07 3.91 3.71 4.95 4.61 ...
 $ SedentaryActiveDistance : num  0 0 0 0 0 0 0 0 0 0 ...
 $ VeryActiveMinutes       : int  33 89 56 39 28 30 33 47 40 15 ...
 $ FairlyActiveMinutes     : int  12 17 5 20 28 13 12 21 11 30 ...
 $ LightlyActiveMinutes    : int  205 274 268 224 243 223 239 200 244 314 ...
 $ SedentaryMinutes        : int  804 588 605 1080 763 1174 820 866 636 655 ...
 $ Calories                : int  1819 2154 1944 1932 1886 1820 1889 1868 1843 1850 ...

> head(hourly_steps)
          id          activityhour steptotal
1 1503960366 3/12/2016 12:00:00 AM         0
2 1503960366  3/12/2016 1:00:00 AM         0
3 1503960366  3/12/2016 2:00:00 AM         0
4 1503960366  3/12/2016 3:00:00 AM         0
5 1503960366  3/12/2016 4:00:00 AM         0
6 1503960366  3/12/2016 5:00:00 AM         0

> glimpse(daily_sleep)
Rows: 410
Columns: 5
$ id                 <dbl> 1503960366, 1503960366, 1503960366, 1503960366, 1503960366, 1503960366, …
$ sleepday           <chr> "04/12/2016 00:00", "4/13/2016 12:00:00 AM", "4/15/2016 12:00:00 AM", "4…
$ totalsleeprecords  <int> 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
$ totalminutesasleep <int> 327, 384, 412, 340, 700, 304, 360, 325, 361, 430, 277, 245, 366, 341, 40…
$ totaltimeinbed     <int> 346, 407, 442, 367, 712, 320, 377, 364, 384, 449, 323, 274, 393, 354, 42…
> colnames(heartrate_seconds)
[1] "id"    "time"  "value"

> str(daily_activity1)
'data.frame':	457 obs. of  15 variables:
 $ Id                      : num  1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
 $ ActivityDate            : chr  "3/25/2016" "3/26/2016" "3/27/2016" "3/28/2016" ...
 $ TotalSteps              : int  11004 17609 12736 13231 12041 10970 12256 12262 11248 10016 ...
 $ TotalDistance           : num  7.11 11.55 8.53 8.93 7.85 ...
 $ TrackerDistance         : num  7.11 11.55 8.53 8.93 7.85 ...
 $ LoggedActivitiesDistance: num  0 0 0 0 0 0 0 0 0 0 ...
 $ VeryActiveDistance      : num  2.57 6.92 4.66 3.19 2.16 ...
 $ ModeratelyActiveDistance: num  0.46 0.73 0.16 0.79 1.09 ...
 $ LightActiveDistance     : num  4.07 3.91 3.71 4.95 4.61 ...
 $ SedentaryActiveDistance : num  0 0 0 0 0 0 0 0 0 0 ...
 $ VeryActiveMinutes       : int  33 89 56 39 28 30 33 47 40 15 ...
 $ FairlyActiveMinutes     : int  12 17 5 20 28 13 12 21 11 30 ...
 $ LightlyActiveMinutes    : int  205 274 268 224 243 223 239 200 244 314 ...
 $ SedentaryMinutes        : int  804 588 605 1080 763 1174 820 866 636 655 ...
 $ Calories                : int  1819 2154 1944 1932 1886 1820 1889 1868 1843 1850 ...
```
From the above outcome, we observe that each of the dataset contains key variables such as the users Id, ActivityDate and other critical metrics essential for analyzing users' daily fitness habits and drawing meaningful insights.


### Data Cleaning and Preprocessing

- First, I want to find out how many unique Ids are contained in each of the datasets.

```R
library(dplyr)
n_distinct(daily_activity1$Id)
n_distinct(hourly_steps$Id)
n_distinct(daily_sleep$Id)
n_distinct(heartrate_seconds$Id)
```

- Outcome of the n_distinct function

We have 35 distinct Id in daily_activity1.
We have 34 distinct Id in hourly_steps.
We have 24 distinct Id in daily_sleep
We have 14 distinct Id in heartrate_seconds


## Locate duplicate values in the datasets.

```R
sum(duplicated(daily_activity1))
sum(duplicated(hourly_steps))
sum(duplicated(daily_sleep))
sum(duplicated(heartrate_seconds))
```


- Outcome of duplicated function.

There are no duplicate values in the other datasets except for daily_sleep which contains 3 duplicate values.Therefore, I will remove the duplicates found in daily_sleep and thereafter, confirm that they are removed from the dataset.


```R
library(tidyr)
daily_sleep <- daily_sleep %>% 
  distinct() %>% 
  drop_na()
```
  
- Verify that duplicate values have been removed from daily_sleep

```R
sum(duplicated(daily_sleep))
```

## Clean and Rename Column Names
- I want to rename and format the column names. This is to ensure that the column names are using the right syntax and consistent considering that I may decide to merge the datasets subsequently to discover trends and correlations. I will use the clean_names and rename_with functions to convert the column names to lowercase.

```R
library(janitor)
library(dplyr)

clean_names(daily_activity1)
daily_activity <- rename_with(daily_activity1, tolower)
clean_names(daily_sleep)
daily_sleep <- rename_with(daily_sleep, tolower)
clean_names(hourly_steps)
hourly_steps <- rename_with(hourly_steps, tolower)
clean_names(heartrate_seconds)
heartrate_seconds <- rename_with(heartrate_seconds, tolower)
```
The columns names have now been converted to lowercase for easy manipulation.

## Consistency of Date and Time

I observed that the date and time columns in the datasets are not in the proper format readable by R. The dates are not consistent. Hence, this is where the as.date and POSIXct functions comes into place to ensure date and time consistency.

```R
daily_activity_2 <- daily_activity %>% 
  rename(date = activitydate) %>% 
  mutate(date= as.Date(date, format = "%m/%d/%Y"))

hourly_steps1 <- hourly_steps %>%
  rename(date_time = activityhour) %>% 
  mutate(date_time = as.POSIXct(date_time, format = "%m/%d/%Y %I:%M:%S %p", tz = Sys.timezone()))

daily_sleep1 <- daily_sleep %>%
  rename(date_time = sleepday) %>% 
  mutate(date_time = as.POSIXct(date_time, format = "%m/%d/%Y %I:%M:%S %p", tz = Sys.timezone()))

heartrate_seconds1 <- heartrate_seconds %>%
  rename(date_time = time) %>% 
  mutate(date_time = as.POSIXct(date_time, format = "%m/%d/%Y %I:%M:%S %p", tz = Sys.timezone()))
```
- Let us preview our datasets again to see the structure of the colume names and the data_time column

```R
str(daily_activity_2)
str(hourly_steps1)
str(daily_sleep1)
str(heartrate_seconds1)
```

```R
'data.frame':	457 obs. of  15 variables:
 $ id                      : num  1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
 $ date                    : Date, format: "2016-03-25" "2016-03-26" "2016-03-27" ...
 $ totalsteps              : int  11004 17609 12736 13231 12041 10970 12256 12262 11248 10016 ...
 $ totaldistance           : num  7.11 11.55 8.53 8.93 7.85 ...
 $ trackerdistance         : num  7.11 11.55 8.53 8.93 7.85 ...
 $ loggedactivitiesdistance: num  0 0 0 0 0 0 0 0 0 0 ...
 $ veryactivedistance      : num  2.57 6.92 4.66 3.19 2.16 ...
 $ moderatelyactivedistance: num  0.46 0.73 0.16 0.79 1.09 ...
 $ lightactivedistance     : num  4.07 3.91 3.71 4.95 4.61 ...
 $ sedentaryactivedistance : num  0 0 0 0 0 0 0 0 0 0 ...
 $ veryactiveminutes       : int  33 89 56 39 28 30 33 47 40 15 ...
 $ fairlyactiveminutes     : int  12 17 5 20 28 13 12 21 11 30 ...
 $ lightlyactiveminutes    : int  205 274 268 224 243 223 239 200 244 314 ...
 $ sedentaryminutes        : int  804 588 605 1080 763 1174 820 866 636 655 ...
 $ calories                : int  1819 2154 1944 1932 1886 1820 1889 1868 1843 1850 ...

> str(hourly_steps1)
'data.frame':	24084 obs. of  3 variables:
 $ id       : num  1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
 $ date_time: POSIXct, format: "2016-03-12 00:00:00" "2016-03-12 01:00:00" "2016-03-12 02:00:00" ...
 $ steptotal: int  0 0 0 0 0 0 0 0 0 8 ...

> str(daily_sleep1)
'data.frame':	24 obs. of  5 variables:
 $ id                : chr  "1503960366" "1644430081" "1844505072" "1927972279" ...
 $ date_time         : POSIXct, format: NA "2016-04-29" "2016-04-15" ...
 $ totalsleeprecords : int  1 1 1 3 1 1 1 1 1 1 ...
 $ totalminutesasleep: int  327 119 644 750 503 61 467 274 501 535 ...
 $ totaltimeinbed    : int  346 127 961 775 546 69 531 469 541 557 ...

> str(heartrate_seconds1)
'data.frame':	1154681 obs. of  3 variables:
 $ id       : num  2.02e+09 2.02e+09 2.02e+09 2.02e+09 2.02e+09 ...
 $ date_time: POSIXct, format: "2016-04-01 07:54:00" "2016-04-01 07:54:05" "2016-04-01 07:54:10" ...
 $ value    : int  93 91 96 98 100 101 104 105 102 106 ...
```
As observed, the changes have been successfully applied. The column names are now in lowercase, and the date_time columns have been converted to a format readable by R.

- Now that the date$time are in the right format recognizable by R, I will go ahead to separate the date_time column in hourly_steps1 into separate columns of date and time.

```R
library(tidyr)
library(dplyr)

hourly_steps2 <- hourly_steps1 %>%
  separate(date_time, into = c("date", "time"), sep = " ", fill = "right")  # Fills missing parts with NA

str(hourly_steps2)
```

- Outcome of the Separate Function

```R
$ id       : num  1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
 $ date     : chr  "2016-03-12" "2016-03-12" "2016-03-12" "2016-03-12" ...
 $ time     : chr  NA "01:00:00" "02:00:00" "03:00:00" ...
 $ steptotal: int  0 0 0 0 0 0 0 0 0 8 ...
```
I am done with data exploration. It is time to analysis the datasets to find hidden insights therein.

### Data Analysis

- I will use the daily_activity_2 to find the average of the daily steps taken by each user, group_by id as well as daily calories. Then, I will use the daily_sleep1 dataset to calculate the average of the minutesassleep by each user.

```R
daily_average <- daily_activity_2 %>% 
  group_by(id) %>% 
  summarise(mean_daily_steps = mean(totalsteps), mean_daily_calories = mean(calories))

avearge_sleep <- daily_sleep1 %>% 
  group_by(id) %>% 
  summarise(mean_daily_sleep = mean(totalminutesasleep))
```

- For ease of reference, I will merge the daily_average $ average_sleep datasets.

```R
daily_average1 <- merge(daily_average, avearge_sleep,by=c("id"),all=TRUE)
```

| id | mean_daily_steps | mean_daily_calories | mean_daily_sleep |
| ----------- | ----------- | ----------- | ----------- |
| 1503960366 | 11640.526 | 1796.211 | 360.2800 |
| 1644430081 | 9274.800 | 2916.400 | 294.0000 |
| 1844505072 | 3640.583 | 1615.917 | 652.0000 |
| 1927972279 | 2180.833 | 2254.000 | 417.0000 |
| 2026352035 | 3392.750 | 1355.500 | 506.1786 |
| 2320127002 | 3138.417 | 1532.083 | 61.0000 |
| 2347167796 | 9800.067 | 2021.333 | 446.8000 |
| 3977333714 | 8663.917 | 1398.083 | 293.6429 |
| 4020332650 | 5776.594 | 3075.375 | 349.3750 |
| 4319703577 | 7820.583 | 1994.250 | 476.6538 |
Showing 1 to 10 of 24 enteries

- Having calculated the average daily steps, calories, and sleep for each user, I now aim to group the users into four activity categories: Sedentary, Lightly Active, Fairly Active, and Very Active. This classification will help identify how many users fall into each category based on their daily activity levels.
To achieve this, I will use the mean_daily_steps as the primary metric. First, I will determine the minimum and maximum values of the mean_daily_steps to better understand the data distribution and define appropriate step thresholds for each category.

```R
min_daily_step <- daily_average1 %>%
  filter(mean_daily_steps > 0) %>%
  summarise(min_daily_step = min(mean_daily_steps, na.rm = TRUE))  

max_daily_step <- daily_average1 %>%
  filter(mean_daily_steps > 0) %>%
  summarise(max_daily_step = max(mean_daily_steps, na.rm = TRUE))
```
- Outcome
  
1. **min_daily_step = 773.625**
2. **max_daily_steps = 17417.08**

- Next, is to calculate thresholds 

```R
step_range <- max_daily_step - min_daily_step
increment <- step_range / 4
```

- Thresholds for categories
  
```R
thresholds <- c(
  min_daily_step,
  min_daily_step + increment,
  min_daily_step + 2 * increment,
  min_daily_step + 3 * increment,
  max_daily_step
)
```

```R
user_type <- daily_average1 %>% 
  mutate(user_type = case_when(
    mean_daily_steps <= thresholds[2] ~ "sedentary",
    mean_daily_steps <= thresholds[3] ~ "lightly active",
    mean_daily_steps <= thresholds[4] ~ "fairly active",
    TRUE ~ "very active"
  ))
```



