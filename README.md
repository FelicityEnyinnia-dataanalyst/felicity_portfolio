# Playing it Smart: Data-Driven Insights for a Wellness Tech Company

## Table of Contents
---
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Load R Packages](#load-r-packages)
- [Import Dataset into RStudio](#import-dataset-into-rstudio)
- [Data Cleaning and Preprocessing - Exploratory Data Analysis](#data-cleaning-and-preprocessing)
- [Data Analysis](#data-analysis)
- [Recommendations](#recommendations)


## Project Overview
---

This data analysis project is being completed as part of the Google Data Analytics Capstone Project. In this simulation, I am acting as a junior data analyst on the marketing analytics team at Bellabeat. Bellabeat is a high-tech company that manufactures health-focused smart devices. The Chief Creative Officer (CCO) of Bellabeat has tasked me with analyzing smart device data available on Kaggle to identify opportunities for the company's growth.
The primary objective is to uncover insights about how Bellabeat consumers are using their smart devices to support their fitness journeys. My findings from this analysis will form the basis of data-driven recommendations that I will present to the CCO, which will help Bellabeat optimize its product offerings and marketing strategies to better meet consumer needs and expand its market presence.

## Data Sources
---

FitBit Fitness Tracker Data [Download here](https://www.kaggle.com/datasets/arashnic/fitbit): This public dataset, sourced from Kaggle, contains personal fitness tracking data from 30 Fitbit users. It captures a variety of metrics, including:
- Daily Steps: Records of users' daily step counts.
- Sleep Patterns: Information on sleep duration and quality.
- Calories Burned: Daily caloric expenditure.
- Heart Rate: Heart rate monitoring data.
   
## Tools
---

- Excel 
- R Programming Language - Data Claening, Analysis and Visualization.
I mostly utilized R in this data analysis. However, Excel was useful in previewing the dataset after I downloded it from Kaggle.

# Load R Packages
---

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

## Import Dataset into RStudio
---

The dataset for this analysis is downloaded from Kaggle.Rather than using the readr package to import the dataset directly from Kaggle into R, I downloaded the dataset to my laptop and thereafter, uploaded and imported into RStudio using the following codes:

```R
dailyActivity_merged <- read.csv("Fitabase Data 3.12.16-4.11.16/dailyActivity_merged.csv")
hourly_steps <- read.csv("Fitabase Data 3.12.16-4.11.16/hourlySteps_merged.csv")
daily_sleep <- read.csv("Fitabase Data 3.12.16-4.11.16/daily_sleep_merged.csv")
heartrate_seconds <- read.csv("Fitabase Data 3.12.16-4.11.16/heartrate_seconds_merged.csv")
```

## Preview Data set

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


## Data Cleaning and Preprocessing
---

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


### Locate duplicate values in the datasets.

I want to check for duplicate values in the datasets.

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

### Clean and Rename Column Names
- I want to rename and format the column names. This is to ensure that the column names are using the right syntax and consistent considering that I may decide to merge the datasets subsequently, to discover trends and correlations. I will use the clean_names and rename_with functions to convert the column names to lowercase.

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

### Consistency of Date and Time

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
At this point, I am done with data exploration. It is time to analysis the datasets to find hidden insights therein.

## Data Analysis
---

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
**Outcome**
  
1. **min_daily_step = 773.625**
2. **max_daily_steps = 17417.08**

- Now that we have the min_daily_step$max_daily_steps, we will utilize same to set the criteria for distributing our users into the above four activity levels.  

```R
step_range <- max_daily_step - min_daily_step  # 16,643.46
increment <- step_range / 4                    # 4,160.865
```
The result step_range gives the total spread of step counts in the dataset.
Increment divides the step_range by 4 to create equal intervals for categorizing users into four activity levels. This means that each category covers a 4,160.865 step_range.

- Now, let us define the thresholds for the categories
  
```R
thresholds <- c(
  min_daily_step,
  min_daily_step + increment,
  min_daily_step + 2 * increment,
  min_daily_step + 3 * increment,
  max_daily_step
)
```
| thresholds | list[5] | list of length |
| ----------- | ----------- | ----------- |
| min_daily_step | double [1] | 773.625 |
| min_daily_step | double [2] | 4934.49 |
| min_daily_step | double [3] | 9095.354 |
| min_daily_step | double [4] | 13256.22 |
| max_daily_step | double [5] | 17417.08 |

Now that we have arrived at the threshold for categoring our users into the identified activity levels, lets dive into it. 

```R
user_type <- daily_average1 %>% 
  mutate(user_type = case_when(
    mean_daily_steps <= thresholds[2] ~ "sedentary",      # if a user's daily steps are less than or equal to the value of thresholds [2], classify them as "sedentary" 
    mean_daily_steps <= thresholds[3] ~ "lightly active", # steps within thresholds [3], classify them as "lightly active"
    mean_daily_steps <= thresholds[4] ~ "fairly active",  # seps within threholds [4], classify them as "fairly active"
    TRUE ~ "very active"                                  # any remaining values fall into "very acrive" category.
  ))
```
Here is the outcome of the above analysis:
| id | mean_daily_steps | mean_daily_calories | mean_daily_sleep | user_type |
| ----------- | ----------- | ----------- | ----------- | ----------- 
| 1503960366 | 11640.526 | 1796.211 | 360.2800 | fairly active |
| 1644430081 | 9274.800 | 2916.400 | 294.0000 | fairly active |
| 1844505072 | 3640.583 | 1615.917 | 652.0000 | sedentary |
| 1927972279 | 2180.833 | 2254.000 | 417.0000 | sedentary |
| 2026352035 | 3392.750 | 1355.500 | 506.1786 | sedentary |
| 2320127002 | 3138.417 | 1532.083 | 61.0000 | sedentary |
| 2347167796 | 9800.067 | 2021.333 | 446.8000 | fairly active |
| 3977333714 | 8663.917 | 1398.083 | 293.6429 | lightly active |
| 4020332650 | 5776.594 | 3075.375 | 349.3750 | lightly active |
| 4319703577 | 7820.583 | 1994.250 | 476.6538 | lighly active |
showing 1 to 10 of 24 enteries

- Visualization of the outcome of the user_type using ggplot2 (Bar chart):  

```R
library(ggplot2)
ggplot(user_distribution, aes(x = user_type, y = total_percent, fill = user_type)) +
  geom_bar(stat = "identity") + # Use identity since you've already calculated the values
  geom_text(aes(label = labels), vjust = -0.5) + # Add percentage labels above bars
  scale_y_continuous(labels = scales::percent) + # Format y-axis as percentages
  scale_fill_manual(values = c("#66c2a5", "#fc8d62", "#8da0cb", "#e78ac3")) + # Four colors
  labs(
    title = "User Type Distribution",
    x = "User Type",
    y = "Percentage",
    fill = "User Type"
  )
```

![bar char](https://github.com/user-attachments/assets/349cc605-b3c3-49a1-aab0-139d65bdad0b)

**Findings/Outcome**

The visualization reveals that a higher percentage of smart device users engage in sedentary activity, followed by lightly active, fairly active, and very active users. Based on this finding, I recommend that Bellabeat introduce reminders to encourage sedentary users to take short walks and stay active throughout the day. Gamified challenges and personalized goals can motivate users to gradually increase their daily activity levels. Additionally, providing educational content on the health benefits of regular movement can help users make informed decisions to improve their fitness habits from sedendary to at aleast fairly active.


### Finding Correlations

- I want to discover if there are correlation between the following different variables:
  
  - **Daily steps and daily sleep**
  - **Daily steps and calories**
  
**Note**: totalminutesasleep is not in the daily_activity_2 dataset. So, I will merge daily_activity_2 and daily_sleep1 as daily_activity_1 for ease of reference. For this, I will perform the following analysis to ensure that:

- Ensure 'id' columns are consistent in daily_activity_2 & daily_sleep1.
- Remove duplicate valuse from the two datasets.
- Remove missing values in 'id'
- Thereafter, I will merge the two datasets for easy analysis. 
  

```R
library(dplyr)

# Ensure 'id' columns are consistent
daily_activity_2$id <- as.character(daily_activity_2$id)
daily_sleep1$id <- as.character(daily_sleep1$id)

# Remove duplicates
daily_activity_2 <- daily_activity_2 %>%
  distinct(id, .keep_all = TRUE)

daily_sleep1 <- daily_sleep1 %>%
  distinct(id, .keep_all = TRUE)

# Remove missing values in 'id'
daily_activity_2 <- daily_activity_2 %>% filter(!is.na(id))
daily_sleep1 <- daily_sleep1 %>% filter(!is.na(id))

# Merge datasets
daily_activity_1 <- merge(daily_activity_2, daily_sleep1, by = "id", all = TRUE)
```
All done. I will go ahead to preview daily_activity_1

```R
head(daily_activity_1)
```
**Result**

```R
 id       date totalsteps totaldistance trackerdistance loggedactivitiesdistance
1 1503960366 2016-03-25      11004          7.11            7.11                        0
2 1624580081 2016-03-25       1810          1.18            1.18                        0
3 1644430081 2016-04-01       4636          3.41            3.41                        0
4 1844505072 2016-04-01       6847          4.53            4.53                        0
5 1927972279 2016-04-01       4317          2.99            2.99                        0
6 2022484408 2016-04-01      13603          9.60            9.60                        0
  veryactivedistance moderatelyactivedistance lightactivedistance sedentaryactivedistance
1               2.57                     0.46                4.07                    0.00
2               0.00                     0.00                1.13                    0.01
3               0.00                     0.78                2.60                    0.03
4               0.61                     0.37                3.55                    0.00
5               0.00                     0.37                2.62                    0.00
6               5.46                     0.63                3.51                    0.00
  veryactiveminutes fairlyactiveminutes lightlyactiveminutes sedentaryminutes calories  date_time
1                33                  12                  205              804     1819       <NA>
2                 0                   0                  121             1319     1373       <NA>
3                 0                  16                  586              838     3323 2016-04-29
4                 9                   9                  251             1171     1969 2016-04-15
5                 0                  11                  192              854     2590       <NA>
6                72                  16                  213             1139     2645       <NA>
  totalsleeprecords totalminutesasleep totaltimeinbed
1                 1                327            346
2                NA                 NA             NA
3                 1                119            127
4                 1                644            961
5                 3                750            775
6                NA                 NA             NA

```

### Finding correlations with ggplot2

I want to visualize the daily_activity_1 dataset to find the relationship betweeen:

1. **Daily Steps and Sleep**.

```R
ggplot(daily_activity_1, aes(x = totalminutesasleep, y = totalsteps )) +
  geom_jitter() +
  geom_smooth(color = "blue") +
  labs(title = "Relationship Between Daily Steps and Sleep", x = "Sleep Duration (minutes)", y = "Daily Steps")+
  theme(panel.background = element_blank(),
        plot.title = element_text(size=15))
```

![dailysteps sleep](https://github.com/user-attachments/assets/ae204668-613e-4abb-891a-55ee23e24fcf)


2. **Daily Steps and calories**.

```R
ggplot(daily_activity_1, aes(x = totalsteps, y = calories)) +
  geom_jitter() +
  geom_smooth(color = "blue") +
  labs(title = "Relationship Between Daily Steps and Calories", x = "Daily Steps", y = "Calories")+
  theme(panel.background = element_blank(),
        plot.title = element_text(size=15))
```

![dailysteps$calories](https://github.com/user-attachments/assets/d36691cd-0c53-4fd2-b7fe-c875fd783cde)

3. **Daily Sleep and Calories**.
   
```R
ggplot(daily_activity_1, aes(x = totalminutesasleep, y = calories)) +
  geom_jitter() +
  geom_smooth(color = "blue") +
  labs(title = "Relationship Between Daily Sleep and Calories", x = "Sleep Duration (minutes)", y = "Calories")+
  theme(panel.background = element_blank(),
        plot.title = element_text(size=14))
```

![dailysleep calories](https://github.com/user-attachments/assets/d06e7e39-8655-4adc-b53a-aa02d602d739)

**Outcome/Findings of the above viz**

1. There is no correlation between daily activity level based on steps and the length of minutes users sleep a day.
2. There is a positive correlation between steps and calories burned. This means that the more steps walked by users the more calories burn.
3. There is no correlation between the amount of minutes users sleep a day and calories burned.
- Since there is a positive correlation between steps and calories burned, Bellabeat can introduce features that highlight and track daily calorie burn based on step goals. This approach will inspire users to engage more in daily walks, as it enables calories loss and overall fitness.
- Since sleep length does not correlate with calorie burn, sleep tracking can be positioned as a general wellness tool. Additionally, Bellabeat can encourage users to view sleep data alongside other indicators like stress, which can negatively impact sleep habits.


### Active Hour of the Day

- I want to calculate the hour of the day when users are more active based on steps taken.

```R
hourly_steps2 %>%
  group_by(time) %>% 
  summarise(averagesteps = mean(steptotal, na.rm = TRUE)) %>%
  ggplot(aes(x = time, y = averagesteps)) +
  geom_line(group = 1, color = "green") +
  labs(title = "Hourly Steps Throughout the Day", x = "time", y = "averagesteps")
```

- Viz hourly activity with ggplot2

```R
hourly_steps2 %>%
  group_by(time) %>% 
  summarise(averagesteps = mean(steptotal, na.rm = TRUE)) %>%
  ggplot(aes(x = time, y = averagesteps)) +
  geom_line(group = 1, color = "green") +
  labs(title = "Hourly Steps Throughout the Day", x = "time", y = "averagesteps")
```

![activityhour](https://github.com/user-attachments/assets/6a582a78-daed-488e-9b84-016ada290cce)

**Outcome**:

- The visualization shows that users are more active between 8 am and 7 pm, with peak activity during lunchtime (12 pm to 2 pm) and evenings (5 pm to 7 pm).
- Given the positive correlation between steps and calories burned, I recommend that Bellabeat introduce a feature reminding users that calories are effectively burned during these key periods. This approach will encourage users to stay more active and take advantage of these peak activity times.


### Active Days of the Week

I want to determine which days of the week users are more active based on steps taken.

```R
daily_activity_1 %>%
  mutate(weekday = weekdays(date)) %>%         
  group_by(weekday) %>%
  summarise(averagesteps = mean(totalsteps, na.rm = TRUE)) %>%
  ggplot(aes(x = reorder(weekday, averagesteps), y = averagesteps)) +  
  geom_bar(stat = "identity", fill = "steelblue") +
  labs(title = "Average Steps by Day of the Week", x = "Day", y = "Average Steps")
```
- viz active days with ggplot2
  
![active_day](https://github.com/user-attachments/assets/0934af7f-98b1-46af-9119-1919a78923a6)

**Outcome**: 

Users walk more steps on Wednesdays. The average of users walk more than 7,500 steps daily besides Tuesday. 

### Sleep Days

I want to calculate which days of the week users sleep the most.
  
```R
daily_activity_1 %>%
  mutate(weekday = weekdays(date)) %>%         # Ensure 'weekday' is lowercase
  group_by(weekday) %>%
  summarise(averagesleep = mean(totalminutesasleep, na.rm = TRUE)) %>%
  ggplot(aes(x = reorder(weekday, averagesleep), y = averagesleep)) +  # Use 'weekday'
  geom_bar(stat = "identity", fill = "purple") +
  labs(title = "Average Sleep by Day of the Week", x = "Day", y = "Average Sleep")
```

- viz sleep days withh ggplot2

![sleep_day](https://github.com/user-attachments/assets/a89ae00e-1b90-45ba-bc3e-b703a7aeed87)

**Outcome**: 

Users tend to sleep longer on weekends, particularly Saturdays, but typically sleep between 5 to 8 hours daily, which aligns with a healthy sleep pattern for adults as recommended by science. To support users in maintaining this routine, I recommend that Bellabeat introduce a feature that educates users on the health benefits of achieving the ideal 6 to 8 hours of sleep. Additionally, Bellabeat could implement a tool to help users track and maintain a consistent daily sleep schedule.

### Sleep Efficiency

I want to determine the sleep efficiency of users.

```R
ggplot(daily_sleep1, aes(x = totalminutesasleep, y = totaltimeinbed)) +
  geom_point(alpha = 0.6) +
  geom_abline(slope = 1, intercept = 0, color = "red") +
  labs(title = "Sleep Efficiency", x = "Minutes Asleep", y = "Time in Bed")
```

- viz sleep efficiency with ggplot2
  
![sleep_efficiency](https://github.com/user-attachments/assets/bae7affc-cb47-4def-9101-e4df990aa52c)

**Outcome**: There is a positive relationship between time in bed and minutes asleep, suggesting that users generally spend their time in bed sleeping. Bellabeat can leverage this pattern by introducing a smart feature that tracks sleep duration and provides a gentle alert or bip once users achieve the recommended minimum of 6 hours of sleep. This approach can encourage healthier sleep habits and help users meet the 6 to 8-hour sleep guideline.  

### Recommendations
---

1. I recommend that Bellabeat introduce reminders to encourage sedentary users to take short walks and stay active throughout the day. Gamified challenges and personalized goals can motivate users to gradually increase their daily activity levels. Additionally, providing educational content on the health benefits of regular movement can help users make informed decisions to improve their fitness habits from sedendary to at aleast fairly active.
   
2. From our analysis, we observed that users generally walk over 7,500 steps daily, except on Tuesdays. This is commendable. However, Bellabeat could further encourage users to consistently meet the daily recommended step count of 7,000 to 8,000 steps as suggested by the World Health Organization (WHO), American Heart Association (AHA), and Centers for Disease Control and Prevention (CDC). This can be achieved by sharing motivational health tips on the smart devices, highlighting the benefits of reaching the daily recommended step target.
   
3. Since there is a positive correlation between steps and calories burned, Bellabeat can introduce features that highlight and track daily calorie burn based on step goals. This approach will inspire users to engage more in daily walks, as it enables calories loss and overall fitness.
   
4. I recommend that Bellabeat introduce a feature that educates users on the health benefits of achieving the ideal 6 to 8 hours of sleep. Additionally, Bellabeat could implement a tool to help users track and maintain a consistent daily sleep schedule.

