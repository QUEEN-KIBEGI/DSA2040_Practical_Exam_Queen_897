## DSA 2040 Practical Exam Submission

## Overview
This repository contains my complete submission for the DSA 2040 Data Warehousing and Data Mining practical exam. The implementation includes all required tasks for both sections:


**Section 1**: Data Warehousing (Tasks 1-3)

**Section 2**: Data Mining (Tasks 1-3)

**Task 1**:
## Data Warehousing
 Designed a star schema for a retail data warehouse to support analytical queries (e.g., sales by product category per quarter).
## 1. Schema Design and Diagram
## Star Schema Design
## Fact Table
<img width="808" height="321" alt="image" src="https://github.com/user-attachments/assets/11dd832d-4076-4fce-81c7-14741ed12095" />
## Dimension tables
<img width="976" height="624" alt="image" src="https://github.com/user-attachments/assets/060cfa7a-beb0-4278-abd9-e9427b5d8cdd" />

## Handdrawn Diagram
![WhatsApp Image 2025-08-12 at 22 38 50_28597dab](https://github.com/user-attachments/assets/7ff754df-499e-49de-8a1b-a58ef9766ac5)


## 2. Why Star Schema
The star schema was selected because:
1. **Query Simplicity**: Retail analytics require frequent aggregations (e.g., sales by quarter) that star schemas optimize
2. **Performance**: Denormalized dimensions reduce join operations during country/category roll-ups
3. **Maintainability**: Flat dimension tables are easier to ETL than snowflake's normalized structure

## SQL Statements
<img width="1027" height="810" alt="image" src="https://github.com/user-attachments/assets/08f7b557-5a95-469b-9624-9dcfee918d17" />
<img width="864" height="322" alt="image" src="https://github.com/user-attachments/assets/6d407943-7120-40e7-83ba-35482ac5bf9a" />


**Task 2**:
## ETL Process Implementation
Implemented an ETL pipeline to generate and load synthetic retail data (1000 rows) into retail_dw.db

**Synthetic Data Generation**:
      Creates realistic retail data with 1000 records
      Includes 5% missing values for realistic handling
      Uses Faker library for realistic descriptions/countries

1. **Extraction and transformation code**
   ## Extraction
   <img width="1105" height="646" alt="image" src="https://github.com/user-attachments/assets/2e53002f-4a18-4673-85f8-9b4c26cdc005" />

## Transformations:
     Handles missing values
     
     Calculates TotalSales (Quantity × UnitPrice)
     
     Filters invalid records and last year of data
     
     Creates dimension tables (CustomerDim, TimeDim)
     
<img width="991" height="599" alt="image" src="https://github.com/user-attachments/assets/64dea210-cc28-4df6-8776-206849657043" />
<img width="914" height="681" alt="image" src="https://github.com/user-attachments/assets/0fb08636-9f3b-4f94-ba9a-29eaedafafc5" />

2. **Loading to Database**
     Creates SQLite database with proper schema
     Establishes foreign key relationships
     Uses batch loading for efficiency
<img width="962" height="767" alt="image" src="https://github.com/user-attachments/assets/fc222132-7658-44e5-833d-9f02985aeefb" />
<img width="909" height="728" alt="image" src="https://github.com/user-attachments/assets/36588c45-16c4-45b8-a970-8dedbeba04db" />

3. **Function to perform all ETL**
   **Error checks**:
  ## Missing value handling
  ## Data type validation (e.g., InvoiceDate as datetime)
   ## Foreign key integrity
   <img width="937" height="636" alt="image" src="https://github.com/user-attachments/assets/f1a4e879-794b-4fcf-9ee7-053ee0bf3e1a" />

4. **Logging and comments**:
     Tracks row counts at each stage
     Comprehensive error handling
     Progress logging with timestamps
## Logging
<img width="884" height="281" alt="image" src="https://github.com/user-attachments/assets/ec196ea1-b704-440d-96d4-241efda7b50c" />
# Sample result log
<img width="782" height="401" alt="image" src="https://github.com/user-attachments/assets/824f02e5-118f-4998-b6d9-ea9dae4d8ea8" />

# Comments
<img width="909" height="246" alt="image" src="https://github.com/user-attachments/assets/8faf5146-3309-4354-a1dc-b7d9a9a8453d" />


**Task 3**:
## OLAP Queries and Analysis
Executed three OLAP queries (roll-up, drill-down, slice), visualized sales by country, and provided an analysis report.

This notebook executes three OLAP-style SQL queries on the retail data warehouse (`retail_dw.db`) created in Task 2, visualizes the roll-up query result (total sales by country) as a bar chart saved as `task3_sales_by_country.png`, and logs the process. The queries support analysis of sales trends, customer behavior, and product performance.

**Queries**:
1. Roll-up: Total sales by country and quarter.
2. Drill-down: Sales details for the UK by month.
3. Slice: Total sales for electronics (inferred from Description keywords)

**Roll-up**
<img width="922" height="481" alt="image" src="https://github.com/user-attachments/assets/c56f6f6d-6f18-4a92-bcb5-38fdf2a3a2ff" />
<img width="904" height="233" alt="image" src="https://github.com/user-attachments/assets/ff80474a-0f89-4144-9aca-86d63e0107bb" />

**drill-down**
<img width="1077" height="500" alt="image" src="https://github.com/user-attachments/assets/25a8f294-4ab4-448f-8b20-d361e1357d5b" />
<img width="1022" height="216" alt="image" src="https://github.com/user-attachments/assets/26302f96-b467-4ef0-9e27-0eeff81ef55a" />

**slice**
<img width="926" height="479" alt="image" src="https://github.com/user-attachments/assets/f36bf2df-7b73-4c28-8d6c-b121a5aaf508" />
<img width="1015" height="155" alt="image" src="https://github.com/user-attachments/assets/bbf2844b-74cc-4f83-92a2-94de7ddeddac" />

**Barchart of sales by Country**
<img width="1000" height="600" alt="image" src="https://github.com/user-attachments/assets/45404168-ec0c-4ca7-9ac9-7d722b75ee5c" />


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
<img width="1146" height="795" alt="image" src="https://github.com/user-attachments/assets/e3bec549-9f19-4e6d-bfba-a48463c94c84" />
<img width="974" height="799" alt="image" src="https://github.com/user-attachments/assets/d12ca85b-3330-4b21-9083-bad4a6c49876" />
<img width="968" height="615" alt="image" src="https://github.com/user-attachments/assets/cab9372c-054c-451e-b6e2-980a596efdcf" />

<img width="959" height="370" alt="image" src="https://github.com/user-attachments/assets/ccf286b3-18bd-48fb-9d9a-d369a1b88b11" />

**Experiment and Visualizations**
**Experiment**
<img width="653" height="138" alt="image" src="https://github.com/user-attachments/assets/7076b1bc-086b-4d7e-b35b-631f5024d6e1" />
<img width="609" height="154" alt="image" src="https://github.com/user-attachments/assets/b2f320f2-7e43-412e-864a-5e8077816bb1" />
**Visualization**
## Elbow curve
<img width="2400" height="1500" alt="image-13" src="https://github.com/user-attachments/assets/cda7101b-c74e-4453-9320-aedd39bbb523" />

## Visualize clusters
<img width="3000" height="1800" alt="image-14" src="https://github.com/user-attachments/assets/925137e7-b14a-4f94-a9dd-85a3a67b5cba" />

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
**codes**
<img width="1074" height="799" alt="image" src="https://github.com/user-attachments/assets/bf4a4674-c3ff-4d8d-9fcb-d31fe08d6993" />
<img width="792" height="339" alt="image" src="https://github.com/user-attachments/assets/29ae038c-1241-4384-b0e7-050a9c6b7703" />

**Results for accuracy, precision, recall, F1-score**
<img width="760" height="364" alt="image" src="https://github.com/user-attachments/assets/9a6c59ae-fc3e-4b4b-ad9d-e9767af933ca" />

**Decision Tree visual**
<img width="6000" height="3000" alt="image-19" src="https://github.com/user-attachments/assets/c1cb9e61-485c-4077-ac53-9fae29b35e77" />

**Compare with another classifier (e.g., KNN with k=5); report which is better and why**
<img width="1128" height="271" alt="image" src="https://github.com/user-attachments/assets/c30963dd-25a8-44ca-8bc4-b3b763494191" />

**Analysis Report**
**Part A: Classification Results**
  ## The Decision Tree achieved 96.7% accuracy with clear decision boundaries visualized in the tree diagram. Key splits used petal measurements, showing their importance in species classification. The KNN classifier (k=5) performed slightly better (100% accuracy) due to:
  ## Inherited cluster structure from the data
 ## Similarity-based approach working well with distinct species groupings
  ## No overfitting with small k-value
   ## However, the Decision Tree provides better interpretability - we can see that petal width ≤ 0.8 cm perfectly identifies setosa, while virginica requires petal length > 4.95 cm.

**Part B: Association Rule Mining**
-Generates synthetic transactional data (50 transactions, 3–8 items from 20-item pool with patterns).
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

**Tools Used**
## Python 3.x
Purpose: Core programming language for all tasks.
Usage: Used to write scripts and notebooks (e.g., task1_data_warehouse_design.ipynb, etl_retail.py, task3_olap_analysis.ipynb, mining_iris_basket.ipynb).
## Jupyter Notebook
Purpose: Interactive environment for developing and documenting Python code.
Usage: Used to create and run .ipynb files (e.g., task1_data_warehouse_design.ipynb, task3_olap_analysis.ipynb, mining_iris_basket.ipynb) with markdown cells and code execution.
## SQLite
Purpose: Lightweight relational database management system.
Usage: Used to create and manage databases (retail_warehouse.db for Task 1, retail_dw.db for Tasks 2 and 3) with SQL queries.
## DB Browser for SQLite
Purpose: GUI tool for viewing and verifying database contents.
Usage: Recommended for inspecting table structures and data in retail_warehouse.db and retail_dw.db (e.g., screenshots for large files).
## Draw.io
Purpose: Online diagramming tool.
Usage: Used to create the star_schema_diagram.png for visualizing the star schema design.
## pandas
Purpose: Python library for data manipulation and analysis.
Usage: Used for data frame operations in ETL (etl_retail.py), OLAP queries (task3_olap_analysis.ipynb), and transactional data handling (mining_iris_basket.ipynb).
## numpy
Purpose: Python library for numerical computations.
Usage: Used for random number generation and array operations in synthetic data creation (etl_retail.py, mining_iris_basket.ipynb).
## faker
Purpose: Python library for generating synthetic data.
Usage: Used to create realistic retail data (e.g., Description, CustomerID) in etl_retail.py.
## matplotlib
Purpose: Python library for data visualization.
Usage: Used to create bar charts (task3_sales_by_country.png) and Decision Tree visualization (decision_tree.png).
## mlxtend
Purpose: Python library for machine learning extensions.
Usage: Used for Apriori algorithm (apriori, association_rules) and transaction encoding (TransactionEncoder) in mining_iris_basket.ipynb.
## seaborn 
Purpose: Python library for statistical data visualization.
Usage: to generate a pairplot for the Iris dataset
