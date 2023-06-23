# Movie-Popularity-Prediction 
## Preprocessing

### Data Gathering:
The data has been gathered by reading two different CSV files using the Pandas library of Python. The first file, "movies-regression-dataset.csv," and The second file, "movies-credit-students-train.csv," These two CSV files have been merged based on the ID column to form a single dataset. (We changed the column name of IDs in the second CSV which was named (movie_id to id) to facilitate the merging process)

Upon reviewing the data, we conducted a thorough analysis of the null and unique values present in each column. Subsequently, we implemented the following steps to refine the dataset:

1. `IDs` column: We opted to drop this column as it contains unique values that are only beneficial for merging purposes.
2. Duplicate `Title` Column: Given that there were two title columns from merging, we removed one of them, as they are duplicates.
3. `Homepage` column: Due to the presence of numerous null values, we eliminated this column, as it did not provide any useful data.
4. `Tagline` Column: Similar to the Homepage column, we removed the `Tagline` column due to the significant number of null values. Furthermore, the remaining data consisted of unique values, which did not yield any useful insights.
5. `Runtime` Column: We observed that only one null value was present in the Runtime column. Consequently, we decided to drop it from the dataset.
6. `Status` Column: With only two unique values present, and one of them appearing only once, we deemed this column to be of little use in our analysis.
7. `Release Date` Column: In an effort to further analyze the dataset, we partitioned the `Release Date` column into three separate columns: `Days`, `Month`, and `Year`.

### Data Split:
The next step is to split the data into training and testing sets. The dataset has been split into 80% training data and 20% testing data using the `train_test_split` function of Scikit-Learn library. The training set has 2425 rows and 15 columns, while the testing set has 607 rows and 15 columns.

### Handling Outliers:
We conducted an exploratory data analysis by plotting the data points in the `X_train` and `X_test` columns with numerical values. Our analysis revealed the presence of outliers in six columns: `revenue`, `budget`, `viewer count`, `runtime`, `vote count`, `year`, `month`, and `day` columns. To address this, we utilized a function called `replace_outliers`, which uses the interquartile range method to replace upper and lower outliers with the respective upper and lower limits. These limits were saved for future use in removing outliers from the `X_test` set.

The `replace_test_outlier` function has been created to replace the outliers in the testing data. The function takes the name of the column and the list of limits (we applied the limits obtained from `X_train` to remove the outliers in the `X_test` set.) as input and replaces the outliers in the testing data with the limits.

