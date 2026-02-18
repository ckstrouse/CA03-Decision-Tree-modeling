# CA03-Decision-Tree-modeling
Project Overview

This project builds and evaluates a Decision Tree classification model to predict whether an individual earns more than 50K per year. The model uses demographic and socioeconomic features that have been grouped into meaningful categories.

The objective was to build a structured and reproducible modeling pipeline, evaluate baseline performance, systematically tune hyperparameters, retrain the optimal model, and analyze results from both a technical and business perspective.

This was approached as a complete modeling workflow rather than a simple one time model fit.

Business Objective

The model predicts whether a person belongs to the higher income group above 50K annually. This type of classification is relevant for financial services, marketing segmentation, customer analytics, and policy evaluation.

The focus was not only overall accuracy but also balanced performance. Because the dataset is imbalanced, evaluation included accuracy, precision, recall, and F1 score to ensure the model performs responsibly across both income classes.

Dataset Overview

The dataset contains 48,842 observations and 11 columns.

Nine columns are categorical predictor variables representing demographic and socioeconomic factors. One column indicates whether the observation belongs to the training or testing set. One column is the binary target variable indicating income class.

All predictors are already discretized into bins. There are no missing values in the dataset.

The target variable is imbalanced. Approximately 76 percent of individuals earn 50K or less. Roughly 24 percent earn more than 50K. This imbalance affects recall performance and was considered during evaluation.

The dataset includes a predefined training and testing split. That split was preserved to prevent data leakage and maintain consistency.

Data Preparation

The target variable and split indicator were separated from the feature set before modeling.

The predefined training and testing split was used rather than creating a random split. This maintains the integrity of the original dataset structure.

Because all predictors are categorical, one hot encoding was applied within a pipeline. This ensures transformations are applied consistently to both training and testing data.

A reproducible pipeline was built so preprocessing and modeling occur together in a controlled structure.

Baseline Model

A Decision Tree classifier was trained using default settings with a fixed random state.

Baseline performance on the test set achieved approximately 83.6 percent accuracy.

Precision for predicting high income was approximately 69 percent. Recall was approximately 55 percent. The F1 score was approximately 0.62.

The model correctly identifies most lower income individuals. It is more conservative in identifying higher income individuals. This pattern is consistent with the class imbalance.

Hyperparameter Tuning Strategy

Hyperparameter tuning was conducted in structured stages rather than through automated grid search. Each parameter was evaluated individually while holding previously selected best parameters constant.

Split criterion was evaluated first. Gini performed slightly better than entropy and was selected.

Minimum samples per leaf was tested across multiple values. The best performance occurred at 20. This improved generalization and reduced overfitting.

Maximum features was evaluated next. The optimal value was 0.8.

Maximum depth was tested across increasing levels. Accuracy improved as depth increased initially, then plateaued. A depth of 10 provided the strongest performance while avoiding unnecessary complexity.

This sequential tuning approach ensured interpretability of each parameter’s impact rather than blind optimization.

Final Model Configuration

The final model used the following parameters

criterion equals gini
minimum samples per leaf equals 20
maximum features equals 0.8
maximum depth equals 10

This configuration achieved the highest test accuracy within the tested parameter space while maintaining balanced performance metrics.

The model was retrained using these parameters and evaluated on the test dataset.

Model Performance

The optimized model achieved approximately 84.5 percent accuracy.

Precision and recall improved slightly relative to the baseline model. Performance remains stronger for the majority class, which is expected given the dataset distribution.

The confusion matrix shows that most misclassifications occur when predicting high income individuals.

Overall performance is strong and stable without excessive complexity.

Feature Importance and Insights

Feature importance analysis shows that only a small number of variables drive most of the predictive power.

Marital or relationship category is the strongest predictor in the model.

Capital gains, occupation level, and education level also have significant influence.

Income prediction is therefore driven primarily by a few dominant socioeconomic variables rather than equal contribution from all features.

This aligns with economic intuition and improves interpretability.

Model Behavior

Accuracy increases as tree depth increases initially. After a moderate depth, improvements slow significantly.

Very deep trees do not produce meaningful accuracy gains and introduce overfitting risk.

The selected depth of 10 provides a strong balance between complexity and generalization.

The tree structure shows clear logical splits that separate high and low income groups based on meaningful categories.

Example Prediction

A new individual profile was passed through the final model.

The model predicted income above 50K with approximately 71 percent probability.

This confirms the pipeline supports end to end inference from raw categorical inputs to probability output.

Why Discretization Was Appropriate

Income outcomes are typically influenced by ranges rather than small numeric variations.

Discretization simplifies decision boundaries and improves interpretability.

If continuous variables were used without binning, the tree could create overly specific numeric thresholds. That would increase complexity and reduce generalization.

Binning reduces noise and supports clearer decision rules.

Runtime and Efficiency

Training a single Decision Tree is computationally fast.

The tuning process required training multiple models sequentially. This increased runtime relative to a single fit but remained efficient overall.

The entire workflow executes comfortably on standard computing hardware.

Conclusion

This project demonstrates a structured machine learning workflow from data validation through final model selection.

The best performing Decision Tree was identified using systematic hyperparameter tuning within a defined search space.

The final model achieves strong accuracy, maintains interpretability, and reflects logical socioeconomic drivers of income classification.

The process was controlled, reproducible, and analytically sound.

This is a complete modeling pipeline rather than a one off experiment.


Authors Christopher Strouse & Jasmine Cheng
