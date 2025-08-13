# Energy Consumption and Electricity Cost Estimation – Taiwan ETC

## Overview
This project presents a predictive model designed to estimate daily electricity consumption and associated costs for Taiwan’s **Electronic Toll Collection (ETC)** system.  
By leveraging temperature and infrastructure data, the model aims to forecast energy demand, enabling improved planning, operational efficiency, and cost optimization.

## Dataset
The dataset, provided by the course instructor, consists of:
- Two months of electricity billing records.
- Minute-level voltage and current sensor data from ETC stations.
- Daily temperature data from **19 meteorological stations** across Taiwan.

## Data Preprocessing
1. **Weather Data Transformation**  
   Converted meteorological datasets from a matrix format (days × months) into a tabular structure containing:
   - Date  
   - Temperature  
   - Station name  
   - Station ID  
   - Latitude and longitude  
   
2. **Merging Infrastructure and Billing Data**  
   Aggregated hourly electricity usage from ETC stations (server shelter + gantry) into daily totals and merged them with the billing dataset.

3. **Geographical Matching**  
   Linked each gantry to its nearest meteorological station using latitude and longitude coordinates.

## Model
We implemented the **CatBoost Regressor**, a decision tree–based machine learning algorithm known for handling both numerical and categorical features effectively.

**Key configuration details:**
- Tuned for capturing non-linear daily patterns.
- Applied regularization to prevent overfitting.
- Progressive learning over 1000 iterations.
- Training restricted to 2024 data to maintain test set integrity.

## How It Works
- Learns consumption patterns from daily historical data.
- Builds multiple small decision trees, each improving the accuracy of the previous ones.
- Combines the predictions of all trees to produce the final output.

## Key Findings
- **Temperature Effect:** Higher temperatures lead to increased electricity consumption, especially in summer.
- **Lane Count Effect:** Stations with more lanes consume more energy on average.
- **Combined Effect:** High temperatures combined with high lane counts significantly raise consumption.

## Evaluation Metrics
- **R² (Explained Variance):** Measures the proportion of variance captured by the model (close to 1 indicates excellent fit).
- **RMSE (Root Mean Squared Error):** Quantifies error magnitude, penalizing large deviations.
- **MAE (Mean Absolute Error):** Reports average prediction error in kWh.
- **Accuracy (% vs. Real Billing):** Compares predictions against actual billed values.

## Results
- Tested on billing periods from late 2024 to early 2025.
- Achieved **over 80% accuracy** with low prediction errors.
- Proven reliability for energy demand forecasting in real-world operational scenarios.

## Repository Structure
- `Code.ipynb` – Main Jupyter Notebook for training, testing, and evaluating the model.
- `training_ready_dataset_balltree.csv` – Final preprocessed dataset.
- `daily_predictions.csv` – Predicted daily electricity usage.
- `all_gantries_period_predictions_with_accuracy.csv` – Gantry-level predictions with accuracy metrics.
- `Electricity data of the toll station-phase 1.xlsx` – Original infrastructure and billing data.
- `Project_Presentation.pdf` – Full project presentation slides.
- `catboost_info/` – Directory containing CatBoost training logs and metadata.

## Conclusion
This project demonstrates the feasibility of using machine learning, specifically **CatBoost**, to forecast energy consumption for large-scale infrastructure. By integrating environmental and structural variables, the model provides valuable insights for improving energy efficiency and cost control.
