# Predictive_Maintenance_Project_Summary_with_Visualizations
Predictive Maintenance Project Summary Here’s a detailed summary of my results, key findings, and insights from the predictive maintenance project using the AI4I 2020 Predictive Maintenance Dataset from the UC Irvine Machine Learning Repository. Project Overview In this project, I aimed to develop a predictive maintenance model to proactively detect equipment failures, thereby reducing unplanned downtime and enhancing operational efficiency. I used the AI4I 2020 Predictive Maintenance Dataset from the UC Irvine Machine Learning Repository, which provided machine sensor readings and operational metrics relevant to failure prediction. My approach included systematic steps: data cleaning, feature engineering, model selection and evaluation, hyperparameter tuning, and deployment for real-time monitoring. By iterating through each step, I refined the model to maximize its reliability in identifying potential failures.

Data Cleaning and Feature Engineering Data Cleaning: I first ensured the data was clean and free from missing values. Recognizing that extreme values in features like Rotational Speed [rpm] and Torque [Nm] could introduce noise, I applied a 99th percentile cap on outliers. This capping was critical to ensure that my model focused on generalizable patterns rather than rare anomalies.
Feature Engineering: To enhance the model’s predictive power, I engineered several features: Temperature Delta: Calculated as the difference between process and air temperature, this feature captures overheating potential, a known precursor to failure. Vibration Indicator: This feature combines rotational speed and torque to represent machine vibration, which reflects mechanical stress that can wear down equipment. Tool Wear Level: By categorizing tool wear into 'Low Wear,' 'Medium Wear,' and 'High Wear,' I simplified this variable, making it more interpretable while retaining its predictive relevance.

Through this process, I observed that these new features improved the model’s understanding of complex mechanical and thermal stresses, which are key indicators of equipment health.

Model Selection and Performance Comparison
I evaluated multiple models to find the one most capable of accurately predicting failures: Logistic Regression: This model yielded an F1 score of 0.214, indicating limited ability to capture failure cases in an imbalanced dataset. Random Forest and Gradient Boosting: Both models performed considerably better, with cross-validated F1 scores of 0.734 and 0.731, respectively. LightGBM: This model was the top performer with an F1 score of 0.69, balancing precision and recall effectively, and a recall rate of 82%.

Insight: The results showed that while ensemble models like Random Forest and Gradient Boosting had strong performance, LightGBM offered the best balance of recall and precision, making it ideal for minimizing false negatives in a maintenance context.
Feature Importance Analysis
Using the Random Forest model, I explored feature importance to understand which variables most impacted failure predictions. This analysis highlighted: Vibration Indicator: Ranked as the most important feature, it underscored the role of mechanical stress in equipment failure. Temperature Delta: Also highly influential, indicating that temperature fluctuations contribute to stress. Torque: Reflects operational force, suggesting that load-related stresses impact machine longevity.

Insight: This feature importance analysis validated that mechanical and thermal stress markers were essential indicators of failure risk, helping guide operational monitoring.

Precision-Recall Analysis and Confusion Matrix Insights Precision-Recall Curve: The curve illustrated the balance between precision (minimizing false positives) and recall (minimizing false negatives). I achieved a balance that captured most failures without significantly inflating false alerts.
Confusion Matrix: Provided an in-depth look at the model’s performance in detecting failures and avoiding false positives: True Positives (TP): Correctly predicted failures, enabling proactive maintenance. False Positives (FP): Non-failures predicted as failures, acceptable to prevent downtimes. True Negatives (TN): Accurate predictions of non-failures, reducing unnecessary checks. False Negatives (FN): Missed failures, which are critical to minimize.

Insight: The model achieved a high recall (82%) with reasonable precision (59%), ensuring that most failures were detected while avoiding an excessive false alarm rate.

Hyperparameter Tuning and Final Model Selection Using GridSearchCV, I optimized LightGBM’s parameters (num_leaves, max_depth, learning_rate, and n_estimators), enhancing its accuracy and reliability. The final tuned LightGBM model showed robust reliability in both recall and precision, solidifying it as the most suitable model for this project.
Insight: Hyperparameter tuning allowed LightGBM to better capture complex, subtle failure patterns. This adjustment enhanced recall and precision, aligning the model with the practical demands of predictive maintenance.

Deployment for Real-Time Monitoring and Alerting Using FastAPI, I deployed the model as a REST API endpoint that accepts real-time sensor data and returns predictions. The API generates alerts if a failure is likely, allowing maintenance teams to take preemptive action.
Insight: Real-time deployment transforms the model into a proactive monitoring system. By continuously analyzing incoming data and generating alerts, the system enables teams to prevent failures, enhance equipment longevity, and reduce unexpected downtimes.

