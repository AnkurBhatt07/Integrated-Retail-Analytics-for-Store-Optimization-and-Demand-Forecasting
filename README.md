# Retail Analytics Capstone

## Project Overview
This project focuses on integrated retail analytics using historical sales data to understand sales behavior, detect anomalous patterns, and build a strong foundation for segmentation and demand forecasting.  
The goal is to demonstrate an end-to-end data science workflow, starting from raw data integration to advanced machine learning–based anomaly detection, while keeping business interpretability at the core.

---

## Datasets Used

### Sales Data
- Weekly sales data for multiple stores and departments  
- Contains information such as store ID, department ID, weekly sales, date, and holiday indicator  
- This dataset acts as the core transactional table  

### Store Information
- Metadata for each store  
- Includes store type and store size  
- Helps in understanding structural differences between stores  

### Features Data
- External and contextual variables that may influence sales  
- Includes temperature, fuel price, CPI, unemployment rate, markdown information, and holiday flags  

---

## Data Integration and Initial Processing
After a thorough inspection of all three datasets, they were merged into a single comprehensive dataset using Store and Date as the primary keys.

**Key points of the integration process:**
- The sales dataset was treated as the core table  
- A left join strategy was used to ensure no sales records were lost  
- Date columns were parsed correctly to support time-based analysis  
- The merged dataset serves as the foundation for all further analysis  
- The integrated dataset was saved for reuse to ensure reproducibility and modularity across notebooks  

---

## Anomaly Definition (Project-Specific)
For this project, an anomaly is defined as:

> A Store–Department–Week observation where weekly sales deviate significantly from the expected behavior, given historical sales patterns, short-term trends, store characteristics, promotional activity, and external economic factors.

This definition emphasizes contextual and temporal anomalies, rather than treating anomalies as simple extreme values.

---

## Feature Engineering and Exploratory Analysis (Notebook-2)
In the second stage of the project, extensive exploratory data analysis (EDA) and feature engineering were performed to better understand sales behavior and prepare the data for anomaly detection.

**Key steps included:**
- Handling missing values, especially in markdown-related features  
- Creating time-based features such as week, month, and year (used later for forecasting)  
- Engineering behavioral features such as:  
  - Rolling mean and rolling standard deviation of weekly sales  
  - Lagged sales values  
  - Percentage deviation from recent sales trends  
- Encoding categorical variables in a model-ready format  
- Saving the feature-engineered dataset for downstream tasks  

**EDA revealed:**
- Strong seasonality effects  
- Holiday-driven sales spikes  
- Varying levels of volatility across stores and departments  

---

## Model-Based Anomaly Detection (Notebook-3)
The third notebook focuses on formal anomaly detection using machine learning techniques, building upon the engineered features.

### Anomaly Detection Techniques Used
- **Isolation Forest**  
  - Captures global anomalies that differ significantly from the overall data distribution  
  - Scales well to large datasets  

- **Local Outlier Factor (LOF)**  
  - Identifies contextual anomalies based on local density deviations  
  - Useful for detecting subtle, neighborhood-level irregularities  

### Feature Selection Rationale
- Only behavioral and contextual features were used for anomaly detection  
- Identifiers (such as Store ID and Department ID), calendar variables (week/month/year), and diagnostic features (such as Z-score) were deliberately excluded to avoid artificial distance relationships, seasonal bias, and circular reasoning  

---

## High-Confidence Anomalies
To improve robustness and interpretability, a High-Confidence Anomaly label was created:

> A data point is considered high-confidence anomalous only if both Isolation Forest and LOF identify it as an anomaly.

This produces a small, highly reliable set of anomalous observations suitable for business investigation.

---

## Key Outcomes
- Anomalies were found to be rare, which is expected in real retail data  
- Certain stores exhibited higher anomaly rates, indicating irregular or volatile sales behavior  
- Time-based analysis showed that anomalies often cluster around specific periods, such as promotional or holiday weeks  
- The anomaly-enriched dataset was saved for use in subsequent segmentation and forecasting stages  