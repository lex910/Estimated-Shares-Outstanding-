# Estimated-Shares-Outstanding-
Utilizing linear regression and false discovery rate to evaluate models to predict estimated shares outstanding 

## 1. Data Exploration and Visualization:
{'Number of Rows': 1781,
 'Number of Columns': 78,
 'Number of Companies': 448,
 'Date Range': ('2003-06-30', '2017-01-01')}


The correlation heatmap of a subset of variables shows that some are highly correlated. This may lead to multicolinearilty and will need to be handled to obtain accurate model results
<img width="684" alt="Screenshot 2024-06-19 at 10 52 41 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/52a80acb-5e70-4ce4-8c9a-4f5060b68b63">

Now we will vizualize trends in total revenue, total assets, and earnings per shared varied across the scope of the dataset. I will use Apple (AAPL) in specific to conduct this analysis

<img width="1057" alt="Screenshot 2024-06-19 at 10 53 09 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/b0049b45-1870-47aa-870d-ccd773a51a2c">

Total Revenue for Apple showed an upward trend until 2015 and then started to fall going into 2016. Total assets steadily increasd while earnings per share dramatically decreased from 2013-2014 and have stayed consistent since.


#### Bar charts for the top 10 companies in Total revenue, total assats, and earnings per share
<img width="786" alt="Screenshot 2024-06-19 at 10 55 05 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/367da11a-51e6-435c-8db9-6cbf34e66521">
From the bar chart, we can see that walmart has the highest total revenue in 2015 followed by Exxon and then Apple.

<img width="802" alt="Screenshot 2024-06-19 at 10 55 53 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/e587a656-9245-429f-8759-bed4fcdca33c">
The bar chart of the top 10 companies by total assets is interesting because not many of the companies that have the highest total revenue also have a large amount of total assets. While JP Morgan may have the highest amount of assets, they are not in the top 10 companies based on total revenue. Exxon and AT&T are the only companies in the top 10 foe both total revenue and total assets. Companies that have high total assets may not efficiently using assets to drive revenue

<img width="824" alt="Screenshot 2024-06-19 at 10 56 16 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/e4fc814e-699c-4c7e-82df-f3367a987f72">
When looking at the bar graph of earnings per share none of the top 10 companies in total revenue and total assets are reflected in the highest earnings per share. Higher total revenue typically leads to higher income, thus increasing earnings per share, so it is interesting to see different companies in the top ten compared to the previous two charts.

## Linear Regression Model Development 
- checking number of missing values in each row & clean data 

Cash Ratio                      299
Current Ratio                   299
Quick Ratio                     299
For Year                        173
Earnings Per Share              219
Estimated Shares Outstanding    219

-build full model (only showing a subset of the output) 
<img width="526" alt="Screenshot 2024-06-19 at 10 58 28 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/a1334f02-6bbe-4cd6-8b5b-934b55d8f474">

<img width="748" alt="Screenshot 2024-06-19 at 10 59 46 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/e419cecb-e370-45d5-8e9e-8491dc9e4668">

#### Interpretation:
The condition number is large indicating that there may be multicolinearity between the variables.
There are 23 significant variables.
There are many large p-values indicating that some of the variables are not significant in our model to predict the estimated shares outstanding. P-values less than the 0.05 significance level may be considered statistically significant in our model for example cost of revenue, gross profit, etc.
Our adjusted R-squared can be used to evaluate the fit of the model since it will penalize more for unnecessary variables compared to R-Squared. 84.6% of the variation in estimated shares outstanding can be explained using the predictor variables in our model. Additionally a high F-statistic value also indicates a good fit of the model.


## Multicollinearity in Linear Regression 
One of the assumptions of linear regression is that there is no exact multicollinearity between the x variables. Multicollinearity will always be present, so it is a concern of the degree of correlation, not of whether or not it exists. Multicollinearity occurs when two of the explanatory variables of the regression are highly correlated. This is concerning because it is hard to separate the individual effects of each explanatory variable on the response variable. If there is perfect multicollinearity, the slope regression coefficients become indeterminate and their standard errors are infinity. If multicollinearity is less than perfect the slope regression coefficients remain indeterminate, and the variance and standard errors of the estimators are large. The coefficients can not be estimated with good precision. Ultimately, multicollinearity leads to large variance and standard error of the coefficients, wide confidence intervals, inflated R^2 value, few significant t-values, and difficulty in determining the individual effects of explanatory variables on the dependent variable.

