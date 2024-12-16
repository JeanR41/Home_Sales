# Spark SQL Data Analysis of Home Sales

## Overview
This project performs a series of data manipulations and queries using **Apache Spark** and **PySpark**. The goal is to analyze home sales data using SQL queries and Spark functionalities. The data is loaded from an AWS S3 bucket and is then processed to answer several analytical questions such as average home price based on bedroom count, year built, square footage, and view rating. Various optimization techniques like caching and partitioning are also applied to enhance the performance of queries.

## Setup Instructions

### Requirements
To run this project, the following Python packages need to be installed:

- **pyspark**: For Spark functionalities in Python.
- **findspark**: To initialize Spark on your local machine.

### Data
The home sales data from an AWS S3 bucket is loaded into a DataFrame.
The url for the date is https://2u-data-curriculum-team.s3.amazonaws.com/dataviz-classroom/v1.2/22-big-data/home_sales_revised.csv

### SQL Queries

#### Query 1: Average Price for a Four-Bedroom House Sold Per Year
This query calculates the average price of four-bedroom homes, grouped by the year of sale:
The highest average price for a four-bedroom house sold in a year was **$301,819.44** in 2021.

#### Query 2: Average Price of a Home for Each Year It Was Built (3 Bedrooms and 3 Bathrooms)
This query calculates the average price of homes with 3 bedrooms and 3 bathrooms, grouped by the year they were built:
The highest average price for homes built was the **2017** average of **$292,676.79**.

#### Query 3: Average Price for Homes Built with 3 Bedrooms, 3 Bathrooms, 2 Floors, and >= 2,000 Sq Ft
This query calculates the average price of homes that have 3 bedrooms, 3 bathrooms, two floors, and are at least 2,000 square feet, grouped by the year they were built:
The highest average price for homes that meet these criteria was from the year **2012**, with an average price **$307,539.97**.

#### Query 4: Average Price of Homes by View Rating with a Price >= $350,000
This query calculates the average price of homes per "view" rating, with an average price greater than or equal to $350,000:
Average prices across all view ratings were calculated, with the top **view rating of 100** for a home correlating to a price of **$1,026,669.50**.

#### Comparing Cached vs Non-Cached Query Performance
Caching the `home_sales` table reduced the runtime for Query 4 on view ratings and average home price from **1.318 seconds** (uncached) to **0.473 seconds** (cached).
=
#### Comparing Average Price by View Rating on Parquet Data
Query 4 was again repeated; this time it was executed on the partitioned data stored in **Parquet** format:
When querying the partitioned Parquet data, the query runtime was **1.089 seconds**.


### Runtime Comparison
The execution time for queries before and after caching, as well as for partitioned data, is measured to compare performance improvements.

- **Uncached Query Runtime**: The time it takes to execute a query without caching. Sample query (query 4) took **1.318 seconds**
- **Cached Query Runtime**: The time taken when the table is cached. Sample query (query 4) took **0.473 seconds**
- **Partitioned Data Query Runtime**: The time taken when partitioned data is queried. Sample query (query 4) took **1.089 seconds**

## Key Findings

- **Highest Average Price for Four-Bedroom Homes Sold in a Year**: The highest average price was **$301,819.44** in **2021**.
- **Highest Average Price for Homes Built with 3 Bedrooms and 3 Bathrooms**: The highest average price was **$292,676.79** for homes built in **2017**.
- **Highest Average Price for Homes with 3 Bedrooms, 3 Bathrooms, 2 Floors, and >= 2,000 Sq Ft**: The highest average price was **$307,539.97** for homes built in **2012**.
- **Highest Average Price by View Rating**: Homes with a **view rating of 100** had the highest average price of **$1,026,669.50**.
- **Performance Improvement with Caching**: Caching the `home_sales` table reduced the query runtime for **view ratings and average home price** from **1.318 seconds** (uncached) to **0.473 seconds** (cached).
- **Partitioned Data Performance**: Querying the partitioned **Parquet** data resulted in a runtime of **1.089 seconds** for view rating analysis, offering a moderate performance improvement over uncached data.