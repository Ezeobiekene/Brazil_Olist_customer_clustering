# Enterprise Customer Segmentation & Supply Chain Analytics (Olist E-Commerce)

##  Project Overview
This project transforms raw, multi-table relational transaction data from Olist (the largest e-commerce marketplace in Brazil) into an actionable, enterprise-level customer segmentation engine. By engineering an **RFM (Recency, Frequency, Monetary)** framework combined with advanced unsupervised machine learning, this pipeline automates the identification of high-value consumer personas, at-risk accounts, and localized logistical bottlenecks to drive targeted marketing spend and operational improvements.

---

## Tech Stack & Architecture
* **Language:** Python 3.13
* **Data Manipulation:** Pandas, NumPy
* **Machine Learning:** Scikit-Learn (K-Means, DBSCAN, Isolation Forest, StandardScaler)
* **Data Visualization:** Plotly Express, Plotly Graph Objects, Seaborn, Matplotlib


## Key Technical Implementation Steps

### 1. Relational Schema Merging & Deduplication
Stitched together 8 separate relational data tables (Orders, Customers, Items, Payments, Reviews, Products, Categories, and Sellers) using precise `inner` and `left` join constraints. Implemented preemptive Pandas `.groupby()` aggregation routines on the transaction tables to eliminate "one-to-many" fan-out, ensuring item frequencies and currency volumes were never artificially inflated.

### 2. Multi-Dimensional Outlier Mitigation
Transaction databases are plagued by extreme outliers (bulk distributors/institutional orders). Trained an **Isolation Forest** classifier to isolate and drop the top 3% multi-dimensional anomalies, preventing severe distortion of downstream clustering centroids.

### 3. Feature Scaling & Hyperparameter Optimization
Applied a `StandardScaler` to uniformize variance across the highly skewed Monetary and Frequency boundaries. Validated the optimal cluster count mathematically by plotting the **Elbow Method (Inertia)** against **Silhouette Scores** side-by-side, proving **$K=4$** provided the ultimate balance of compact geometric density and clear business separation.

### 4. Algorithmic Benchmarking
Evaluated **K-Means Clustering** against density-based **DBSCAN**. K-Means successfully partitioned the workspace into 4 robust consumer segments, while DBSCAN acted as an excellent baseline to identify sparse noise boundaries.

---

## Business Personas Discovered
Through the final K-Means assignment, the customer base was classified into four distinct operational cohorts:
* **The Champions:** Low recency, high frequency, and maximum financial footprint. (High-priority VIP perks).
* **The Loyal Budget Shoppers:** Frequent repeat visitors who consistently buy lower-priced items. (Upselling/cross-selling targets).
* **The At-Risk Big Spenders:** Customers who spent heavily on single transactions long ago but have stalled. (Win-back discount campaigns).
* **The Inactive One-Timers:** Historic low-value, single-purchase shoppers. (Low-priority automated marketing triggers).

---

## Key Insights & Portfolio Visualizations
* **The Radar Matrix:** Built an interactive `plotly.graph_objects.Scatterpolar` visualization displaying the averaged, scaled RFM dimensions to map persona silhouettes clearly.
* **Logistical Friction Analysis:** Computed delivery latency parameters (`order_estimated_delivery_date` vs. `order_delivered_customer_date`) and aggregated them by Brazilian state. Plotted these against `review_score` averages to visually map how geographic delivery bottlenecks negatively correlate with customer satisfaction ratings.

---