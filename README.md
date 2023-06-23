# Movie-Popularity-Prediction 

## 1. The preprocessing steps included:

• Data gathering: The data was gathered from two CSV files.
• Data split: The data was split into training and testing sets.
• Handling outliers: Outliers were identified and replaced with the respective upper and lower limits.
• Handling missing values: Missing values were replaced with the mean value of their respective columns.
• Preprocessing of the original Language column using an Ordinal encoder: The Language column was encoded using an Ordinal encoder.
• Preprocessing of the title column: The title column was preprocessed using lemmatization and sentiment analysis.
• Preprocessing of the Original Title column: The Original Title column was preprocessed using lemmatization, stop words removal and punctuation removal.
• Preprocessing of the tagline column: The tagline column was preprocessed using sentiment analysis.
• Handling Columns in JSON Form: The relevant information from the JSON columns was extracted.
• One hot encoding: Two columns were one hot encoded.
• Word2vector: The word2vector technique was used to create feature vectors for columns containing text data.
• Scaling: To standardize the numeric columns of X_train ('budget', 'viewer count', 'revenue', 'runtime', 'vote count', 'year', 'month', 'day').
•	Feature Selection: Selecting feature using Pearson's Correlation Coefficient, KBest and Combining Pearson's Correlation Coefficient and KBest

Pre-Processing of Production Companies and Production Countries Columns: The production companies and production countries columns were preprocessed and one hot encoded.
The preprocessing steps were performed to improve the quality of the data and to make it more suitable for machine learning.

## 2. Dataset Analysis
•	The dataset was analyzed to identify the most relevant features for predicting movie revenue.
•	The following features were selected: budget, viewer count, runtime, vote count, and vote average.

## 3. Models
•	Six different models were trained to predict movie revenue: Support Vector Regression (SVR), Ridge Regression, Principal Components Regression (PCR), Elastic Net Regression, Partial Least Squares Regression (PLS), and Polynomial Regression.
•	SVR had the highest accuracy with an R-squared score of 0.60.


## 4. The effect of HyperParameter tuning 
* The report discusses the use of hyperparameter tuning to improve the performance of three machine learning models: SVM, logistic regression, and gradient boosting.
* For SVM, the best hyperparameters were found to be kernel='rbf', C=2.2, and gamma='scale'. This resulted in an accuracy of 0.762.
* For logistic regression, the best hyperparameters were found to be penalty='l2', C=0.2, and solver='newton-cg'. This resulted in an accuracy of 0.74299.
* For gradient boosting, the best hyperparameters were found to be n_estimators=44, max_depth=2, and learning_rate=0.3. This resulted in an accuracy of 0.7495881383855024.
* Overall, the hyperparameter tuning significantly improved the performance of all three models. The best parameters for each model are summarized in the table below.

| Model | Best Parameters | Accuracy |
|---|---|---|
| SVM | kernel='rbf', C=2.2, gamma='scale' | 0.762 |
| Logistic Regression | penalty='l2', C=0.2, solver='newton-cg' | 0.74299 |
| Gradient Boosting | n_estimators=44, max_depth=2, learning_rate=0.3 | 0.7495881383855024 |


