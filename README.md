# Retail Analytics Capstone

**Project Description:** This project focuses on integrated retail analytics to identify anomalous sales behaviour, understand demand patterns, segment stores/departments, and forecast future demand using historical sales and external economic indicators.


**Datasets Used:**
1. **Sales Data:** Weekly sales data for various stores and departments over several years.
2. **Store Information:** Metadata about each store, including type and size.
3. **Features Data:** Additional features such as temperature, fuel price, and holiday indicators that may influence sales.


After thorough understanding of the datasets , we have merged them into a single comprehensive dataset named `final_df`.It was ensured that the merging process preserved all the rows from the sales dataset,as it is the core table for our analysis.



**Anomaly Definition for this project:** An anomaly is a Store-Department-Week observation where weekly sales deviate significatly from the expected behaviour,given historical patterns, seasonality, store characteristics, and external factors.


