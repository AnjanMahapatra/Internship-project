# Internship-project
Report outline
Introduction: climate and yield forecasting matter for food security.
Data: FAO + World Bank, India, 1990-2013; rainfall, temperature, pesticides, crop type. Cleaning: removed duplicates, averaged to one row per crop-year.
Method: preprocessing (StandardScaler, one-hot), 4 models (Linear, KNN, Random Forest, Gradient Boosting), GridSearchCV.
Key point: a random split puts the same crop-year patterns in train and test (leakage), giving near-perfect R². A time split (train up to 2008, test 2009-2013) simulates real forecasting.
Results: table from results.csv, fig_model_comparison.png, fig_actual_vs_pred.png.
Feature importance: fig_importance.png (crop type dominates; weather effect is small at national level).
Demo: Streamlit app with a what-if climate scenario.
Limitations: national averages, only 24 years, no soil/irrigation/fertilizer data.
Future work: state-level data, satellite NDVI, SHAP, prediction intervals, IoT.
Reference

Hoque et al., "Incorporating Meteorological Data and Pesticide Information to Forecast Crop Yields Using Machine Learning," IEEE Access, vol. 12, 2024.

Actual results from this dataset
India: 4048 rows -> 3384 after duplicates -> 184 unique crop-year rows (8 crops: Cassava, Maize, Potatoes, Rice, Sorghum, Soybeans, Sweet potatoes, Wheat).
Rainfall is constant (1083 mm) for India in every year, so it carries no information. Temperature and pesticides are one national value per year.
Random split (paper style): R2 0.80-0.97. Time split (2009-2013 held out): R2 0.42-0.90.
A baseline that only predicts each crop's average yield gets R2 = 0.895, matching the best ML model. So weather and pesticide features add almost nothing here; crop type explains the variation.
Using last year's yield as a feature improves the forecast (Linear 0.991, Gradient Boosting 0.976).
The paper's 99.99% R2 is not reproducible with an honest evaluation.
