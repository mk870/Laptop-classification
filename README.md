# Laptop Brand Classifier: Project Overview
* The 2020 Covid pandemic revealed some cracks in the global tech supply chains, it showed that many laptop brands share the same technology(lithium ion batteries,semiconductors,OLED),chip manufacturers(Intel,AMD,TSMC) and depend on almost the same Chinese and global companies for supplies. So as a customer, I wanted to see if these brands can still be distinguished by their product features alone even though they share the same supply chains and underlying technologies or we as consumers are just paying for the brand names alone.
* Scraped over 1500 laptops from <**pricebaba.com**> using python and the Beautiful soup library.
* Engineered, extracted and created new features from the data and finaly filled in missing values.
* Optimized logistic,random forest and xgboost multi-classifiers using GridSearchCV and RandSearchCV to arrived at the best model.
* Built a Feature importance graph showing the top 10 laptop brand distinguishing features.
## Code And Resources Used

**Python version:** 3.8.

**Packages:** pandas,numpy,seaborn,matplotlib,beatiful soup.

**Web Framework Requirements:** pip install.

## Web Scraping
First scraped the product links from the website then scraped the detailed laptop features inside the links themselves,so I got the following features:
* Brand name
* Ratings
* Number of ratings
* Colour
* Operating system
* Screen size(inches)
* Screen resolution
* Display type
* Display features
* Touchscreen
* Processor
* Processor model
* Processor speed(GHz)
* Cache memory(MBs)
* Graphics processor
* RAM(Gig)
* RAM max
* Memory slots
* RAM type
* Fingerprint
* Keyboard
* Battery life(Hrs)
* Pointing device
* RAM speed(MHz)
* Harddrive type
* Harddrive capacity(Gig)
* Weight(kg)
* Dimensions(mm)
* Warranty
* Sale package
* USB 2.0
* Wifi
* Bluetooth
* Optical Drive
* USB typeC
* Multimedia input
* Adapter(watts)
* Battery cells
* Battery type

## Data Cleaning

After scraping,I cleaned the data to make it usable in the models. So I made the following changes and variables:

* Aligned the columns and data,removed rows without brand name in excel.
* Renamed the columns appropriately.
* Removed and Replaced unnecessary strings from the data.
* Converted columns to their rightful datatype.
* Created Number of Processor cores from the Processor feature.
* Created Length,Width and Height columns from the Dimensions feature.
* Split the data into 2, a holdoutset and the training set (80% training and 20% holdoutset).
* Removed Battery life column since it had more than 70% missing data.
* Checked and removed outliers in the numeric data
* Built an Iterative imputer model using the Extra Trees Regressor to fill in missing numeric data.
* Built Categorical imputer model to fill in missing categorical features with less than 20 missing values using the frequent imputation method.
* Built 4 XGBoost classifiers and used the SMOTE technique to predict the missing values of Harddrive type, USBtypeC, Optical drive and Fingerprint columns.
* Applied the same models and procedures used on the training set to the holdout data set.

## EDA
Looked at the relationship between the features and our target (Brand) and also the relationship between the features themselves. Below are the highlights:

![image 1](/images/pic1.png)

![image 2](/images/pic2.png)

![image 3](/images/pic3.png)

## Model Building
First, I transformed the categorical features into dummy variables.

Secondly, I applied the SMOTE technique since my data was imbalanced.

Then optimized and trained three different models using Kfold cross validation with gridSearch and RandomSearchCV on the training set.

Then finally used the tuned models to predict the holdoutset

Models used:

* Logistic Regression (multiclassification)
* RandomForest Classifier (multiclassification)
* XGBoost Classifier (multiclassification)


## Model Perfomance
The XGBoost Classifier by far outperformed other models both on the training and holdout sets

* **Logistic Regression**: Accuracy ~ 49.5%
* **Random Forest Multi-Classifier**: Accuracy ~ 73.6%
* **XGBoost Multi-Classifier**: Accuracy ~ 86.7%
## Conclusion
Feature importance ranking:

![image 4](/images/pic4.png)

The operating system,Touchscreen,screen pixel density,display type and harddrive capacity seem to rank high as laptop features 
that differentiate brands. This shows that there is not a lot of technological differences that set aside these brands from  
each other.
This is due to the fact that every laptop can have different operating system installed in it after being purchased,
nowadays external harddrives compensate for low internal harddrive capacity, only leaving display type,screen pixel density 
and touch screen technology. 

If perfomance is the objective then almost any brand can provide that optimal perfomance but if
screen technology is the priority then certain brands have better technology for those needs such as Apple and microsoft.
