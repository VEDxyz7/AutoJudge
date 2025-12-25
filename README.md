# AutoJudge 

AutoJudge predicts the difficulty of programming problems (basically DSA/CP problems) using historical data.The difficulty level is classified into three categories (easy/medium/hard) and a problem score (on the scale of 1-10) is given to the problem.

## Dataset

Source : Provided dataset (originally in .jsonl format and further converted to .csv)
Total samples : 4112
Fields of the dataset are :
- Title
- Description
- input_description 
- output_description
- sample_io
- problem_class 
- problem_score
- url

## Text Preprocessing

Combined the first 5 fields of dataset into single text field , handled missing values by replacing them with empty strings

## Feature Extraction

- Calculated the frequency of keywords(like dp,greedy,dfs etc) occuring in combined text of a problem
- Converted text features to numeric using TFIDF vectorization
- Added text length as a feature

## Classification

- Splitted the data for training and testing using train_test_split (80% train and 20% test)

- Used Logistic Regression
Accuracy - 48.60267314702308 %
Confusion Matrix -
        easy  hard  medium
easy      91    26      36
hard      66   200     123
medium    71   101     109

- Used Random Forest Trees
Accuracy - 54.79951397326853 %
Confusion Matrix -
        easy  hard  medium
easy      55    77      21
hard       8   363      18
medium    23   225      33

- Used Support Vector Machines
Accuracy - 47.38760631834751 %
Confusion Matrix -
        easy  hard  medium
easy       1   152       0
hard       0   389       0
medium     0   281       0

- Logistic Regression predicts all types of classes and is mainly confused between easy-medium and medium-hard.
- Random Forest has the best accuracy among all the tested models and problems are majorly classified as hard.
- Support Vector Machines collapsed as it is majorly predicting only one category(hard) which tells us that it fails to predict on this dataset.

## Regression

- Splitted the data for training and testing using train_test_split (80% train and 20% test)

- Used Linear Regression
RMSE - 2.87

- Used RandomForestRegressor
RMSE - 2.05

- Used GradientBoosting
RMSE - 2.07

- In Linear Regression model , relatively high RMSE concludes that the relation between textual features and numeric difficulty is non-linear.
- Random Forest significantly improves performance by modeling non-linear relationships.
- Gradient Boosting provides same results as Random Forest but however Random Forest has more accurate results.

## Model Used 

- So as we can see Random Forest classifier and Random Forest Regressor had given the best results , so they are used in the project.

## Web Interface and Backend Integration

- Used HTML and CSS for Ui and Javascript for sending requests and updating results.
- The backend serves as an interface API that loads ML models , processes input and performs prediction and returns the result in JSON format , the technologies used in backend were Flask (python framework) , Sckit-learn (for ML models) , joblib (for loading models) and numpy and scipy (for handling features).
