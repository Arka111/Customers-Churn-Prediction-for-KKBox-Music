# Customers-Churn-Prediction-for-KKBox-Music
Worked on this project to predict customer churn from KKBox Music Streaming Service

Dataset
KKBOX is Asia’s leading music streaming service, holding the world’s most comprehensive Asia-Pop music library with over 30 million tracks. They offer a generous, unlimited version of their service to millions of people, supported by advertising and paid subscriptions. This delicate model is dependent on accurately predicting churn of their paid users. In this project we're working on a approach that predicts whether a user will churn after their subscription expires.
The train and the test data are selected from users whose membership expires within a certain month. The train data consists of users whose subscription expires within the month of February 2017, and the test data is with users whose subscription expires within the month of March 2017. This means we are looking at user churn or renewal roughly in the month of March 2017 for train set, and the user churn or renewal roughly in the month of April 2017. Train and test sets are split by transaction date, as well as the public and private leaderboard data.
In this dataset, KKBox has included more user’s behaviors than the ones in train and test datasets, in order to enable participants to explore different user behaviors outside of the train and test sets. For example, a user could actively cancel the subscription, but renew within 30 days.
Dataset: Kaggle: WSDM – KKBox’s Churn Prediction Challenge[4]
1. train.csv: msno vs is_churn
• rows = 99,921, columns = 2
2. user_logs.csv:
• rows = ~50000000, columns = 9
3. transactions.csv: details of transaction made by the users
• rows = 21547746, columns=9
4. members.csv: details about the user
• rows = 5116194, columns=7

# Findings from exploratory data analysis

i) Training and member’s data exploration:-
• There was an increase in registration trends yearly.
• “10” and “16” class of cities present in the member dataset but missing in merged dataset, so those city classes can be one hot-encoded.
• Yearly registration trends have increased.
• Monthly registration trends are higher in year start and year end
• Higher daily registration trends on weekends.
ii) Transactions data exploration
• Training set is almost 4.6% of entire transactions data.
• Almost 4.14% users had cancelled their subscription during plan period.
• There are 51 amount paid types with amount paid type “149” is the most frequent one.
• There is 93.5% correlation between actual amount paid and payment plan.
• Also observed that same user can have multiple payment plans with different subscription time.
• Almost 85.2% of users had set their plan to auto-renewal.
iii) User_Logs data exploration
• User Logs have logs for users not listed in train and test data sets. By removing those users, dataset reduced to half of its original size.
• 89259 train/test users don’t have logs.
• There is high correlation among songs listened on Monday, Tuesday, Wednesday and Thursday.
• Number of unique songs listened on Friday has higher influence on output.
• Users who opted for auto renew are listening more than 100 unique songs on Sundays in two months.

# Feature Engineering

Members data :
Engineered 8 new features out of the members 
Dropped  two preexisting  features.
Removed highly correlated features such as expiration_month ,expiration_year  based on correlation matrix scores

![alt text](https://github.com/techsachinkr/Customers-Churn-Prediction-for-KKBox-Music/blob/master/Outputs/Memberfeatures_Correlation_matrix.png)

Registration_via is feature with  evident higher churn rate percent, ranging from few percent to almost 20% for value 4.

![alt text](https://github.com/techsachinkr/Customers-Churn-Prediction-for-KKBox-Music/blob/master/Outputs/registered_via_churn%20relation.png)

Complete data
Removed 24 features that had correlation of greater than 0.92 using correlation matrix,leaving a total of 44 features

![alt text](https://github.com/techsachinkr/Customers-Churn-Prediction-for-KKBox-Music/blob/master/Outputs/AllFeatures_Correlation_matrix.png)

# Modeling
Modeled data using Random Forest Classifier with 100 estimators or trees to get 94.5% test accuracy and 0.10 log-loss.

# Feature Importance for validating hypothesis

Top 10 features from Random Forest
![alt text](https://github.com/techsachinkr/Customers-Churn-Prediction-for-KKBox-Music/blob/master/Outputs/features_importance.png)
