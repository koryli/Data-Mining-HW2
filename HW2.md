### Author: Suyu Liu, Siyuan Liu, Jingru Li
## Q1 Saratoga house prices
-   **Linear model for the price**

rmse of step_lm:
[1] 53013.2

Based on the backward selection, although the RMSE is lower, the function contains too many variables and is kind of hard to explain in the reality. So, we try to select by hand based on the significance.

Call:
lm(formula = price ~ lotSize + age + landValue + livingArea + 
    bedrooms + bathrooms + rooms + centralAir + waterfront + 
    livingArea:newConstruction, data = saratoga_train)

Residuals:
    Min      1Q  Median      3Q     Max 
-225934  -34419   -5723   28364  459112 

Coefficients:
                               Estimate Std. Error t value Pr(>|t|)    
(Intercept)                   1.494e+05  1.787e+04   8.360  < 2e-16 ***
lotSize                       6.021e+03  2.272e+03   2.650  0.00814 ** 
age                          -1.474e+02  6.013e+01  -2.452  0.01435 *  
landValue                     9.334e-01  5.203e-02  17.940  < 2e-16 ***
livingArea                    5.408e+01  5.700e+00   9.488  < 2e-16 ***
bedrooms                     -8.157e+03  2.907e+03  -2.806  0.00509 ** 
bathrooms                     2.359e+04  3.754e+03   6.284 4.41e-10 ***
rooms                         3.598e+03  1.092e+03   3.294  0.00101 ** 
centralAirNo                 -1.054e+04  3.687e+03  -2.859  0.00431 ** 
waterfrontNo                 -1.268e+05  1.629e+04  -7.783 1.39e-14 ***
livingArea:newConstructionNo  1.513e+01  3.236e+00   4.675 3.23e-06 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 59460 on 1371 degrees of freedom
Multiple R-squared:  0.6431,	Adjusted R-squared:  0.6404 
F-statistic:   247 on 10 and 1371 DF,  p-value: < 2.2e-16

RMSE of Selected model:
[1] 59225.28

Out-of-sample RMSE:

Average the estimate of out-of-sample RMSE over 100 different random train/test splits randomly:

  result 
  
58067.95 

-   **KNN regression model for the price**

Pick up K value by cross-validation and the RMSE:

The model is regressing price on lotSize + age + livingArea + pctCollege + bedrooms + fireplaces + bathrooms + rooms + heating + fuel + centralAir + landValue + sewer + newConstruction +waterfront.

RMSE of knn regression model(k = 10):
69217.9	

### Report:
Based on the results, the first model has the lower out-of-sample mean-squared error, meaning this model fits better.

(the formula = price ~ lotSize+age +landValue +livingArea+bedrooms+bathrooms+rooms+centralAir + waterfront+livingArea:newConstruction)

For the linear model selection, I firstly use backward selection, but the model contains more variables and some of them are not statistically significant. To get a lower RMSE and reasonable function, I choose the variables by hand and intuition based on their significance and the model as above. When estimating the house price, we need consider the lotSize, age, landValue, livingArea, bedrooms, bathrooms, rooms, centralAir, waterfront and the interaction of livingArea and newConstruction of the house. And some variables, like heating, fuel and sewer, have insignificant impact on the price, so I exclude them from the model.    

For the KNN regression, I use the cross validation to choose K with the lowest RMSE. And the model is simply polynomial linear regression, including all variables in the data.

Comparing these two models, I find when considering more variables into the linear regression model, the RMSE increase more likely and the model will performance worse. Because the model includes some explanatory variables that have no or little effect on price, like heating, fuel.

## Q2 Classification and retrospective sampling

## Q3 Children and hotel reservations
### Model building
small model:

RMSE: 
[1] 0.2681091

Accuracy:
[1] 0.9194444

big model:

RMSE:
[1] 0.2315222

Accuracy:
[1] 0.9358889

My best model:

RMSE:
[1] 0.2301603

Accuracy:
[1] 0.9373333

Model building:

My best model is children ~ . - arrival_date - days_in_waiting_list - required_car_parking_spaces + total_of_special_requests:adults  + adults:booking_changes + adults:assigned_room_type

The RMSE of the small model is larger than the big model.

The RMSE of the big model is larger than my best model.

And the predict accuracy is the same situation.

So the big model performs better than the small model,

my best model performs better than the big model.

### Model validation: step 1
![image](https://user-images.githubusercontent.com/112587000/220745095-cb8abbcb-2d55-40cf-9aba-b6907c42753f.png)

### Model validation: step 2
The predict accuracy: 

$Fold01
[1] 0.904

$Fold02
[1] 0.936

$Fold03
[1] 0.936

$Fold04
[1] 0.92

$Fold05
[1] 0.912

$Fold06
[1] 0.936

$Fold07
[1] 0.932

$Fold08
[1] 0.948

$Fold09
[1] 0.944

$Fold10
[1] 0.944

$Fold11
[1] 0.936

$Fold12
[1] 0.932

$Fold13
[1] 0.948

$Fold14
[1] 0.952

$Fold15
[1] 0.916

$Fold16
[1] 0.964

$Fold17
[1] 0.944

$Fold18
[1] 0.936

$Fold19
[1] 0.952

$Fold20
[1] 0.952

![image](https://user-images.githubusercontent.com/112587000/220745271-54f51394-bffe-466d-87c8-82948c64a1cf.png)
