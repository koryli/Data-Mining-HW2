### Author: Suyu Liu, Siyuan Liu, Jingru Li
## Q1 Saratoga house prices

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