• Before Handling Outliers
![image](https://github.com/MINALOTFY10/Movie-Popularity-Prediction/assets/99563220/013aa668-a477-40e2-b817-24995566a36c)

• After Handling Outliers
![image](https://github.com/MINALOTFY10/Movie-Popularity-Prediction/assets/99563220/eb8832ae-c088-4f42-ade8-700029b464e9)

## Preprocessing

### Handling Missing:
To address the issue of missing values, it was observed that certain columns such as budget and runtime had 0 values, which did not make sense. Therefore, the missing values in these columns were replaced with the mean value of their respective columns in `X_train`. The mean value of each column was saved to replace the missing values in `X_test`.

### Preprocessing of the original Language column using Ordinal encoder:
The `Language` column contained a limited number of unique values (in `X_train` in total). As a result, an ordinal encoder was applied to transform this column. The `fit_transform` method was used on `X_train` and `transform` method on `X_test`. If any new category was found in `X_test`, it was replaced with -1.
![image](https://github.com/MINALOTFY10/Movie-Popularity-Prediction/assets/99563220/5dd99f49-c1e4-4b38-b60b-96ea58698b9b)


### Preprocessing of the title column:
We applied lemmatization and used TextBlob to obtain sentiment scores for each movie title. The sentiment score is computed using the polarity property of the `TextBlob.sentiment` object, which ranges from -1 to 1. A value closer to -1 indicates a negative sentiment, while a value closer to 1 indicates a positive sentiment. The `title` column of both the training and testing sets will be replaced with the corresponding sentiment score values.

## Preprocessing

### Preprocessing of the `title` column:
o We applied lemmatization and used TextBlob to obtain sentiment scores for each movie title. The sentiment score is computed using the polarity property of the `TextBlob.sentiment` object, which ranges from -1 to 1. A value closer to -1 indicates a negative sentiment, while a value closer to 1 indicates a positive sentiment. The `title` column of both the training and testing sets will be replaced with the corresponding sentiment score values.

### Preprocessing of the Original Title column:

o We applied three preprocessing techniques to the original title column of the dataset: lemmatization, stop words removal, and punctuation removal. These steps helped to standardize the text, reduce noise, and improve model performance by removing unnecessary words and characters from the data.

o In this case, we have identified rows where the original title differs from the title. We then created a binary variable to indicate whether the two titles match or not. Specifically, if the titles are the same, we assign a value of 1 to the original title column. If they are not the same, we assign a value of 0 to the original title column. This process helps to distinguish between cases where there may have been modifications made to the original title and cases where the original title was used without alteration.

o Upon performing the summation of binary values assigned to the original title column, it has been observed that out of a total of 3040 rows, 2901 rows have been assigned a value of 1. This indicates that in these cases, the original title matches the title. On the other hand, the remaining 139 rows have been assigned a value of 0, indicating that most of these titles are the same but in a different language. As a result, we have decided to drop the original title column from the dataset.

![image](https://github.com/MINALOTFY10/Movie-Popularity-Prediction/assets/99563220/eeaa0530-a722-4416-937b-db4ffc10a67d)

o	Therefore, word2vector algorithm was applied,and matrix containing the results was obtained. Each row was replaced by its corresponding column, and the mean was calculated and replaced with it.

o	Overall, we have successfully incorporated the word-to-vector technique in our machine learning model, and after experimentation with different methods, we have arrived at an optimal solution that yields improved performance.

# Pre-Processing of Production Companies and Production Countries Columns 
The pre-processing of the “production_companies” and "production_countries" columns involved several steps to extract meaningful information from these columns and transform them into one-hot encoded features. Here is a detailed explanation of each step:

## 1.	Extracting Names from Columns
The "production_companies" and "production_countries" columns were initially in JSON format, which contained multiple pieces of information such as the name, ID for "production_companies" and "iso_3166_1", country name for "production_countries". 

To extract only the names of the production companies and countries from these columns, we defined a function extract_keywords(x) that uses the ast library to convert the JSON string to a list of dictionaries. 

We then looped over the list and appended the name of each production company or country to a new list. Finally, this new list of names was returned by the function.

![image](https://github.com/MINALOTFY10/Movie-Popularity-Prediction/assets/99563220/fa082a71-98da-43b3-b799-9351c1f9678c)

## 2.	Frequency Analysis and Selection of Keywords
After extracting the names from the columns, we performed a frequency analysis to identify the most common keywords in both columns. This was done using the Counter() function from the collections library.
We then removed any stopwords and selected the 60 most common keywords for the "production_companies" column and the 21 most common keywords for the "production_countries" column. These keywords were stored in two separate sets, “keywords_freq” and “freq_pro_countries”.

![image](https://github.com/MINALOTFY10/Movie-Popularity-Prediction/assets/99563220/c2a93a8a-a638-4b3c-a505-933d4b64e997)

## 3.	One-Hot Encoding
Finally, we used our class Our_OneHotEncoder to transform the extracted keywords into one-hot encoded features. This class has three methods:
  1.	fit_freq() method fits the set of keywords obtained in step 2.
  2.	fit() method fits the keywords extracted from the columns for the training dataset.
  3.	transform() method transforms the extracted keywords into binary features, where each keyword corresponds to a column and contains a 1 if the keyword is present in the row, and 0 otherwise.
 These methods were applied separately to both the training and testing datasets for the "production_companies" and "production_countries" columns.

![image](https://github.com/MINALOTFY10/Movie-Popularity-Prediction/assets/99563220/0185753f-598e-4d44-a499-e864839afd8c)


# Scaling:
•	To standardize the numeric columns of X_train ('budget', 'viewer count', 'revenue', 'runtime', 'vote count', 'year', 'month', 'day'), Standard Scaler was applied (fit and transform). This scaling was then used on X_test (transform only).

# Feature Selection:
In this section, we will describe the feature selection methods that we used to identify the most relevant features for our regression model.

### Pearson's Correlation Coefficient
Pearson's correlation coefficient is a statistical measure that quantifies the linear relationship between two variables. It can be used to evaluate the correlation between each input feature and the target variable in a dataset. Features with a high correlation coefficient (positive or negative) are more likely to be good predictors of the outcome and can be selected for the model. Pearson's correlation coefficient is a simple and easy-to-use method that can quickly identify the most important features for a model.

### KBest
KBest is another feature selection method that selects the top K features based on their score on a given statistical test. For example, in the case of linear regression, the F-test is often used to evaluate the significance of each feature in predicting the outcome. KBest selects the K features with the highest F-test scores and discards the rest. This method can be used to identify features that are significant predictors of the outcome and can improve the model's performance.


### Combining Pearson's Correlation Coefficient and KBest
We used both Pearson's correlation coefficient and KBest together to select the most relevant features for our regression model. This approach helped to ensure that the selected features were highly correlated with the target variable and were also statistically significant predictors of the outcome. This approach can improve the overall performance of the model and help to avoid overfitting, where the model may perform well on the training data but poorly on new, unseen data.

### Selected Features
Based on the results of feature selection, the following features were chosen for the regression model:

![image](https://github.com/MINALOTFY10/Movie-Popularity-Prediction/assets/99563220/0152c006-93af-4a78-ac92-856a7766af26)

Other features were discarded as they were found to have lower correlation with the target variable or were not deemed significant in predicting the target variable.


# 2. Dataset Analysis
We performed an analysis of the dataset to gain a better understanding of the relationships between the variables. We used scatter plots to visualize the relationship between the budget and revenue columns, and found a positive correlation between the two variables, suggesting that higher budgets may lead to higher revenues. 

We also created a heatmap to visualize the correlations between the numeric columns, including budget, viewer count, revenue, runtime, vote count, and vote average. 
The heatmap showed strong positive correlations between revenue and budget, as well as between vote count and revenue, suggesting that these variables may be important predictors of movie success. 

These findings provide important insights into the factors that drive movie revenues and can inform future movie production and marketing strategies. 

![image](https://github.com/MINALOTFY10/Movie-Popularity-Prediction/assets/99563220/87f8a2d4-8909-48af-bd79-e0f3b538021e)


# 3. Models:
 1)	Support Vector Regression (SVR): Using a radial basis function kernel and hyperparameters C=1.9999 and gamma='scale', SVR achieved an RMSE of 0.58 and an R^2 score 
    of 0.60. SVR is a type of regression that uses support vector machines (SVMs) to perform regression tasks. It can handle non-linear relationships between the 
    predictor variables and the outcome variable, but it can be sensitive to the choice of kernel function and regularization parameters.
 2)	Ridge Regression: This model achieved an RMSE of 0.61 and an R^2 score of 0.56. It used hyperparameters alpha=10.6 and solver='sparse_cg’. Ridge Regression is a 
    type of linear regression that uses L2 regularization to prevent overfitting. Its performance was moderate in this case.
 3)	Principal Components Regression (PCR): After performing PCA on the data and training a Linear Regression model on the transformed data, PCR achieved an RMSE of 0.6 
    and an R-squared score of 0.56. PCR is a technique for reducing the dimensionality of a dataset by projecting the data into a lower-dimensional space.
 4)	Elastic Net Regression: With hyperparameters alpha=0.01 and l1_ratio=0.0, Elastic Net Regression achieved an RMSE of 0.6 and R-squared score of 0.56. Elastic Net 
    is a combination of Lasso and Ridge regressions and can handle multicollinearity among predictors.
 5)	Partial Least Squares Regression (PLS): PLS Regression, with n_components = 5, achieved an RMSE of 0.615 and R-squared score of 0.55. PLS is another technique for 
    reducing the dimensionality of a dataset and is often used when there are many features and multicollinearity is present.
 6)	Polynomial Regression: By creating polynomial features using Polynomial Features(degree=1), and then fitting a Linear Regression model, Polynomial Regression 
    achieved an RMSE of 0.62 and an R-squared score of 0.55. Polynomial Regression is a form of regression analysis in which the relationship between the independent 
    variable x and the dependent variable y is modeled as an nth degree polynomial.
    Overall, SVR had the highest accuracy with an R-squared score of 0.60. 

