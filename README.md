## 1. Background and Overview

### Business Context
This project is based on a synthetically generated dataset that simulates transactional and customer behavior data from a U.S.-based e-commerce business specializing in toys. The company operates across 15 major American cities: Austin, Charlotte, Chicago, Columbus, Dallas, Fort Worth, Houston, Jacksonville, Los Angeles, New York, Philadelphia, Phoenix, San Antonio, San Diego, and San Jose.

The dataset contains approximately 200,000 records collected over a one-year period, capturing key variables related to customer demographics, purchasing behavior, product interactions, and satisfaction levels. As a synthetic dataset, it was designed to resemble realistic patterns and common data quality issues typically encountered in real-world business environments.

### Objectives
- To perform customer segmentation across demographic variables (age group, gender, membership type) to determine which segments yield the highest profit contribution.
- To analyze geographic profit distribution across cities, identifying high-value markets and purchase behavior patterns by location.
- To assess product-level profitability by cross-referencing sales volume and profit margin to identify top-performing SKUs.

The ultimate goal is to translate these findings into data-driven recommendations that can inform marketing segmentation, retention strategies, and operational improvements for a retail business of this nature.

### Technical Approach
For readers interested in the technical implementation, the project follows a structured analytics workflow:

- **Data Cleaning & Exploration:** Performed using Python to inspect data quality, handle inconsistencies, and prepare the dataset for analysis.
[Python script available here →](./YOUR-PYTHON-FOLDER/)

- **Business Question Analysis:** Core business questions are addressed using SQL, focusing on aggregations, segmentation, and trend analysis.
[SQL queries available here →](./YOUR-SQL-FOLDER/)

## 2. Structure & Initial Data

### Dataset Overview
This dataset contains 200,000 records and 12 columns. It includes customer profile information, purchase details, membership data, and satisfaction-related variables for toy purchases.

### Column Structure & Data Types

| Column | Data Type | Description |
|--------|-----------|-------------|
| Customer ID | Integer (int64) | Unique identifier for each customer. |
| Gender | Categorical (object) | Customer's gender. |
| Age | Integer (int64) | Customer's age in years. |
| City | Categorical (object) | City where the customer is located. |
| Membership Type | Categorical (object) | Customer's membership level. |
| Total Spend | Numeric (float64) | Total amount spent by the customer. |
| Cost | Numeric (float64) | Cost associated with the purchase. |
| Items Purchased | Categorical (object) | Name of the product purchased. |
| Average Rating | Numeric (float64) | Average rating given to the product or experience. |
| Discount Applied | Boolean-like categorical (object) | Indicates whether a discount was applied. |
| Days Since Last Purchase | Integer (int64) | Number of days since the customer's previous purchase. |
| Satisfaction Level | Categorical (object) | Overall satisfaction reported for the customer or purchase. |

### Column Groups

**Customer Information:**

| Column |
|--------|
| Customer ID |
| Gender |
| Age |
| City |

**Membership Information:**

| Column |
|--------|
| Membership Type |

**Purchase & Transaction Details:**

| Column |
|--------|
| Total Spend |
| Cost |
| Items Purchased |
| Discount Applied |

**Experience & Loyalty Indicators:**

| Column |
|--------|
| Average Rating |
| Days Since Last Purchase |
| Satisfaction Level |

---
Before analysis, the following validation steps were performed
### Initial Data Checks

- **Missing Values:** Empty and null fields were detected across multiple columns. All missing values were replaced with the label `Unknown` to preserve row integrity and avoid data loss during aggregation queries.

- **Typographical Errors:** Inconsistent string formatting was identified in categorical columns (e.g., membership types, city names, satisfaction levels). These were standardized to ensure correct grouping and filtering behavior in both SQL and Power BI.

- **Invalid Age Values:** Outlier values in the `Age` column were found, including negative numbers, zeros, and unrealistically low ages inconsistent with the customer profile. These were replaced with the column's mean age to maintain statistical representativeness without removing records.

- **Special Characters:** Unexpected characters such as commas (`,`) and hash symbols (`#`) were found embedded in numeric and categorical fields, which could cause parsing errors and incorrect data type inference. These were removed during the cleaning process.

- **Profit Column Engineering:** A new column `Profit` was derived as:

$$Profit = Total\ Spend - Cost$$
