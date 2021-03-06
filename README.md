# Financial Model

a classification model that classify whether the EURUSD stock exchange will go up or down next day based on historical data

## Experiments

* ### Linear Regression
  i used linear regression model to evaluate the features in the future prediction of the time-series over the time

* ### Feature investigation
  i used multiple features and got the following results:

  * using the High-Low average as the only feature <br> ![training results](/res/avg_feat.png)
  * using `High`, `Low`, `Close`, `Volume`, `Avg`, `year`, `month`, `day` as features <br> ![training results](/res/multiple_feat.png)
  * using `year`, `month`, `day`, `Volume` as features <br> ![training results](/res/time_feat.png)
  * using 116 features that can be found [here](/notebooks/FeatureEngineering.ipynb) <br> ![training results](/res/all_feat.png)
* ### Classification
  i used multiple classifiers to get the best results, the main idea is the same, having the average of any day compared by the next day (the objective of the task), and the rate could be higher `1` or lower `0`, results could be found below

  * Adaboost classifier `1.61s` training time

  ```python
                precision    recall  f1-score   support

          0.0       0.55      0.60      0.57       230
          1.0       0.51      0.46      0.48       208

  avg / total       0.53      0.53      0.53       438
  ```

  * Random Forest `484ms` training time

  ```python
                precision    recall  f1-score   support

          0.0       0.61      0.61      0.61       230
          1.0       0.57      0.57      0.57       208

  avg / total       0.59      0.59      0.59       438

  ```

  * SGD Classifier `5.04s` training time

  ```python
                precision    recall  f1-score   support

          0.0       0.64      0.56      0.60       230
          1.0       0.57      0.65      0.61       208

  avg / total       0.61      0.60      0.60       438
  ```

  * SVC `473ms` training time

  ```python
                precision    recall  f1-score   support

          0.0       0.63      0.60      0.61       230
          1.0       0.58      0.61      0.59       208

  avg / total       0.60      0.60      0.60       438
  ```

* ### new classification experiment
  this time we used multiple techniques to make sure that we have the best accuracy and that our model is actually has the accuracy that it says it has

  * Polynomial Features
    > i did experiment with 2 and 3 poly feautres and got better results using 2nd degree poly feautres
  * using correlation as indicator for the features
    > i tried to use feautres that has high correlation with the output variable, i tried features that has correlation above or equal [0.5, 0.7, 0.8, 0.9] and got the best cv score on the `0.8` correlation
  * Grid search for best params
    > i used grid search techniques to get the best params for my model, and after trying muliple feautres i got the best result using `logistic regression` with penalty score of `100` and using `l1` as penalty function.

## Conclusion

* ### Regression Investigations
  we could see clearly that the set of features could capture more of the time series and resulted in better model both on the short and long terms.
* ### Classification Investigations
  i chose the logistic regression as it had the best cv score and test score for prediction.
