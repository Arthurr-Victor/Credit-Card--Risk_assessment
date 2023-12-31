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

### Initial Data Analysis:

I began by plotting categorical variables and describing the predominant profiles within the data. For instance:

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/tiporenda.png)

* The chart above clearly indicates that the majority of clients are full-time fixed employees with signed contracts.

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/genero.png)  
![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/escolaridade.png)

Analyzing each variable, I concluded that the predominant profile consists of:

* Female customers
* Married individuals
* Those without children
* Homeowners
* Individuals without a car
* High school educated
* Common employment under the CLT regime.

With an understanding of our dataset, I formulated several hypotheses to guide our risk evaluation task.

### Key Questions and Hypotheses:

To address our goals, I compiled six key questions:

**Question 1:**
_How does ownership of assets, ranging from smaller possessions (e.g., cell phones) to larger ones (e.g., property, cars), influence the client's status? Is there a significant influence?_

**Question 2:**
_How do demographic variables relate to the client's status? Do any of these variables play a significant role in predicting the target variable?_

**Question 3:**
_Is considering annual income important in determining credit approval? Are clients with higher incomes more likely to be reliable payers?_

**Question 4:**
_Does the type of housing provide relevant insights into the target variable, or is it of little importance? Do those who own houses/apartments tend to be more reliable payers?_

**Question 5:**
_Does the total continuous employment duration of the client lead to any distinct behavior in their status?_

**Question 6:**
_Does age play a role? Are younger clients less prudent and thus more likely to default?_

### Hypothesis Testing:

To answer these questions, I conducted hypothesis tests such as Chi-square and ANOVA, using a significance level of 5% as a baseline. Due to data imbalance, graphical bivariate analysis was not always viable.

**Question 1:**

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/Teste%20Chi2%20Imovel.png)

Based on the Chi-square test results, we can conclude that there is a statistically significant association between the predictor variable (property ownership) and the target variable (whether the client is risky or not). In other words, owning property and thus being free from rental obligations is relevant and influential in risk analysis.

**Question 2:**

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/genero2.png)
![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/estadocivil2.png)

The most significant p-values were observed in variables:

* Gender
* Marital status
* Slightly less influential: income type

This suggests that certain demographic profiles are more prone to default.

**Question 3:**

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/salarioboxplot.png)

The analysis of median salary segmented by status did not show a significant influence.

**Question 4:**

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/tipohabitacao4.png)

The p-value of 0.21 does not indicate a consistent association between the two variables.

**Question 5:**
An ANOVA test was applied to compare the influence of employment duration on the client's risky behavior. The resulting p-value was 0.0000147, indicating that employment duration is likely a crucial variable for our model.

**Question 6:**
The p-value for the ANOVA test between "age" and "status" was 0.74, indicating no significant relationship.

### Data Preprocessing and Model Building:

After successfully identifying and removing outliers, a pivotal step in ensuring the data's quality, I proceeded to establish a robust pipeline tailored for the machine learning model. Within this pipeline, careful attention was given to addressing the multicollinearity challenges by judiciously excluding redundant variables. By doing so, we not only mitigated potential issues arising from correlated predictors but also streamlined the utilization of these variables in our subsequent machine learning modeling.

Once the pipeline was meticulously configured, the dataset underwent a prudent division into distinct training and testing subsets. To tackle the critical concern of class imbalance, a state-of-the-art technique called Synthetic Minority Over-sampling Technique (SMOTE) was effectively applied. This technique generated synthetic samples to amplify the representation of the minority class, thereby promoting a balanced training environment for the models.

Three prominent machine learning algorithms, namely Random Forest, XGBoost, and Logistic Regression, were methodically evaluated using the Area Under the Receiver Operating Characteristic Curve (AUC) as our primary performance metric. The AUC metric provides a comprehensive assessment of a model's ability to distinguish between positive and negative classes, making it particularly well-suited for binary classification tasks. Following the rigorous evaluation, the XGBoost model emerged as the triumphant contender, displaying a superior performance that surpasses the alternatives.

