# Credit Card Risk Assessment Project
## Overview
Credit scoring is a widely employed risk management technique in the financial sector. It leverages personal information and data provided by credit card applicants to estimate the likelihood of future bankruptcies and credit card defaults. This empowers banks to make informed decisions regarding the issuance of credit cards. Credit scores serve as objective measures of risk level.

In this project, the primary objective is to develop a machine learning model capable of predicting whether an applicant is a 'good' or 'bad' user based on the available dataset. Notably, the criteria for categorizing applicants as 'good' or 'bad' are not explicitly defined, adding complexity to the task. Moreover, the project grapples with the challenge of unbalanced data, a significant concern that needs to be addressed.

## Data and Variables
Two datasets extracted from Kaggle will be utilized for this project:

#### Application Record Dataset
The application record dataset contains comprehensive information about each applicant, encompassing details such as gender, date of birth (DOB), education type, assets, and more. It consists of the following types of variables:

*12 categorical variables* -
*5 continuous variables* -
*1 variable to uniquely identify applicants (applicant ID)*

#### Credit Record Dataset
The credit record dataset comprises an applicant's loan payment records, aiding in assessing creditworthiness. It encompasses the following variables:

*1 categorical variable* -
*1 continuous variable* -
*1 variable to uniquely identify applicants (applicant ID)*

## What do we want to predict?

Our criterion for defining the target variable is as follows: Customers whose default period exceeds 60 days will be classified as high-risk (status=1), while those whose debt does not surpass this threshold will be considered low-risk.
