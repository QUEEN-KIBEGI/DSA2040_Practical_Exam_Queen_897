# DSA 2040 Practical Exam Submission

## Overview
This repository contains my complete submission for the DSA 2040 Data Warehousing and Data Mining practical exam. The implementation includes all required tasks for both sections:
- **Section 1**: Data Warehousing (Tasks 1-3)
- **Section 2**: Data Mining (Tasks 1-3)

**Task 1**:
## Data Warehousing
     - Designed a star schema for a retail data warehouse to support analytical queries (e.g., sales by product category per quarter).
## 1. Schema Design and Diagram

## 2. Why Star Schema
The star schema was selected because:
1. **Query Simplicity**: Retail analytics require frequent aggregations (e.g., sales by quarter) that star schemas optimize
2. **Performance**: Denormalized dimensions reduce join operations during country/category roll-ups
3. **Maintainability**: Flat dimension tables are easier to ETL than snowflake's normalized structure

## SQL Statements

**Task 2**:
## ETL Process Implementation
    - Implemented an ETL pipeline to generate and load synthetic retail data (1000 rows) into retail_dw.db

**Synthetic Data Generation**:
      Creates realistic retail data with 1000 records
      Includes 5% missing values for realistic handling
      Uses Faker library for realistic descriptions/countries

1. **Extraction and transformation code**
## Transformations:
     Handles missing values
     Calculates TotalSales (Quantity × UnitPrice)
     Filters invalid records and last year of data
     Creates dimension tables (CustomerDim, TimeDim)

2. **Loading to Database**
     Creates SQLite database with proper schema
     Establishes foreign key relationships
     Uses batch loading for efficiency

3. **Logging & Error Handling**:
     Tracks row counts at each stage
     Comprehensive error handling
     Progress logging with timestamps


**Task 3**:
## OLAP Queries and Analysis
      -Executed three OLAP queries (roll-up, drill-down, slice), visualized sales by country, and provided an analysis report.

This notebook executes three OLAP-style SQL queries on the retail data warehouse (`retail_dw.db`) created in Task 2, visualizes the roll-up query result (total sales by country) as a bar chart saved as `task3_sales_by_country.png`, and logs the process. The queries support analysis of sales trends, customer behavior, and product performance.

**Queries**:
1. Roll-up: Total sales by country and quarter.
2. Drill-down: Sales details for the UK by month.
3. Slice: Total sales for electronics (inferred from Description keywords)

**Roll-up**
<img width="922" height="481" alt="image" src="https://github.com/user-attachments/assets/c56f6f6d-6f18-4a92-bcb5-38fdf2a3a2ff" />

**drill-down**

**slice**

**Barchart of sales by Country**


**Report Analysis**

The OLAP queries on the retail data warehouse (retail_dw.db) provide valuable insights into sales trends, customer behavior, and product performance. The roll-up query reveals total sales by country and quarter, highlighting top-performing markets. For instance, countries like the UK and USA likely dominate due to higher transaction volumes, with sales peaking in specific quarters (e.g., Q4 for holiday seasons). This helps the retail company allocate marketing budgets to high-potential regions and optimize seasonal promotions. The drill-down query focuses on UK sales by month, showing detailed transaction patterns, such as spikes in specific months (e.g., December). This granularity aids in identifying customer preferences and optimizing inventory for peak periods. The slice query, targeting electronics-like products (inferred from descriptions containing “device” or “gadget”), shows sales trends for high-value categories, enabling targeted promotions for tech-savvy customers.

The star schema in retail_dw.db, with SalesFact linked to CustomerDim and TimeDim, supports efficient querying for decision-making. The denormalized structure simplifies joins, enabling fast roll-up and drill-down operations, crucial for real-time analytics. However, the synthetic data, generated with faker, may lack real-world nuances (e.g., seasonal patterns or regional preferences), potentially skewing insights. For example, the uniform distribution of countries and dates may not reflect actual market dynamics. Despite this, the warehouse effectively supports strategic decisions like inventory planning, marketing campaigns, and customer segmentation, making it a robust tool for retail analytics.

**Section 2**: Data Mining
**Task 1**:
## Data Preprocessing and Exploration

**Loading and Preprocessing**

**Loading the dataset code**
<img width="1101" height="614" alt="image" src="https://github.com/user-attachments/assets/f6b18972-a0f7-43d8-95c8-651c38feff3f" />

**Preprocess**
<img width="912" height="613" alt="image" src="https://github.com/user-attachments/assets/01ba1b52-3992-4d91-9ef1-05b8791e358b" />

**Explore**
<img width="874" height="593" alt="image" src="https://github.com/user-attachments/assets/cdd7840f-728e-4e12-b969-b814d62cd5e6" />

## Boxplot code
<img width="1003" height="425" alt="image" src="https://github.com/user-attachments/assets/eccf6103-f6bb-45b1-8204-682917f8b5db" />

