# Ames, Iowa Housing Analysis

## Overview

### Problem Statement

- What are the factors that affect Ames’ housing price in the past?
- How accurately could we predict the trend of housing market using existing information and past data? 

### Primary Objective

Use existing data and sales price to train a predictive model and predict sales price for houses with unknown sales price

## Dataset

### dataset overview

The dataset includes housing sales data in Ames Iowa from 2006 to 2010. The data has 81 columns and 2051 rows in train dataset and 80 columns and 878 rows in test dataset


### dataset source

The raw data is from Kaggle competition. The dataset could be accessed at https://www.kaggle.com/c/dsi-us-10-project-2-regression-challenge/data

## EDA

### Data Cleaning

1. Drop all the columns with null values more than 1000
2. Fill in columns with null values based on columns' categories or relative scales
3. Clear outliers with exceptionally large values such as 'Ground Living Area'


### Visualization

1. Check overall distribution of Sales Price
2. Visualize distribution of sales price by Neighborhood based on neighborhood category, year built, and overall quality

- Package used: Matplotlib.pyplot, seaborn

## Model Selection

### Model 1: use only numeric variables

#### Method used:

1. Linear Regression
2. Lasso
3. Ridge
4. Ridge CV
5. Elastic Net

#### Conclusion:
In Model 1, I selected all numeric variable from the dataset into the model. For each method, I split data into 70% training and 30% testing, and set cross validation to 5 times per method. By measuring RMSE, R2 score for both training and testing, I select the method with lowest RMSE and highest R2 testing with smallest difference between R2 training and testing. I conclude that Ridge CV has the most accurate prediction.

### Model 2: use high correlated numeric variables and add interaction and sqaured terms

#### Method used:

1. Linear Regression
2. Lasso
3. Ridge
4. Ridge CV

#### Conclusions:
In Model 2, I select only high correlated numeric variables from model 1. I used a heatmap to visualize all variables' correlation with sales price, and selected variables with absolute values of correlation higher than 0.5. Through the correlation analysis, I found out some predictor variables have high correlations with each other, so I added their interaction terms to the model. Also, by plotting residuls from model 1, I found out that the plot shows a pattern of a parabola shape. As a result, I added all included variables' squared value into the model as well. Ridge CV continues to be the best fit method. However, compare to Model 1, the accuracy of prediction in Model 2 merely increased very little.

### Model 3: Model 2 improvement with high correlated scaled classification variables

#### Method used:

1. Linear Regression
2. Ridge CV
3. Pipeline gridsearch

#### Conclusion:

In Model 3, I turned ordinal classification variables to numeirc scale, which turned them into numeric variables. Then I conducted correlation analysis on all numeric variables again and select high correlated variables with sale price. (correlation > 0.5), repeat the process for model 2. Ridge CV and Pipeline gridsearch both have the highest R2 score and low RMSE while the difference between R2 training and R2 testing is small. The prediction result also improved significantly.

### Model 4: Model 3 improvement with scaled Neighborhood and log sale price

#### Method used:

1. Linear Regression
2. Ridge CV

####  Conclusion:

In Model 4, I added log value on sales price to make its distribution closer to fit normality. Then based on the median sale price, I scaled all Neighborhood from the highest median sales price to lowest median sales price. The prediction result was a bit worse than model 3 pipeline, so I might included some low correlated variables in the model.

## Summary 

- Model 3 with pipeline method has the highest accuracy of predicting sales price
- The prediction model tends to undervalue extremely expensive houses

## Slide Link

https://drive.google.com/file/d/1PUx15Evh_m84E4RLdQKiFr5rn-FC4JBl/view?usp=sharing
# ames_housing_price