The culmination of this rigorous evaluation process yielded valuable insights into the optimal hyperparameters for the XGBoost model, namely {'scale_pos_weight': 9, 'n_estimators': 700, 'max_depth': 6, 'max_delta_step': 10, 'learning_rate': 0.3}. Accompanied by this fine-tuned configuration, the XGBoost model demonstrated an exceptional AUC score of 0.6140456639522053, signifying its robust predictive capabilities in discerning credit risk.

As we progress towards deploying this model in a real-world scenario, it is imperative to recognize the meticulous efforts invested in refining each facet of the pipeline, from data preprocessing to model selection and tuning. This diligent approach sets the stage for a seamless transition into practical application and underpins the reliability and effectiveness of our credit risk assessment solution.

### Threshold Selection and Model Evaluation:

To optimize model performance, I determined the probability threshold for class separation (risky vs. low risk) using the F1-score metric, which balances precision and recall. It's important to note that calculating expected value could also be a valuable metric, requiring knowledge of profit/loss from each confusion matrix decision. This approach was utilized in another project of mine, named "Churn Analysis and Prediction."

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/f1-score.png)

An optimal F1-Score point falls between 0 and 0.12. As the majority of instances are labeled as 0, our model predicts most values with low probabilities of risky behavior (status=1), indicating a high probability of low risk.

As an illustrative example, I adjusted the probability threshold to a considerably low value, 0.000005, and plotted a confusion matrix. This resulted in an excellent recall for the positive class (1) but significantly impacted other metrics.

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/confusionmatrix.png)

## Deploying a Machine Learning Model: Making Real-World Impact

![Exemplo de Imagem](https://github.com/Arthurr-Victor/Credit-Card--Risk_assessment/blob/main/Images/Credit_deploy.png)

Deploying a machine learning model is a pivotal step, enabling its application in real-world decisions. This involves creating an accessible service, often through APIs, for seamless interaction with systems, applications, or users. Here, we outline the deployment process and key tools, including Flask and Ngrok.

### Model Selection
After thorough analysis, the XGBoost model was chosen for deployment due to its high AUC score, indicating strong predictive performance.

Selected input features:

- casado(1 ou 0)

- possui_carro(1 ou 0)

- possui_imovel(1 ou 0)

- ensino_superior(1 ou 0)

- salario(float)

- idade(int)

### Flask: Streamlined Web Framework

Flask, a lightweight Python web framework, facilitated model deployment. It enables the creation of a RESTful API that exposes prediction capabilities via HTTP, allowing other applications to send data and receive predictions.

##### Flask deployment steps:

1. Defining a Flask app: Creating and configuring routes for incoming requests.
2. Model integration: Loading the pre-trained XGBoost model.
3. Data preprocessing: Transforming incoming data to the model's required format.
4. Prediction endpoint: Establishing an API endpoint for making predictions.

### Ngrok: Bridging Local and Global

Ngrok was utilized to make the Flask app accessible online. It establishes a secure tunnel from the locally hosted server, enabling external applications to interact with the deployed model.

##### Ngrok deployment process:

1. Installation: Downloading and installing Ngrok.
2. Server exposure: Running Ngrok to expose the Flask app externally.
3. Generating a public URL: Ngrok provides a public URL for sending requests to the Flask app.
4. Conclusion: Unlocking Real-World Potential
5. Deploying a machine learning model involves transforming it into a practical tool for real-world applications. Through Flask and Ngrok integration, we've successfully created an API endpoint, allowing seamless interaction with our XGBoost model for credit risk assessment.

As you progress with deployment, consider scalability, security, and monitoring. Ensuring the model maintains its accuracy and responsiveness in a production environment is crucial for successful credit risk assessment outcomes.

### Final Recommendations:

Following the statistical tests such as Chi-square and ANOVA, and establishing a significance level of 5%, I arrived at the following conclusions:

* Demographic information about clients is crucial for credit risk analysis, particularly marital status, gender, and income type.
* Ownership of assets like property contributes to risk score classification.
* Clients with longer employment duration tend to be less risky compared to others.

Feel free to use this project summary as a README to provide an overview of the analysis you conducted.