## P-value Analysis and Histogram 
<img width="641" alt="Screenshot 2024-06-19 at 11 01 46 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/146d5205-207a-4f97-8101-3387cb547a07">

Skewness=0.477 
Kolmogorove-Smirnov Test: (0.273605701211858, 1.8789456034107103e-05)

#### Interpretation:
The histogram shows a right skew pattern in the distribution of p-values. Additionally, the positive skew value of 0.538 further supports the indication of a right skew distribution. Usually, when the null hypothesis is true, we would expect the p-values to be normally distributed between 0 and 1. Since this is not the case and there are more small p-values it means that there is a higher rejection of the null hypothesis of statistical tests due to the significance of more variables. With right skewed p-values there is also a higher concern for false dicovery rate because when the null hypothesis is true, some tests may show significant results just by chance. Running the Kolmogorove-Smirnof Test results in a small p-value allowing for the rejection of the null hypothesis and concluding that the p-values are not uniformly distributed.

## False Discovery Rate Control with BH Procedure
-controll FDR with q=0.1
-estimate "true" discoveries: 14 

<img width="713" alt="Screenshot 2024-06-19 at 11 05 59 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/f0cbb9d2-135e-4f39-b79c-d8c1b4d4bea9">

## Sensitivity Analysis
-determining how the number of false discoveries changes if we change q 
<img width="672" alt="Screenshot 2024-06-19 at 11 07 20 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/e4546c32-daa2-421e-969d-2f296a785ee3">
<img width="632" alt="Screenshot 2024-06-19 at 11 07 34 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/0df64963-916c-4938-9140-fea8a598c5a1">
<img width="681" alt="Screenshot 2024-06-19 at 11 07 53 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/728cc7ea-9d62-417e-9a10-ea01afcf5a39">

#### Interpretation: 
When increasing the threshold it will result in a higher value of alpha. A lower q value allows for less false discoveries and a higher q will result in more false discoveries. When variables remain significant across different levels of q, they are less likely to be false positives since they are statistically significant across a range of thresholds indicating robustness. Since the number of true discoveries remains consistent from q=0.05-0.01 it is likely that the variables are not false positives and are robust

## Exploring Interaction Terms 
<img width="537" alt="Screenshot 2024-06-19 at 11 08 48 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/35d47b52-740e-49cc-933e-e2d63e6a7812">
Interaction terms are important in predicting Estimated Shares Outstanding because one or more variables may have a combined effect on the number of shares outstanding. For example, accounts payable does not seem to be significant in predicting estimated shares outstanding at the 5% significance level on its own, but when interacted with capital expenditures, the interaction effect is significant.

## Comparing full model to model with interaction terms 
The model without interaction terms results in an adjusted R squared value of 0.846. Since there are many variables used in our regression using the R squared adjusted value is more appropriate since it will penalize for adding additional, unnecessary variables in the model. R^2 will never decrease when additional variables are added. The model with interaction has an adjusted R squared value of 0.926. This illustrates an improvement in our model fit when accounting for interaction terms and quadratic terms. 92.6% of the variation in estimated shares outstanding can be explained by the predictors in our interaction model.

The models performance seems to improve overall with the inclusion of interaction terms. Adding interaction terms increase the model to have 99 significant variables as opposed to the 23 from the simple linear regression model with no interaction. The fit of the model improves with interaction terms illustrated by R^2, so it would be important to include them to better predict shares outstanding. The coefficients of the predictors seem to overall decrease with the added interactions as they will have less effect in the predictor as more variables are added into the model.


## FDR Analysis With Interaction Terms 

<img width="778" alt="Screenshot 2024-06-19 at 11 11 13 AM" src="https://github.com/lex910/Estimated-Shares-Outstanding-/assets/101606445/a14021fe-ab6e-416a-bdec-5db68548255f">

skew=0.6815053473121794
Kolmogorove-Smirnov Test: (0.2849697077635196, 1.200174379800724e-25)

We again see that the pvalues are right skewed, suppored by the positive skew metric as well as failing to reject the null hypothesis of the kologorove-Smirnov test for uniformity.

There are 99 significant predictors identified including both main and interaction effects.
The interaction model leads to more significant predictor variables and more true discoveries since there are a greater number of variables represented in the model. After including the interaction terms in our model there will be more possible discoveries that would not be able to be identified using the previous model. There is a posibility of more overfitting with an interaction model which can lead to the detection of more false positives.
