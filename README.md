# Movie Recommendation System

## Preprocessing Steps

The following steps were taken to preprocess the data for building a movie recommendation system:

1. Data Gathering: The data was obtained from two CSV files.
2. Data Splitting: The data was split into training and testing sets.
3. Handling Outliers: Outliers were identified and replaced with their respective upper and lower limits.
4. Handling Missing Values: Missing values were replaced with the mean value of their respective columns.
5. Encoding Language Column: The language column was encoded using an ordinal encoder.
6. Preprocessing Title Column: The title column was preprocessed using lemmatization and sentiment analysis.
7. Preprocessing Original Title Column: The original title column was preprocessed using lemmatization, stop words removal, and punctuation removal.
8. Preprocessing Tagline Column: The tagline column was preprocessed using sentiment analysis.
9. Handling Columns in JSON Form: Relevant information from JSON columns was extracted.
10. One Hot Encoding: Two columns were one hot encoded.
11. Word2vector: The word2vector technique was used to create feature vectors for columns containing text data.
12. Scaling: Numeric columns of X_train ('budget', 'viewer count', 'revenue', 'runtime', 'vote count', 'year', 'month', 'day') were standardized.
13. Feature Selection: Features were selected using Pearson's Correlation Coefficient, KBest, and a combination of Pearson's Correlation Coefficient and KBest.

Pre-Processing of Production Companies and Production Countries Columns: The production companies and production countries columns were preprocessed and one hot encoded.
The preprocessing steps were performed to improve the quality of the data and to make it more suitable for machine learning.

## 2. Dataset Analysis
•	The dataset was analyzed to identify the most relevant features for predicting movie revenue.
•	The following features were selected: budget, viewer count, runtime, vote count, and vote average.

## 3. Models
•	Six different models were trained to predict movie revenue: Support Vector Regression (SVR), Ridge Regression, Principal Components Regression (PCR), Elastic Net Regression, Partial Least Squares Regression (PLS), and Polynomial Regression.
•	SVR had the highest accuracy with an R-squared score of 0.60.


## 4. The effect of HyperParameter tuning 
* Hyperparameter tuning improved the performance of three machine learning models: SVM, logistic regression, and gradient boosting.
* For SVM, the best hyperparameters were found to be kernel='rbf', C=2.2, and gamma='scale'. This resulted in an accuracy of 0.762.
* For logistic regression, the best hyperparameters were found to be penalty='l2', C=0.2, and solver='newton-cg'. This resulted in an accuracy of 0.74299.
* For gradient boosting, the best hyperparameters were found to be n_estimators=44, max_depth=2, and learning_rate=0.3. This resulted in an accuracy of 0.7495881383855024.
* Overall, the hyperparameter tuning significantly improved the performance of all three models. The best parameters for each model are summarized in the table below.

| Model | Best Parameters | Accuracy |
|---|---|---|
| SVM | kernel='rbf', C=2.2, gamma='scale' | 0.762 |
| Logistic Regression | penalty='l2', C=0.2, solver='newton-cg' | 0.74299 |
| Gradient Boosting | n_estimators=44, max_depth=2, learning_rate=0.3 | 0.7495881383855024 |


