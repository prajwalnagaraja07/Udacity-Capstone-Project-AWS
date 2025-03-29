# AWS Machine Learning Engineer Nanodegree  
## Capstone Project

<p align="center">
  <img alt="AWS" src="https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white">
  <img alt="Udacity" src="https://img.shields.io/badge/Udacity-grey?style=for-the-badge&logo=udacity&logoColor=15B8E6">
  <img alt="License" src="https://img.shields.io/github/license/angeligareta/ml-engineer-nanodegree-capstone-project?style=for-the-badge" />
</p>

## Project Overview

This project aims to analyze customer behavior in the Starbucks Rewards mobile app to understand how different promotional offers impact customer interactions. The focus is on analyzing the customer responses to promotional offers, with an emphasis on their demographic profiles and previous interactions with the app. This analysis will help Starbucks optimize marketing campaigns, increase user engagement, and boost sales.

The key challenge involves identifying demographic groups that respond well to specific promotional offers. Since the response to offers can vary among customer segments, the task is to analyze customer demographics and preferences to predict the likelihood of completing a promotional offer after viewing it.

## Resources

- **Source Code**: The full project code is available in the repo.
- **Project Report**: The detailed project report outlining the methodology and findings can be accessed [here](capstone_project_report.pdf).

## Proposed Solution

A machine learning model will be created to predict the likelihood that a customer will complete a promotional offer after viewing it, based on their demographic information and past interactions with the app. This model will help determine which features of an offer are most likely to appeal to specific customer segments.

As a baseline, a heuristic approach using historical response data will be implemented. While this rule-based model can provide basic insights, it lacks the depth and flexibility of a machine learning model that incorporates a broader set of features and user behaviors.

## Methodology

The approach will include several key steps:

1. **Data Preprocessing**: Cleaning, transforming, and preparing the data.
2. **Exploratory Data Analysis (EDA)**: Identifying trends, correlations, and potential features for modeling, which is documented in the [data_processing notebook](data_processing.ipynb).
3. **Model Selection**: SageMaker AutoGluon will be used to automate the model selection process, evaluating multiple algorithms on the validation data to determine the best-performing model. This is covered in the [model_selection notebook](mbest_hyperparameter.ipynb).
4. **Model Training**: The selected model will be trained, and its hyperparameters fine-tuned using SageMaker. This process is detailed in the [model_training notebook](training.ipynb).
5. **Model Evaluation**: The final model will be evaluated using test data and compared against a benchmark. The model's features will also be analyzed for importance using SHAP values. Results can be found in the [model_evaluation notebook](evaluation.ipynb).

## Conclusions

The LightGBM model developed successfully predicts the likelihood of a customer completing an offer. By setting a threshold of 0.35 based on the F1-score, the model correctly identifies 83% of customers who complete an offer, with a precision of 0.75, meaning that 75% of the predictions are accurate. The model's overall accuracy is 0.65.

Key metrics such as Precision-Recall and ROC curves reinforce the model's ability to differentiate between customers who complete offers and those who do not. The PR AUC score is approximately 0.64, and the ROC AUC score is 0.784, indicating a solid performance in identifying potential offer completers.

Several features have been found to significantly influence offer completion:
- **Reward**: Moderate rewards improve offer completion, especially for long-term members, whereas no reward or excessive rewards reduce this likelihood.
- **Membership Duration**: Long-term members are more likely to complete offers.
- **Communication Channel**: Social channels are the most effective for sharing offers, outperforming web, mobile, and email.
- **Income**: Middle-income customers show higher completion rates, particularly with increased rewards, while both low and high-income customers are less likely to complete offers.
- **Difficulty**: Simpler offers tend to have higher completion rates.
- **Offer Type & Duration**: These factors do not significantly influence completion rates.
- **Gender**: Non-male customers are more likely to complete offers, particularly when the rewards are greater. Male customers tend to complete fewer offers.
- **Age**: Older customers, especially those over 40, are more likely to complete offers, particularly with higher rewards. Younger customers are less likely to engage with offers.

These insights can help shape targeted marketing strategies. However, it is important to ensure that any demographic-based targeting is done ethically and aligns with business objectives.

In summary, the model is highly effective in identifying customers likely to complete offers, even at the cost of some false positives. This could be valuable for improving marketing efforts and optimizing promotional strategies.

## Next Steps

Future work could involve refining the model by focusing solely on the key features that have the strongest predictive power—such as reward, membership days, income, social channel, difficulty, and offer duration—while omitting gender and age-related factors. This may help improve interpretability and reduce noise.

Additionally, a two-step model approach could be explored. The first model would predict whether a customer will view an offer, and the second model would focus on whether they will complete the offer once viewed. This could improve accuracy by addressing each step in the customer journey separately, allowing for more precise predictions.