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

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/Status.png)

We can clearly observe that there is an issue with unbalanced data. This challenge alters our approach to the analysis.
Such an imbalance in the target variable is a potential "weakening" factor in our modeling process. We will address this later on.

After addressing issues such as missing data and duplicates, correcting variable types, and performing other transformations on the dataset, we initiated the analysis of predictor variables that reflect individual client characteristics.

## Exploring Categorical Variables

To start, I plotted the categorical variables and described the predominant profile present in the data. For example:

The graph above clearly demonstrates that the majority of clients are full-time salaried employees with formal contracts.

By examining each variable in this manner, we concluded that the predominant profile includes:

- Female clientele
- Married individuals
- Clients without children
- Property owners
- Clients without cars
- Individuals with a high school education
- Clients in common full-time employment (CLT).

## Hypothesis Testing

To address several questions, I conducted hypothesis tests such as Chi-square and ANOVA, using a significance level of 5%. Due to class imbalance, graphical bivariate analysis was not always feasible.

### Question 1:

Based on the results of the Chi-square tests, we can infer a statistically significant association between the predictor variable (property ownership) and the target variable (credit risk status). In other words, clients owning their own property, and thereby being relieved of rental burdens, significantly influence the risk assessment.

### Question 2:

More notable p-values were observed in demographic variables:

- Gender
- Marital status
- Income type (to a slightly lesser extent)

### Question 3:

The analysis of median "income" values segmented by "status" did not suggest significant influence.

### Question 4:

A p-value of 0.21 did not indicate a meaningful association between the two variables.

### Question 5:

By applying ANOVA, we assessed whether the segmentation of clients based on years of employment had an impact on the client's risk status. The resulting p-value was 0.0000147, indicating the potential importance of "years employed" for our modeling.

### Question 6:

The p-value of the ANOVA between "age" and "status" was 0.74, exceeding the base significance level of 0.05.

## Continued Data Preprocessing

With a clearer understanding of our data, we proceeded with further data preprocessing. This involved identifying and addressing outliers using the Local Outlier Factor (LOF) algorithm.

## Feature Selection

We removed redundant variables and those showing multicollinearity, optimizing our predictive model pipeline.

## Model Building

Following the pipeline setup, we divided the data into training and testing sets. We utilized the Synthetic Minority Over-sampling Technique (SMOTE) to address class imbalance.

## Model Evaluation

We assessed the performance of three models—Random Forest, XGBoost, and Logistic Regression—using the AUC Value. The XGBoost model outperformed the others.

Best Parameters: {'scale_pos_weight': 9, 'n_estimators': 700, 'max_depth': 6, 'max_delta_step': 10, 'learning_rate': 0.3}
Best AUC Score: 0.6140456639522053

## Fine-Tuning the Model

To extract the best possible results from the model, we set a probability threshold based on the F1-score, which strikes a balance between precision and recall.

## Visualizing Results

The optimal F1-score threshold appeared to be between 0 and 0.12. Due to the prevalence of class 0 instances, our model predominantly predicts low occurrence of high-risk users (status=1).

## Final Remarks

This README provides a concise overview of the credit risk evaluation project, encompassing statistical tests that shed light on influential variables. It offers valuable insights into the risk assessment process.

For detailed analysis and comprehensive findings, please refer to the complete project documentation.
