# Predictive Maintenance 

## Abstract
Utilizing a publically available data set, this project predicts pump failures based on psuedo-alarm data generated from a publically available data set. 

## Dataset
Pump sensor data set found on Kaggle [here](https://www.kaggle.com/nphantawee/pump-sensor-data). The data set is comprised of roughly 50 sensors with period sampling prior to and during a water pump's normal operation and failure.

## Data Representation and Processing
The sensor data was cleaned and converted to discrete alarms which assert when the readings are in the 2% and 98% quantiles. The number of alarms per 5 day interval were averaged and this rolling alarm rate used to predict pump failures with a forecast window of 5 days prior to pump catestrophic failure.

## Model Derivation
Four models were optimized via grid search and 5-fold cross-validation: Logistic Regession, Random Forest, XGBoost, Gradient Boosted Classifier and scored area under the reciever operator curve.  The results were as follows:

| Model | Optimized Parameters | AUC|
|-------|----------------------|---------|
| Logistic Regression | C: 0.001, penalty: L2 | 0.945 |
| Random Forest | max_depth: 32, n_estimators: 16 | 0.999 |
| XGBoost | gamma: 0.3, max_depth: None | 0.999 |
| Gradient Boost | learning_rate = 0.1, max_depth=4,n_estimators=500| 0.999 |

## Results
Scoring the Logistic Regression and Random Forrest models on the test set gives the following classification reports and confusion matricies:
#### Classfication Reports
![](https://github.com/jgalloway42/predictive_maintenance_playground/blob/main/classification_report.png)

#### Logistic Regression Confusion Matrix and ROC
![](https://github.com/jgalloway42/predictive_maintenance_playground/blob/main/log_reg_cm_and_roc.png)

#### Classification Report for Random Forrest
![](https://github.com/jgalloway42/predictive_maintenance_playground/blob/main/rf_cm_and_roc.png)

## Conclusion
Overall, the scheme works exceedingly well. The random forrest model performed slightly better than logistic regression, but given the latter's simplicity, speed of training and interpretability, logistic regression would likely be the preferred model for productionalization.

