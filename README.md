# Retail Analytics Capstone

Github Repository: https://github.com/AnkurBhatt07/Integrated-Retail-Analytics-for-Store-Optimization-and-Demand-Forecasting.git

## Project Overview
This project focuses on integrated retail analytics using historical sales data to understand sales behavior, detect anomalous patterns, perform behavioral segmentation, and build demand forecasting models.  

The goal is to demonstrate an end-to-end data science workflow, starting from raw data integration to anomaly detection, clustering, and time-series forecasting — while maintaining business interpretability and methodological rigor.

---

## Datasets Used
- **Sales Data**  
  Weekly sales data for multiple stores and departments  
  Contains store ID, department ID, weekly sales, date, and holiday indicator  
  Acts as the core transactional table  

- **Store Information**  
  Metadata for each store  
  Includes store type and store size  
  Captures structural differences across stores  

- **Features Data**  
  External and contextual variables that may influence sales  
  Includes temperature, fuel price, CPI, unemployment rate, markdown information, and holiday flags  

---

## Data Integration and Initial Processing
- All three datasets merged using **Store** and **Date** as primary keys  
- Sales data treated as the base table  
- Left joins ensured no loss of sales records  
- Date columns converted to datetime format  
- Merged dataset saved for reproducibility  

This integrated dataset became the foundation for feature engineering, anomaly detection, segmentation, and forecasting.

---

## Anomaly Definition
A **Store–Department–Week** observation where weekly sales deviate significantly from expected behavior, given historical trends, short-term dynamics, promotional context, and external factors.  

This emphasizes contextual and temporal deviations, not merely statistical extremes.

---

## Feature Engineering and Exploratory Analysis
Key engineered features:
- **Lag features**: Lag_1, Lag_4, Lag_52 (short-term + yearly seasonality)  
- **Rolling statistics** (leakage-free): Rolling_Mean_4, Rolling_Std_4  
- **Percentage Deviation** from rolling baseline  
- **Markdown indicator**: Has_Markdown  
- **Time-based features**: Week, Month, Year  

The engineered dataset was saved for modular workflow continuity.

---

## Model-Based Anomaly Detection
Two complementary unsupervised methods:
- **Isolation Forest** → detects global anomalies  
- **Local Outlier Factor (LOF)** → detects local density-based anomalies  

**High-Confidence Anomalies**:  
A record is labeled anomalous only if both methods agree.  

### Key Findings
- Anomalies are rare (<1%)  
- Certain stores show higher anomaly rates  
- Anomalies cluster around promotional and seasonal periods  
- Extended lag features reduce forecasting error on anomalous weeks  

The anomaly-enriched dataset was saved for downstream segmentation and forecasting.

---

## Store-Level Segmentation
Aggregated store-level features:
- Mean sales  
- Sales volatility (std)  
- Percentage deviation behavior  
- Anomaly rates  
- Markdown frequency  
- Holiday sales proportion  
- Store size  

**Clustering Approach**:  
- KMeans clustering with power transformation  
- Final selection: **6 clusters**  
- Metrics: Silhouette, Davies-Bouldin, Calinski-Harabasz  

### Cluster Insights
- Large, high-volume volatile stores  
- Mid-volume stable stores  
- Small promotion-sensitive stores  
- Behaviorally distinct groups  

---

## Store–Department Segmentation
- KMeans clustering on Store–Dept aggregated features  
- Final selection: **4 clusters**  
- Improved silhouette score (~0.36)  
- Captured intra-store heterogeneity  

---

## Demand Forecasting
**Strategy**:
- Time-aware train-test split (last 12 weeks holdout)  
- Leakage-free rolling features  
- Autoregressive lag-based modeling  
- Baseline comparison against Rolling Mean  

**Models Evaluated**:
- Baseline: Rolling_Mean_4  
- Gradient Boosting Regressor  

### Forecasting Experiments
- **Experiment 1**: Base features (Lag_1, rolling stats, economic indicators, store cluster)  
- **Experiment 2**: Extended lags (Lag_4, Lag_52) → improved performance  

### Results
- Baseline: MAE ≈ 1580, RMSE ≈ 3622, R² ≈ 0.97  
- Extended ML Model: MAE ≈ 1446, RMSE ≈ 3130, R² ≈ 0.98  

Residual analysis showed reduced variance, with larger errors during anomaly weeks.

---

## Business Insights
- Sales behavior is largely autoregressive  
- Promotion-driven clusters are more volatile and harder to forecast  
- Yearly lag features significantly enhance forecasting accuracy  
- Simple baselines are strong competitors — ML must be rigorously benchmarked  

---

## Final Artifacts Saved
- Feature-engineered dataset  
- Anomaly-enriched dataset  
- Store segmentation dataset  
- Store–Dept segmentation dataset  
- Final trained Gradient Boosting model  
- Feature list used for forecasting  

---

## Conclusion
This project demonstrates a complete applied machine learning pipeline in retail analytics:
- Data integration  
- Behavioral feature engineering  
- Unsupervised anomaly detection  
- Behavioral segmentation  
- Time-aware demand forecasting  
- Model evaluation and diagnostics  

**Emphasis**:  
- Avoiding data leakage  
- Robust benchmarking  
- Business interpretability  
- Methodological clarity  