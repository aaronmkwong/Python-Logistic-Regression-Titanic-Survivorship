# Python-Logistic-Regression-Titanic-Survivorship

** ***THIS REPOSITORY IS UNDER CONTRUCTION*** **


**SUMMARY**

This project uses logistic regression modeling to classify a passenger's survivorship as died or survived. It focuses more on statistics to select features, understand assumptions and evaluate results, rather than simply iteratively transforming and selecting features to achieve a best performing model, as was the case in the **[Boston House Prices](https://github.com/aaronmkwong/Python-Linear-Regression-Boston-House-Prices)**) project. This project too is limited in scope as a learning sprint, but the code and methods for which can be applied to future more robust model versions.             

Of the given features, imputation, parsing, dummy encoding and scaling are used to obtain 13 engineered features.     

**WALK THROUGH**

**_Data Exploration_**

The Titanic dataset is available through the **[Kaggle](https://www.kaggle.com/c/titanic/overview)** competition. 

<ins>Target</ins><br/>
Survived : Binary indicator of survival (0 = died, 1 = survived) <br/>

<ins>Given Features</ins><br/>
Passenger ID : Number assigned to each passenger <br/>
Pclass : Proxy for socio-economic status (1 = upper, 2 = middle, 3 = lower) <br/>
Name : Passenger’s name (wedded women, her husband’s name appears first and her maiden name appears in parentheses) <br/>
Sex : Passenger’s sex <br/>
Age : Age of passenger (passengers under the age of 1 year have fractional ages) <br/>
SibSp : Count of the passenger’s siblings or spouses aboard <br/>
Parch : Count of the passenger’s parents or siblings aboard <br/>
Ticket : Number printed on the ticket <br/>
Fare : Price for the ticket<br/>
Cabin : Cabin number occupied by the passenger <br/>
Embarked : The port from which the passenger boarded the ship <br/>
