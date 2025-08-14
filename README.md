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

**Loading**

**Preprocess**

**Visualizations**

**Split Function**

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

**Analyze: Discuss one rule's implications**