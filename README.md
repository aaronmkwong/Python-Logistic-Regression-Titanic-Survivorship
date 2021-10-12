# Python-Logistic-Regression-Titanic-Survivorship

** ***THIS REPOSITORY IS UNDER CONSTRUCTION*** **


**SUMMARY**

This project performs binary logistic regression modeling to classify a passenger's survivorship as died or survived. It focuses more on statistics to select features, understand assumptions and evaluate results, rather than iteratively transforming and selecting features to achieve a best performing model, as is the case in the **[Boston House Prices](https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices)** project. The Titanic Survivorship project too is intended to be limited in scope as a learning sprint with its code and methods potentially applied to more robust model versions in the future.             

Of the given features, imputation, parsing, dummy encoding and scaling are used to obtain 13 engineered features. Model assumptions reviewed include: the dependent variable is binary; observations are independent; the independent variables are not multicollinear; the independent variables and log odds are linear; the dataset is large (Statistics Solutions, 2021). The results are evaluated using a standardized residual to identify outliers, which may be indicative of remaining issues with feature engineering or regression assumptions.   

The Titanic dataset is available at **[Kaggle](https://www.kaggle.com/c/titanic/overview)**.

The average **_model accuracy is 80%_** using Monte Carlo cross validation 25 times with a 0.7-0.3 train-test split. There is an average of **_5 outliers_** with a standard distance of 3 or more. 

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/summary_results.JPG" width="800" height="50">

**WALK THROUGH**

The code is separated into 2 files and **[Titanic_Survivorship_11A.ipynb](https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Program%20Files/Titanic_Survivorship_11A.ipynb)** and ... . All of the functions mentioned below are custom built.

<ins>Feature Engineering</ins> 

In the **_original data_** sample below, Name, Sex, Ticket, Cabin and Embarked are text, also Age, Cabin and Embarked contain nulls.   

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/original_data_01.JPG" width="1000" height="200">

Name is parsed for titles, categorized using the function title_category() as Doctor, Peerage, Nobility, Religious, Military and Untitled then dummy encoded. Ticket is dropped as it does not contain useful information. Cabin is dropped since the majority of values are nulls and unlikely to benefit from imputation. Sex and Embarked are dummy encoded, but the 2 rows which contain nulls under Embarked are removed since they are unlikely to impact model training. Age is imputed with the function impute_avg(), which uses the original dataframe as a global variable and Pclass and Age column names as arguments to calculate the average age of each passenger class then apply to the null Age values.  

In the **_encoded data_** sample below there is an issue with the scale of the data when comparing PassengerId, Pclass, Fare and Age to the other features. Differences in scale across features can result in a model that learns large weight values and is sensitive to input values leading to higher generalization error (Brownlee, 2021a, p. 231).

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/unscaled_data_01.JPG" width="1000" height="200">

In the **_engineered data_** sample below all features have been scaled to be 0 to 1. For example, Pclass changes from 1, 2, 3 to 0, 0.5, 1. 

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/final_data_01.JPG" width="1000" height="200">

<ins>Assumptions Review Part I</ins>

The Survived **_dependent variable is binary_**, but shows an imbalance. Models can skew to predicting the majority class if an imbalance is present (Brownlee, 2021b, p. 42). A slight imbalance is often not a concern, e.g. 4:6, and the problem can often be treated like a normal classification predictive modeling problem (Brownlee, 2021b, p. 23). In this case, the ratio of 1 to 0 is 5:8, so no balance adjustment is performed in the model.   

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/binary_dep_var_assumption_01.JPG">

The **_independent variables are not multicollinear_** after Untitled predictor is removed. If only pairwise correlation is used, the assumption may appear to hold as no pair has a strong R<sup>2</sup> value. It is helpful to regress each predictor on the others to determine how much larger the variance of each coefficient becomes when the corresponding predictor is included; a variance inflation factor greater than 10 is potentially indicative of multicollinearity (Pardoe, 2012, p. 206-9). The functions corr_pair() and multicoll() generate the following dataframes.         

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/multicollinearity_assumption_02.JPG" width="325" height="400">

The **_dataset is large_** at 889 observations and 14 features (before Untitled is removed). Using the one in ten rule, where a minimum of 10 cases is required for the least frequent outcome per independent variable (Statistics Solutions), the function dataset_size_test() returns 366 (732 at 20 cases) required observations to be sufficiently large. So, ( cases / ( least frequent outcome / total outcomes) ) * features = ( 10 / ( 340 / 889 ) ) * 14 = 366. 

<ins>Model Results & Explainability</ins>

Standardized residuals quantify how large the residuals are in standard deviation units and an observation larger than 3 (absolute value) is considered an outlier (Pardoe, 2021b). 

The predicted probability is subtracted from the observed target value 100% or 0% (1 or 0) to get the raw residual.

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/raw_residual_re_pearson_01.JPG">

 The raw residual is then divided by the standard deviation for a Bernoulli distribution (King, 2021) to get the Pearson residual (Pardoe, 2021a).
 
<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/pearson_residual_01.JPG">

The number of outliers range from 0 to 18 for the 25 trials. Only 3 trials have 0 outliers, which have accuracies of 0.82, 0.84 and 0.80. So, the model doesn't generalize well yet. An important predictor may be missing; or one or more regression assumptions may be violated, in which case transformations or interactions can be helpful (Pardoe, 2012, p.190). The function log_mod_assess() generates a dataframe of classification report results and a count of observations with a standard distance between 2 and 3 as well as greater than or equal to 3. Also, the random state value is included, so as to reproduce the same results when interpreting the coefficients.

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/top_middle_worst_results_03.JPG" width="900" height="175">

When the logistic model log odds coefficients are converted to odds (e<sup>(log odds)</sup>) and then odds are distinguished in terms of odds survived (if e<sup>(log odds)</sup> >= 1, then e<sup>(log odds)</sup>) and odds not survived (if e<sup>(log odds)</sup> < 1, then 1 / e<sup>(log odds)</sup>), the following observations can be made. For example, as the independent variable Male increases by one unit, the odds that the person did not survive is multipled by over 10 (Pardoe, 2012, p.271) when all other independent variables are held constant. 

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/intercept_coefficients_02.JPG" width="450" height="400">

The sklearn logistic model predictions (see the below 8 sample target values) of not survived (0) or survived (1) are based on the model probabilities array, which in turn can be confirmed using the logistic function with the independent values (features), coefficients and intercept.

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/model_predictions_01.JPG">

<ins>Assumptions Review Part II</ins>

...independence...

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/raw_residuals_01.JPG">

...independent variables and log odds are linear...

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/linear_logitrespvar_explvar_01.JPG" width="700" height="350">

**REFERENCES**

Brownlee, Jason. (2021a). *Data Preparation for Machine Learning: Data Cleaning, Feature Selection and Data Transforms in Python* (v1.2 ed.). https://machinelearningmastery.com/data-preparation-for-machine-learning/ 

Brownlee, Jason. (2021b). *Imbalanced Classification with Python Choose Better Metrics, Balance Skewed Classes, and Apply Cost-Sensitive Learning* (v1.3 ed.). https://machinelearningmastery.com/imbalanced-classification-with-python/

King, Krista. (2021, October 10). *Bernoulli Random Variables And Mean, Variance, And Standard Deviation*. https://www.kristakingmath.com/blog/bernoulli-random-variables 

Pardoe, Ian. (2012). *Applied Regression Modeling* (2nd ed.). Hoboken, New Jersey: John Wiley & Sons.

Pardoe, Ian. (2021a, October 10). *Applied Regression Analysis: 12.1 Logistic Regression*. https://online.stat.psu.edu/stat462/node/207/

Pardoe, Ian. (2021b, October 10). *Applied Regression Analysis: 9.3 Identifying Outliers*. https://online.stat.psu.edu/stat462/node/172/

Statistics Solutions. (2021, October 6). *Assumptions of Logistic Regression*. https://www.statisticssolutions.com/free-resources/directory-of-statistical-analyses/assumptions-of-logistic-regression/
