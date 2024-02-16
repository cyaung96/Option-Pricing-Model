# Option Pricing Model
Main goal is to develop machine learning models that can accurately predict option prices by using the Black-Scholes algorithm. To achieve this I first cleaned data by removing outliers beyond 3 standard deviations from the mean and dropping records with null values. We then introduced two new features: the Future Value of an Investment and the Intrinsic Value of a Call Option, with the aim of improving model performance.

# Data Preparation 
The training dataset contains 1,680 records, each with six columns. The columns are as follows:

1. Value: the current option value
2. S: the current asset value
3. K: the strike price of the option
4. r: the annual interest rate
5. tau: the time to maturity (in years)
6. BS: the Black-Scholes formula was applied to this data to get the predicted option value

To conduct model explorations, the data underwent three necessary processes: formatting revision and imputation of missing values, outlier removal, and data standardization.

# Data Cleaning 
In order to ensure the integrity of our dataset, we performed two primary data cleaning tasks. Firstly, we eliminated records containing null values to maintain consistency and accuracy throughout the dataset.

Secondly, we identified and removed outliers that fell beyond three standard deviations from the mean of each predictor, as these values may skew the analysis and lead to erroneous conclusions. Dropping outliers boosted the Linear Regression R-square from 0.798 to 0.912

# Feature Engineering 
To boost performance the 2 features created in the model are: 
1. future_mult (1+r)^tau: Future value of an investment. For example, if you have an investment with an annual interest rate of 5% and a time to maturity of 10 years, the expression (1 + 0.05)10 is the value of each $1 you invested today after the 10-year investment period.
2. S/K : Ratio of Current Asset Value and Strike Price of Option: If the result is greater than 1, the option is "in the money" because the option holder could buy the underlying asset at a lower price than the current market price. Vice Versa. For example, if a call option has a K = $100 and S = $120, the intrinsic value of the option would be $20. This means the option holder could exercise the option and buy the underlying asset for $100, then sell it on the market for $120, realizing a profit of $20.

# Model Exploration
The objective in exploring different models was to identify the optimal model for both regression and classification tasks. For the regression task, the aim was to train a model capable of accurately predicting option prices. Meanwhile, for the classification task, the goal was to develop a model that could precisely classify whether the Black-Scholes algorithm would underestimate or overestimate the actual option price.

The strategy began with linear regression for the regression problem and logistic regression for the classification problem as baselines. These models were chosen for their simplicity and interpretability, offering quick insights into how input features influence the predicted outcome or target variable.

After establishing baseline performances, the exploration moved on to more complex, non-linear models, including decision trees, random forests, and boosting models. The strategy for selecting the best model involved tuning various hyperparameters and employing 5-fold cross-validation, with a random_state of 1, to ensure consistency and reproducibility in the results. The focus was on finding the set of hyperparameters that yielded the highest average cross-validation R-squared value for the regression model and the highest average cross-validation accuracy for the classification model.

This approach allowed for a systematic comparison of the performance of different models under a consistent evaluation framework, ensuring that the final model selections were both robust and well-justified.

# Final Model
For selecting the final models, two main criteria were emphasized. First, models demonstrating higher performance with a smaller standard deviation within sets, especially in cross-validation and test sets, were preferred. Second, models showing minimal differences in performance between training, cross-validation (CV), and test sets were favored, as this indicates a balanced model that is neither overfitting nor underfitting. Based on these rules, specific models were chosen as the final models for the project.

1. Regression - Gradient Boosting :
  - Training - R-square: 0.9996
  - Testing - R-square: 0.9988
  - Cross Validation - R-square: 0.9988
    
2. Classification - CatBoost 
  - Training - R-square: 0.9381
  - Testing - R-square: 0.9271
  - Cross Validation - R-square: 0.9247


