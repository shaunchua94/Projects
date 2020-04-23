# General Assembly DSI 13 Capstone
# Investing the Education Consultancy Business

**Shaun Chua**
<br> 23 April 2020
<br> General Assembly (Data Science Immersive 13)

---------------------------------------------------------------------------------
## Introduction
#### **Context**
The inception of the Government Electronic Business Centre (GeBIZ) to standardise government tender and procurement has significantly reduced <a href="https://opentextbc.ca/principlesofeconomics/chapter/16-1-the-problem-of-imperfect-information-and-asymmetric-information/"> imperfect information and assymetric information</a>.

As a result, education consultancies face the daunting challenge of balancing several tenets of business development, such as:
* Outreach to educational institutions
* Pricing stragegies
* Business development


#### **Project Goals**
The objectives of this project are twofold.

**Objective 1:**
To investigate the business of such an education consultancy, identifying business units, consultants, and other relevant contributors to selling price of a programme.

**Objective 2:**
To create a model that may assist in predicting a suitable selling price of educational programmes.

Modelling will be done separately for each obbjective.


#### **Classification Metrics**
Several classification metrics will be considered, and these include:
**Objective 1:** Coefficient of Determination
**Objective 2:** Root-Mean-Square Error (RMSE)


#### **Application**
The findings of this project may provide insight which may assist the business development endeavours of the participating education consultancy.

# Executive Summary
## 1. Methodology

This project is in collaboration with an education consultancy, who has kindkly volunteer some sales data.

#### 1.1 Data Cleaning
We then combined the two CSV files and begun cleaning the data in approximiately the following order:
1) Determining relevant features (most were not helpful)
2) Resolving/Imputation for missing values
3) Standardising case to Snake case
5) Encoding categorical variables

#### 1.2 Preprocessing
We attempted to analyse features based on broad groups, before analysing all features togther.

As such, we defined different groups of predictors to separately train our model. Predictors were broken down into:
* All Features
* Entity
* Consultant
* Zone

A train-test split was then conducted at a 80-20 train-test ratio, before predictors were scaled.

#### 1.3 Modelling
**Objective 1**
1) Linear Regression with Regularisation (Ridge, Lasso, Elastic Net)

**Objective 2:**
2) Decision Tree Regressor
3) Random Forest Regressor
4) Support Vector Regressor
5) Decision Tree Regressor with AdaBoost
6) Random Forest Regressor with AdaBoost
7) Gradient Boosting Regressor
8) Extreme Gradient Boosting (XGBoost)

## 2. Findings
### Objective 1
Linear Regression with Ridge Regularisation performed best.

The table below shows the metric of each run of the models for Objective 1:

<img src="./images/dsi_13_shaun_capstone_metrics_obj1.png">

### Objective 2
The Extreme Gradient Boosting Regressor (XGBoostRegressor) performed best.

The table below shows the metric of each run of the models for Objective 2:

<img src="./images/dsi_13_shaun_capstone_metrics_obj2.png">

## 3. Discussion
### 3.1 Objective 1
Isolating groups of predictors resulted in exceptionally poor Coefficients of Determination.

Therefore, we decided to proceed with the "All Features" run of the model, which returned the following coefficients:

<img src="./images/dsi_13_shaun_capstone_ridge_coef_plot.png">

<br> In the evaluation of the model, consultants had the greatest impact on programme selling price, followed by Zone, and finally the business entity itself.

Unit of Measure (UOM) deserves a special mention, because that feature alone could significantly impact programme selling price.

### 3.2 Objective 2
Several Regression models were run, with XGBoostRegressor emerging as the best model with the following scores:

Train RMSE Score ≈ 1895.90
Validation RMSE Score ≈ 2913.24

The RMSE of 2913.24 suggests that the predicted selling price of a programme can be off by some SGD 2913.24, which is likely to be unacceptable.

This is particularly so for SVPs, as certain lower-value programmes sell for much lower than the RMSE itself. This implies that the XBGRegressor model may have limited utility in terms of predicting a suitable selling price for a programme.

## 4. Conclusion and Recommendations

### Objective 1
**1) Per Pax as Choice of UOM**
* `uom_per_pax` refering to the "Per Pax" unit of measurement generally impacted sale price postively to a greater extent thab `uom_per_hr`

**2) Invest in Lagging Business Entities**
* All Business entities are already making profits, despite the coefficient assigned to them by the model.
* In the long run, investing in trailing entities may become sustainable once revenue streams increase.

**3) Align Pricing Strategies**
* Different consultants tend to adopt different pricing strategies, evident from the coefficents attached to each consultant.
* Some favour high-selling price, while some prefer low-selling price in bulk.
* Regardless, it is important that the company ensures all consultants price in accordance with the direction of the company.

### Objective 2
As best, this model should serve as a modest guide for higher-value programmes, where a difference of SGD 2913.24 does not make a significant impact on profitability.

## 5. Limitations
**Small Dataset**
This project only utilised 2 years worth of data, 2018 and 2019, resulting in 45 features with only 675 observations.

To circumvent this, future studies can consider including more years worth of sales data.

**Limited Hyperparameter Tuning**
Due to memory constraints, it was not feasible to gridsearch an exhaustive list of hyperparameters to produce the best model to train on.

Future studies can consider Amazon Web Services (AWS), to leverage on their powerful computers.

## 6. Future Directions
**Differentiating UOM**
With regard to creating a model to predict selling price, future studies may find it worthwhile to first separate the dataset based on UOM.

Based on domain knowldege, the majority of per_pax tend to result in significantly higher selling prices as compared to per_hr, which may have caused some difficulty for machine learning.

Additionally, this distinction could result in a more targetted model to help predict a suitable selling price for a programme, based on whether the UOM is per_pax or per_hr.

**Include Cost in Place of Qty and/or Unit Price**
Since consultants tend to adopt different pricing strategies, and different business entities sell different value programmes, it may be worth including cost-related features as part of the dataset.

This eliminates the variation between business units and consultants, hopefully allowing the model to determine that some entities and/or consultants tend to sell higher than others despite similar cost-features.
