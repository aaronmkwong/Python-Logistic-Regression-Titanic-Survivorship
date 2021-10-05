# Python-Logistic-Regression-Titanic-Survivorship

** ***THIS REPOSITORY IS UNDER CONSTRUCTION*** **


**SUMMARY**

This project performs binary logistic regression modeling to classify a passenger's survivorship as died or survived. It focuses more on statistics to select features, understand assumptions and evaluate results, rather than iteratively transforming and selecting features to achieve a best performing model, as is the case in the **[Boston House Prices](https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices)** project. The Titanic Survivorship project too is intended to be limited in scope as a learning sprint with its code and methods potentially applied to more robust model versions in the future.             

Of the given features, imputation, parsing, dummy encoding and scaling are used to obtain 13 engineered features. Model assumptions reviewed include: the dependent variable is binary; observations are independent; the independent variables are not multicollinear; the independent variables and log odds are linear; the dataset is large. The results are evaluated using a Pearson Residual to identify outliers, which may be indicative of remaining issues with feature engineering or regression assumptions.   

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

The Titanic dataset dependent variable is indeed binary, but shows an imbalance. Models can skew to predicting the majority class if an imbalance is present (Brownlee, 2021b, Imbalanced Classification with Python, p. 42). A slight imbalance is often not a concern, e.g. 4:6, and the problem can often be treated like a normal classification predictive modeling problem (Brownlee, 2021b, Imbalanced Classification with Python, p. 6). In this case, the ratio of 1 to 0 is 5:8, so no balance adjustment is performed in the model.   

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/binary_dep_var_assumption_01.JPG">

<ins>Model Results & Explainability</ins>

...

<ins>Assumptions Review Part II</ins>

...

**REFERENCES**

Brownlee, Jason. (2021a). *Data Preparation for Machine Learning: Data Cleaning, Feature Selection and Data Transforms in Python*. https://machinelearningmastery.com/data-preparation-for-machine-learning/ 

Brownlee, Jason. (2021b). *Imbalanced Classification with Python Choose Better Metrics, Balance Skewed Classes, and Apply Cost-Sensitive Learning*. https://machinelearningmastery.com/imbalanced-classification-with-python/