Overall Project Summary and Key Takeaways Critical Indicators of Failure: Features related to mechanical and thermal stress—especially vibration, temperature differences, and torque—are primary predictors of failure. These should be continuously monitored for early signs of wear.

Model Selection: LightGBM’s performance and adaptability to imbalanced data made it the most suitable choice, especially after tuning. It achieved a strong recall, ensuring that most failure cases are detected.

Balance of Precision and Recall: By optimizing for recall, I minimized missed failures, addressing a primary concern in predictive maintenance.

Real-Time Predictive Maintenance: The FastAPI deployment enables the model to provide continuous, actionable insights, empowering maintenance teams to act on failure predictions before breakdowns occur.

Comprehensive Summary of the Visualization Analysis
In this analysis, I conducted univariate analysis, bivariate analysis, correlation analysis, and a Chi-Square Test to understand the relationships between features and the target variable, Machine failure.

Univariate Analysis
I started by exploring the distributions of key numerical features (Air temperature [K], Process temperature [K], Rotational speed [rpm], Torque [Nm], and Tool wear [min]).
Air and Process Temperatures: These variables showed narrow ranges, indicating stable operating conditions.
Rotational Speed and Torque: These were more variable, suggesting diverse operational states.
Tool Wear: This feature was skewed, with most observations clustered at lower wear levels.
For the target variable, Machine failure, the count plot revealed a significant class imbalance, with far fewer failure cases (1) compared to non-failures (0). This imbalance highlights the need for techniques like SMOTE during modeling.


Bivariate Analysis
I examined the relationships between numerical features and Machine failure using boxplots:
Tool Wear: Machines with higher tool wear were more likely to fail, reinforcing the importance of wear monitoring.
Torque and Rotational Speed: Variations in these features were associated with failures, suggesting operational stress impacts.
Temperatures: Slight increases in process temperature were linked to failures, indicating potential overheating issues.

Correlation Analysis
I computed a correlation heatmap to quantify relationships:
Process and Air Temperatures: Strongly correlated (0.97), indicating dependency.
Tool Wear and Machine Failure: Weak but positive correlation (0.18), reinforcing its predictive relevance.
Torque and Machine Failure: Moderate correlation (0.15), further highlighting its role in predicting failures.

Chi-Square Test
To analyze categorical relationships, I conducted a Chi-Square Test between failure types (TWF, HDF, PWF, OSF, RNF) and Machine failure:
Significant Relationships:
TWF (Tool Wear Failure): Chi-Square = 409.73, p < 0.001
HDF (Heat Dissipation Failure): Chi-Square = 143.29, p < 0.001
PWF (Power Failure): Chi-Square = 238.95, p < 0.001
OSF (Overstrain Failure): Chi-Square = 171.64, p < 0.001
These failures are significantly associated with Machine failure, confirming their critical role in breakdowns.
Non-Significant Relationship:
RNF (Random Failure): Chi-Square = 0.0, p = 1.0. This failure type appears unrelated to the target variable.


My Interpretation from these analyses:
Tool Wear is the most critical factor, with strong associations across bivariate and Chi-Square analyses.
Torque and Rotational Speed are operational stress indicators linked to failures.
Random failures (RNF) are independent of other features and unpredictable.
Correlation analysis further validated the importance of features like Tool Wear and Torque.
These insights highlight key failure drivers and provide actionable direction for feature prioritization in predictive maintenance modeling. This comprehensive analysis bridges exploratory insights with statistical consistency, ensuring strong bases for the next modeling phase.
Bivariate analysis revealed clear patterns, particularly with Tool wear [min] and Torque [Nm], showing their significance in predicting failures. These insights reinforce the need to focus on these variables in predictive maintenance strategies, as they are critical indicators of machine health.
The Chi-Square Test confirmed that failure types like tool wear, heat dissipation, power, and overstrain failures are strongly associated with machine failures. This insight emphasizes the importance of monitoring these failure types to predict and prevent equipment breakdowns. However, random failures (RNF) are not associated with the target variable, suggesting they may stem from unpredictable, external factors. These findings will guide feature prioritization in model development.

This project demonstrates the potential of machine learning in proactive maintenance, combining feature engineering, robust modeling, and deployment for real-time monitoring. The predictive maintenance model developed here allows maintenance teams to take data-driven actions that prevent equipment failures, optimize resource allocation, and ultimately improve operational efficiency.