**Visualizations**
## pairplot
<img width="4111" height="3750" alt="image-4" src="https://github.com/user-attachments/assets/b41cd417-d994-4bfa-914a-27b21c0e3a5c" />

## Correlation heatmap
<img width="2400" height="1800" alt="image-5" src="https://github.com/user-attachments/assets/e22fce41-bbe4-4d45-aadf-867d0eda96d0" />

## Boxplot
<img width="3600" height="1800" alt="image-6" src="https://github.com/user-attachments/assets/06dccc50-64dc-4483-90e9-9c5cc7d264a5" />
**Split Function**
<img width="873" height="436" alt="image-7" src="https://github.com/user-attachments/assets/ee4c0cf5-ae82-4f7c-89b3-317b33f6711d" />

**Outputs**
<img width="901" height="722" alt="image" src="https://github.com/user-attachments/assets/db735326-2ddd-4785-bef4-3a1a56df0b42" />

**Task 2**: Clustering

**Implementation and Metricss**

**Experiment and Visualizations**

**Analysis Report**

## **Analysis Report (150-200 words):**

**Cluster Quality and Misclassifications**
The K-Means clustering (k=3) achieved an Adjusted Rand Index (ARI) of 0.73, indicating good alignment with the true species labels. The visualization shows clean separation between setosa (cluster 0) and the other species, while versicolor and virginica show some overlap, particularly in petal measurements. This matches biological reality where these species are more similar.

**Optimal K Determination**
The elbow curve showed a clear bend at k=3, validating our choice. At k=2, the ARI dropped to 0.54 as versicolor and virginica were forced into one cluster. With k=4, the ARI decreased to 0.65, suggesting over-clustering.

**Real-World Applications**
This technique directly applies to customer segmentation, where distinct groups might exhibit overlapping characteristics. The methodology would help identify:
Core customer profiles
Transitional segments
Outliers requiring special attention

**Synthetic Data Impact**
Using synthetic data would produce more perfectly separated clusters, missing the natural overlap seen in real biological data. This could lead to overestimating clustering algorithm performance in real applications. The current results demonstrate realistic challenges in distinguishing similar categories.
Task 3: Performed classification on the Iris dataset using Decision Tree and KNN classifiers, and association rule mining on synthetic transactional data.

**Recommendations**

Use cluster probabilities rather than hard assignments for borderline cases

Combine with dimensionality reduction for better visualization

Validate with domain experts for real-world applications


**Task 3: Classification and Association Rule Mining**

## Part A: Classification
This notebook implements Task 3 of the DSA 2040 Practical Exam (Section 2: Data Mining).

**Part A: Classification**
- Loads the preprocessed Iris dataset (Min-Max scaled, 80/20 train-test split).
- Trains a Decision Tree classifier, computes metrics (accuracy, precision, recall, F1-score), and visualizes the tree.
- Trains a KNN classifier (k=5), compares performance, and reports the better model.
- Saves the tree visualization as `decision_tree.png`.

**Predict on test set; compute accuracy, precision, recall, F1-score**

**Decision Tree visual**

**Compare with another classifier**


**Part B: Association Rule Mining**
- Generates synthetic transactional data (50 transactions, 3–8 items from 20-item pool with patterns).
- Applies Apriori algorithm (min_support=0.2, min_confidence=0.5) using `mlxtend`.
- Displays top 5 rules by lift and analyzes one rule.
- Saves transactional data as `synthetic_transactions.csv`.

**Dependencies**: `scikit-learn`, `mlxtend`, `matplotlib`, `pandas`, `numpy`.

**Apply Apriori algorithm**
<img width="825" height="593" alt="image-21" src="https://github.com/user-attachments/assets/b5880d35-4904-4d75-937c-a4cb6e60b327" />
<img width="873" height="652" alt="image-22" src="https://github.com/user-attachments/assets/c93e725a-6180-48b2-a18c-fdfcfcce078f" />
<img width="875" height="630" alt="image-23" src="https://github.com/user-attachments/assets/c91ec906-7736-4aad-bfda-c50637f5879e" />
<img width="888" height="632" alt="image-24" src="https://github.com/user-attachments/assets/c0b473b3-ce6a-4418-bdd7-3f1f15a0ef49" />
<img width="1188" height="651" alt="image-25" src="https://github.com/user-attachments/assets/f1ce0059-3878-4d84-a01d-17dc8d053128" />
<img width="1192" height="330" alt="image-26" src="https://github.com/user-attachments/assets/bf9d6736-d92c-4e0c-8233-48a581d194b0" />

## Output
<img width="1417" height="433" alt="image-27" src="https://github.com/user-attachments/assets/66b45a20-fd86-4d6f-8bc0-6ab9c09f5483" />


**Analyze: Discuss one rule's implications**
<img width="978" height="324" alt="image-28" src="https://github.com/user-attachments/assets/05aa6555-a072-48a2-88d2-c0dbf41a9dd7" />
