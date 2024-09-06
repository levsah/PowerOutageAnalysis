# Analyzing the impacts of Power Outages caused by Natural Disasters across different regions in the US
This is a data science project on if power outages are more likely to effect costal states more than inward states.

Github Pages Deliverable: https://kewlerkids.github.io/outageanalysis/

**Authors**: [Aile Banuelos](https://github.com/kewlerkids), [Levy Sahoo](https://github.com/levsah)

---

## Introduction

Welcome to our exploration of how severe weather affects power outages in the United States. Our analysis dives into a comprehensive dataset to uncover patterns between whether the location of a state matters in comparison to the amount of power outages they get. We will mainly be analyzing if there is a percentage increase in power outages for outer states compared to the number of power outages we see with inward states. While looking at outage raw numbers we will also be looking at outage duration to ensure our model is correctly ran.

## Project Overview:
This project investigates [Is the number of power outages and duration something that is affected by the location of a state?], utilizing data from [Outage]. The dataset consists of [1534] records and includes key columns such as:

|Column	                 |Description|
|---                     |---        |
|`'Year'	`            |The year the outage occured|
|`'Month'`	                 |The month of the year the outage occurred |
|`'U.S._State'`	         |The state our outage occurred in|
|`'Climate.Region'`	     |The region of the US that this state is in|
|`'Anomaly.level'`	            |How much of an anomaly this power outage was |
|`'Outage.Duration'`	              |How long the outage lasted|

Why This Matters: If you want to get a new home somewhere but want to have reliable power this could be useful. As well as people living in those areas can try to be better prepared if they are in a region that gets very frequent as well as long-lasting power outages. Company wise if companies wanted to put their focus more towards those areas that get outages more often to help they could also check and be able to increase their power out put or take precautionary measures.


# Data Cleaning and Exploratory Data Analysis
### Data Cleaning Process

We made a new data frame with only the rows that had severe weather in them. We also took out rows where both CUSTOMERS.AFFECTED  and OUTAGE.DURATION was empty/na because we want to reduce missingness in the main features we want to analyze. Below are the first few rows we have included into our cleaned data frame.


 | EVENT    |     YEAR |     MONTH |    U.S._STATE |    POSTAL |    NERC |    CLIMATE.REGION |
|:-------------|-----------:|-----------:|----------:|----------:|----------:|----------:|
| 1   | 2011   | 7 | Minnesota | MN | MRO | East North Central |
| 2  | 2010   | 10 |  Minnesota | MN |  MRO | East North Central |
| 3  | 2012  | 6 | Minnesota | MN | MRO | East North Central |
| 4  | 2015  | 7 | Minnesota | MN | MRO | East North Central |
| 5 | 2010 | 11 | Minnesota | MN | MRO | East North Central |
| 6  | 2010 | 7 | Minnesota | MN | MRO | East North Central |
| 7 | 2005  | 6 | Minnesota | MN | MRO | East North Central |
| 8 | 2013 |  6 | Minnesota | MN | MRO | East North Central |
| 9  | 2013  |  6 | Minnesota | MN | MRO | East North Central |
| 10 | 2005  |  9 | Minnesota | MN | MRO | East North Central |

|    ANOMALY |    CATEGORY |  START.DATE |    START.TIME |
|----------:|----------:|----------:|----------:|
| -0.3 | normal | 2011-07-01 | 17:00:00 |
| -1.5 | cold | 2010-10-26 | 20:00:00 |
| -0.1 | normal | 2012-06-19 | 4:30:00 |
| 1.2 | warm | 2015-07-18 | 2:00:00 |
| -1.4 | cold | 2010-11-13 | 15:00:00 |
| -0.9 | cold | 2010-07-17 | 20:30:00 |
| 0.2 | normal | 2005-06-08 | 4:00:00 |
| -0.2 | normal | 2013-06-21 | 17:39:00 |
| -0.2 | normal | 2013-06-21 | 3:00:00 |
| 0 | normal | 2005-09-21 | 19:00:00 |

![image](https://github.com/kewlerkids/outageanalysis/assets/42384002/162aec82-339b-4488-987b-3835cfe95489)

### Univariate Analysis
We wanted to create a pivot table of all types of power-outage causes to show the trend between the customers affected compared to this. Please view the pivot table below.

![newplot](https://github.com/kewlerkids/outageanalysis/assets/42384002/8445ec06-4e21-4c07-bb02-b8f42388fd70)


Out of all the power outages, we added all the minutes for each type. We noticed that 75% of power outages were caused by severe weather, which can be seen through here.
 
### Bivariate Analysis
We created scatter plots to compare the number of power outages in the states. With this, we compared the power outage total to the outage duration. With these two numerical features, we wanted to access similar features by finding the R^2 and comparing it to other features. With the R^2 of numerical features, we compared this to the number of power outages per state. To access which features have the best correlation with the number of power outages per state we filter out numerical features from serve weather df. 
![newplot (2)](https://github.com/kewlerkids/outageanalysis/assets/42384002/c3a61838-867f-47ef-bbbb-008d3ed4fb55)

We realized we couldn't perform the same aggregation on all numerical features so we split the features by their aggregation method into two lists. We wanted to find the correlation of each feature per aggregation method with the number of power outages per state. So we can try to see if they are at all related. After we compared the R^2 values to the rank of each group within the two lists. We took the top three features with the best R^2 from each group and determined the best features to compare the number of power outages per state. Then we asked how the correlations of the features we took the sums of compare to the average. We realized that the features that we aggregated with the sum had a much larger R^2, so we stuck with the sum. We already compared the number of power outages per state and the outage duration and coincidently outage duration happened to be a feature with one of the best R^2. So we compared the number of power outages with the other top two features. With this, we made scatter plots with the two top features we had.

### Interesting Aggregates
As the number of power outages what happens to the other features and why? So when we increase the number of power outages the number of customers also increases, and while it makes sense to think that at first, it was nice to see that this was also shown within the data.
![newplot (5)](https://github.com/kewlerkids/outageanalysis/assets/42384002/1f1ebcdb-f336-48c2-9cb9-145d397eef6a)
![newplot (7)](https://github.com/kewlerkids/outageanalysis/assets/42384002/15c7e988-c3c9-4edc-ba21-3a16764de2c2)


# Assessment of Missingness
We had started with a lot of missingness within our data but through our data cleaning process, we were able to reduce or remove the amount of missingness that would have been prevalent. Yet we still found features with missingness dependencies. Such as the customers affected feature, we found that this feature was not missing at random
![newplot (3)](https://github.com/kewlerkids/outageanalysis/assets/42384002/b5eb997d-3139-433a-9198-bd81370f0151)
![newplot (4)](https://github.com/kewlerkids/outageanalysis/assets/42384002/4d95089f-98e7-431b-a894-8c1dadd0d5b1)
### NMAR Analysis
It was not missing a random because the P-value we received was high, which suggests our columns are independent of each other. There is a high probability that the missingness of customers affected is not related to how long a power outage lasts.

### Missingness Dependency
However, when we compare coustmers affected to another column, such as population we have evidence to show that we shouldn't rule out the possibility of customers affected being dependent on the population since the P-value is low.

# Hypothesis Testing
Null Hypothesis: There is no difference in the average number of power outages between coastal states and non-coastal states. By coastal we mean anything on the outer border vs the inner border of the country.
Alternate Hypothesis: There is a difference in the average number of power outages between coastal states and non-coastal states.
![image](https://github.com/kewlerkids/outageanalysis/assets/42384002/38823f95-2177-48c4-ac56-f7626131d289)![image](https://github.com/kewlerkids/outageanalysis/assets/42384002/47aee95b-8823-4fec-b5b5-7b30524f5102)


Our P-value is greater than our alpha level of .05 so we fail to reject the null.
![unnamed](https://github.com/kewlerkids/ailelevy.github.io/assets/42384002/ac3d1dcf-4dae-430a-808e-a043c8b5fafd)


# Framing a Prediction Problem
### Problem Identification
We will be predicting the number of power outages per year by incident. What we know is the year and the cause category that we can use to predict the number of power outages per year by cause category.

# Baseline Model
For quantitative we wanted to predict count, however, count is the only numerical feature and the rest are technically categorical. We made a new feature called random number and that randomizes different. We assign them for each record in the data frame. The purpose is to randomly split the data into training and test sets so that we can introduce randomness. Then we created a list of categorical columns and we also made a list of past-through columns to transform the features that we wanted to transform. We one hot encoded the categorical columns. This is how we created our pipeline data with one hot encoded data. We then fitted the model got the transformed data and then split the data into training and test sets with a test size of 20% or 0.2 and a random state of 42. Then we wanted to compare multiple models so the first one we compared was linear regression after predicting the values of the count of the number of power outages per year by cause category we got an R^2 value of .5 meaning 51% of the variability is cause the features that we analyzed. Now we want to test with the random force classifier and we found the R^2 value was 0! 

# Final Model
How can we make our model better?

We couldn't! After attempting to implement a standard scaler the quantile transformer and tuning the hyperparameters of our perma_grid with a cross-validation value of 5. We were unable to obtain a high R^2.

# Fairness Analysis
We got a root mean squared error of 24 between our y test set and our y prediction set. After running a permutation test we found a P-value of 0.95 which gives us reason to assume that our model overfits our validation set.

---
# Conclusion

Our analysis offers insightful findings on the impact of severe weather on power outages. With this information, we are able to see that there is a correlation between being a costal or outer state compared to an inner state and does not imply an increase in power outages to the outer states.

