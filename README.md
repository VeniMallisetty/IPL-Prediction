Project Overview: IPL Score Prediction
Description
The IPL Score Prediction project is a machine learning-based solution designed to predict the final score of an Indian Premier League (IPL) cricket match based on key match statistics. The project leverages historical IPL match data to train predictive models, enabling users to estimate a team's total score after the first innings, given specific inputs such as the batting team, bowling team, overs completed, runs scored, wickets lost, and performance in the last 5 overs.

Objective
The primary goal is to build an accurate and reliable model for predicting IPL match scores, which can be useful for cricket enthusiasts, analysts, and fantasy league players. The project explores two machine learning approaches—Random Forest Regression and AdaBoost Regression with Linear Regression as the base estimator—to determine the most effective method for score prediction.

Dataset
The dataset (ipl.csv) contains ball-by-ball IPL match data with the following key features:

date: Match date
bat_team: Batting team
bowl_team: Bowling team
runs: Cumulative runs scored
wickets: Cumulative wickets lost
overs: Overs completed
runs_last_5: Runs scored in the last 5 overs
wickets_last_5: Wickets lost in the last 5 overs
total: Final innings score (target variable)
The dataset initially consists of 76,014 rows and 15 columns, which is preprocessed to focus on consistent teams and data after 5 overs, reducing it to 40,108 rows.

Data Preprocessing
The code performs several preprocessing steps to prepare the data for modeling:

Column Removal: Drops irrelevant columns (mid, venue, batsman, bowler, striker, non-striker) to focus on team-level statistics.
Team Filtering: Retains only consistently participating teams (e.g., Chennai Super Kings, Mumbai Indians, etc.), reducing the dataset to 53,811 rows.
Overs Filtering: Excludes data from the first 5 overs to focus on mid-innings predictions, resulting in 40,108 rows.
Date Conversion: Converts the date column to a datetime object for potential temporal analysis.
Encoding: Applies one-hot encoding to bat_team and bowl_team columns to convert categorical variables into numerical format.
Modeling
Two regression models are implemented and evaluated:

Random Forest Regressor:
A robust ensemble method using multiple decision trees.
Evaluation Metrics:
Mean Absolute Error (MAE): 13.82
Mean Squared Error (MSE): 336.24
Root Mean Squared Error (RMSE): 18.34
AdaBoost Regressor (with Linear Regression base):
An ensemble boosting method that iteratively improves predictions.
Evaluation Metrics:
MAE: 12.13
MSE: 247.74
RMSE: 15.74
Chosen as the final model due to better performance (lower error metrics).
The dataset is split into training (80%) and testing (20%) sets, with features (X) including encoded team data and match statistics, and the target variable (y) being the total score.

Prediction Function
A custom predict_score function is implemented using the AdaBoost model. It takes the following inputs:

batting_team: Name of the batting team
bowling_team: Name of the bowling team
overs: Current overs completed (must be >= 5.0)
runs: Current runs scored
wickets: Current wickets lost
runs_in_prev_5: Runs scored in the previous 5 overs
wickets_in_prev_5: Wickets lost in the previous 5 overs
The function returns a predicted final score as an integer, along with a range based on the mean absolute error (±13.40) to account for prediction uncertainty.
