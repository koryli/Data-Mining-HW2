### Author: Suyu Liu, Siyuan Liu, Jingru Li
## Q1 Saratoga house prices
-   **Linear model for the price**

Backward selection model:
rmse of step_lm:  [1] 53013.2

Based on the backward selection, although the RMSE is lower, the function contains too many variables and is kind of hard to explain in the reality. So, we try to select by hand based on the significance.

Call:
lm(formula = price ~ lotSize + age + landValue + livingArea + 
    bedrooms + bathrooms + rooms + centralAir + waterfront + 
    livingArea:newConstruction, data = saratoga_train)


RMSE of Selected model:  [1] 59225.28

Out-of-sample RMSE:

Average the estimate of out-of-sample RMSE over 100 different random train/test splits randomly:
RMSE:  58067.95 

-   **KNN regression model for the price**

Pick up K value by cross-validation and the RMSE:

The model is regressing price on lotSize + age + livingArea + pctCollege + bedrooms + fireplaces + bathrooms + rooms + heating + fuel + centralAir + landValue + sewer + newConstruction +waterfront.

RMSE of knn regression model(k = 10): 69217.9	

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

Number of Fisher Scoring iterations: 4

        (Intercept)            duration              amount 
              -0.71                0.03                0.00 
        installment                 age         historypoor 
               0.22               -0.02               -1.11 
    historyterrible          purposeedu purposegoods/repair 
              -1.88                0.72                0.10 
      purposenewcar      purposeusedcar       foreigngerman 
               0.85               -0.80               -1.26 
               

![image](https://user-images.githubusercontent.com/112587000/220753394-1c1d69a9-b606-4fee-bf38-994f514754da.png)

The coefficient for historypoor is -1.11. So having a poor history credit in a loan fell into default at some point before it was paid back to the bank odds of default by e^-1.11 = 0.329559;
The coefficient for historyterrible is -1.88. So having a terrible history credit in a loan fell into default at some point before it was paid back to the bank, odds of default by e^-1.88 = 0.15259. Coef of historypoor is larger than historyterrible, meaning that people with poor credit are more likely to fall into default than those with terrible credit. This does not fit reality. This phenomenon is because it is very difficult for people with terrible credit to get loans, so the number of people with terrible credit in the sample is smaller than those with poor credit, resulting in a more significant impact of poor credit on the probability of default.

This data set is not appropriate for building a predictive model of defaults. Because there is selection bias. And to eliminate bias, I think we can randomly select the borrowers and use 'history' to group them. Then we can screen prospective borrowers to classify them into "high" versus "low" probability of default.


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
