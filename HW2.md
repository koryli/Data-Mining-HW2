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
![image](https://user-images.githubusercontent.com/112587000/220752505-be907f2a-1057-4765-a188-21e1f196f191.png)
Call:
glm(formula = Default ~ duration + amount + installment + age + 
    history + purpose + foreign, family = binomial, data = german_credit)

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-2.3464  -0.8050  -0.5751   1.0250   2.4767  

Coefficients:
                      Estimate Std. Error z value Pr(>|z|)    
(Intercept)         -7.075e-01  4.726e-01  -1.497  0.13435    
duration             2.526e-02  8.100e-03   3.118  0.00182 
amount               9.596e-05  3.650e-05   2.629  0.00856 
installment          2.216e-01  7.626e-02   2.906  0.00366 
age                 -2.018e-02  7.224e-03  -2.794  0.00521 
historypoor         -1.108e+00  2.473e-01  -4.479 7.51e-06 
historyterrible     -1.885e+00  2.822e-01  -6.679 2.41e-11 
purposeedu           7.248e-01  3.707e-01   1.955  0.05058 
purposegoods/repair  1.049e-01  2.573e-01   0.408  0.68346    
purposenewcar        8.545e-01  2.773e-01   3.081  0.00206 
purposeusedcar      -7.959e-01  3.598e-01  -2.212  0.02694 
foreigngerman       -1.265e+00  5.773e-01  -2.191  0.02849 
---


(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 1221.7  on 999  degrees of freedom
Residual deviance: 1070.0  on 988  degrees of freedom
AIC: 1094

Number of Fisher Scoring iterations: 4

        (Intercept)            duration              amount 
              -0.71                0.03                0.00 
        installment                 age         historypoor 
               0.22               -0.02               -1.11 
    historyterrible          purposeedu purposegoods/repair 
              -1.88                0.72                0.10 
      purposenewcar      purposeusedcar       foreigngerman 
               0.85               -0.80               -1.26 
   yhat
y     0   1
  0 645  55
  1 211  89
[1] 0.734

  0   1 
700 300 
[1] 0.7


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
