Energy Consumption and Electricity Cost Estimation – Taiwan ETC
Overview
This project develops a predictive model to estimate daily electricity consumption and costs for Taiwan’s Electronic Toll Collection (ETC) system.
The objective is to forecast energy demand using temperature and infrastructure data, enabling more efficient planning and cost optimization.

Dataset
The dataset, provided by the instructor, includes:

Two months of electricity billing records.

Minute-level voltage and current sensor data.

Daily temperature readings from 19 meteorological stations across Taiwan.

Data Preprocessing
Transformed meteorological data from matrix format (days vs. months) into tabular format containing:

Date

Temperature

Station name

Station ID

Latitude and longitude

Merged ETC station data (server shelter + gantry structure) with billing data by aggregating hourly consumption to daily totals for each gantry.

Matched each gantry to its nearest meteorological station using latitude and longitude.

Model
The model used is CatBoost Regressor, a decision tree–based machine learning algorithm capable of handling both numeric and categorical data efficiently, and performing well in non-linear scenarios.

Key settings:

Tuned for non-linear daily patterns.

Regularization to prevent overfitting.

Progressive learning over 1000 iterations.

Only 2024 data used to preserve future test integrity.

How It Works
Learns from daily patterns in energy usage.

Builds many small trees, each improving upon the last.

Combines results from all trees to produce the final prediction.

Key Findings
Temperature Effect: Energy consumption rises with higher temperatures, especially in summer.

Lane Count Effect: More lanes in a gantry generally lead to higher electricity consumption.

Combined Effect: High temperatures and many lanes together result in significantly increased energy demand.

Evaluation Metrics
R² (Explained Variance): Measures how well the model captures overall patterns (higher is better; close to 1 is excellent).

RMSE (Root Mean Squared Error): Quantifies prediction error magnitude, penalizing large deviations.

MAE (Mean Absolute Error): Average prediction error in kWh.

Accuracy (% vs. Real Billing): How close predictions are to actual billed values.

Results
Tested on real billing periods from late 2024 to early 2025.

Achieved over 80% accuracy with small prediction errors.

Demonstrated reliability for energy forecasting in real-world conditions.

Files in This Repository
Code.ipynb – Main Jupyter Notebook with model training and evaluation.

training_ready_dataset_balltree.csv – Final preprocessed dataset ready for training.

daily_predictions.csv – Predicted daily consumption values.

all_gantries_period_predictions_with_accuracy.csv – Predictions per gantry with accuracy scores.

Electricity data of the toll station-phase 1.xlsx – Raw billing and sensor data.

Project_Presentation.pdf – Presentation summarizing the project.

catboost_info/ – CatBoost model details and logs.

Conclusion
The project successfully demonstrates the feasibility of predicting ETC system electricity usage with high precision using environmental and infrastructure data. These insights can help optimize energy efficiency and reduce operational costs.
