# Python-Logistic-Regression-Titanic-Survivorship

** ***THIS REPOSITORY IS UNDER CONSTRUCTION*** **


**SUMMARY**

This project performs binary logistic regression modeling to classify a passenger's survivorship as died or survived. It focuses more on statistics to select features, understand assumptions and evaluate results, rather than iteratively transforming and selecting features to achieve a best performing model, as is the case in the **[Boston House Prices](https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices)** project. The Titanic Survivorship project too is intended to be limited in scope as a learning sprint with its code and methods potentially applied to more robust model versions in the future.             

Of the given features, imputation, parsing, dummy encoding and scaling are used to obtain 13 engineered features. Model assumptions reviewed include: the dependent variable is binary; observations are independent; the independent variables are not multicollinear; the independent variables and log odds are linear; the dataset is large. The results are evaluated using a Pearson Residual to identify outliers, which may be indicative of remaining issues with feature engineering or regression assumptions.   

The Titanic dataset is available at **[Kaggle](https://www.kaggle.com/c/titanic/overview)**.

The average **_model accuracy is 80%_** using Monte Carlo cross validation 25 times with a 0.7-0.3 train-test split. There is an average of **_5 outliers_** with a standard distance of 3 or more. 

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/summary_results.JPG" width="800" height="50">

**WALK THROUGH**

<ins>Feature Engineering</ins> 

In the **_original data_** sample below, Name, Sex, Ticket, Cabin and Embarked are text, also Age, Cabin and Embarked contain nulls.  

Name is parsed for titles, categorized using the function title_category() as Doctor, Peerage, Nobility, Religious, Military and Untitled then dummy encoded. Ticket is dropped as it does not contain useful information. Cabin is dropped since the majority of values are nulls and unlikely to benefit from imputation. Sex and Embarked are dummy encoded, but the 2 rows which contain nulls under Embarked are removed since they are unlikely to impact model training. Age is imputed with the function impute_avg().       

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/original_data_01.JPG" width="1000" height="200">

...

<img src="https://github.com/aaronmkwong/Python-Logistic-Regression-Titanic-Survivorship/blob/main/Other%20Files/final_data_01.JPG" width="1000" height="200">

<ins>Assumptions Review Part I</ins>

...

<ins>Model Results & Explainability</ins>

...

<ins>Assumptions Review Part II</ins>

...

