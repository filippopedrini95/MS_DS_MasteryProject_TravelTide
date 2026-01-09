# MS_DS_MasteryProject_TravelTide


# Project Overview
This project analyzes customer behavior on TravelTide, an AI-powered online travel platform, with the goal of supporting the design of a personalized rewards program aimed at improving customer retention.
Starting from raw session-level data (over 5 million records), the analysis focuses on bookings made from January 2023 onward. The data is cleaned, processed, and aggregated at the user level to extract meaningful behavioral insights. Through exploratory data analysis (EDA), feature engineering, and customer segmentation, users are grouped based on both their booking and travel behavior and their RFM profile (Recency, Frequency, Monetary value). By combining these two segmentation approaches, the project identifies distinct user profiles and proposes targeted perks aligned with each group’s behavior and engagement level. The final output is a structured user dataset that can be used by marketing teams to design more effective, data-driven retention strategies.


# Data source and installation instructions
This project was developed using Databricks. The notebooks included in this repository were downloaded directly from the Databricks environment, and all required libraries are listed at the beginning of each notebook.
During the analysis, intermediate datasets were often saved as Delta Lake tables to enable reuse across notebooks and later reloaded as pandas DataFrames.
The original database is not included in this repository due to its size; instead, the access link is provided in the TravelTideDB_link.txt file.


# Project Workflow
The analysis was developed in Databricks and organized into multiple notebooks, each covering a specific step of the data pipeline.
At the beginning of each notebook, a dataset is loaded (stored in this repository as a CSV file), and in several cases a processed version of the data is saved for use in the next steps.

**Step 0 – Data Retrieval and Initial Filtering**\
**Notebook:** 0 - TravelTide Data Retrieval.ipynb\
**Input:** TraveTideDB_link.txt\
This notebook connects to the original TravelTide database using the link stored in the .txt file.
Since the raw database contains over 5 million records, sessions are filtered to keep only those occurring after 01/01/2023.
Relevant tables are joined together to produce a lighter and more manageable dataset.\
**Output:** sessions_filtered_RawData.csv (≈49k records)

**Step 1 – Session-Level Preprocessing**\
**Notebook:** 1 - TravelTide SessionDataset Preprocessing.ipynb\
**Input:** sessions_filtered_RawData.csv\
This step focuses on data cleaning, preparation, and feature engineering at the session level.
Inconsistencies are fixed and new features are created to make the dataset ready for exploratory data analysis (EDA).\
**Output:** sessions_preprocessed.csv

**Step 2 – User Table Creation**\
**Notebook:** 2 - TravelTide UserTab Creation.ipynb\
**Input:** sessions_preprocessed.csv\
Sessions are aggregated at the user level to create a dedicated user dataset.
Each row represents a single user, summarizing their booking activity on the platform.\
**Output:** users_RawTab.csv

**Step 3 – Session-Level Exploratory Data Analysis**\
**Notebook:** 3 - TravelTide SessionEDA.ipynb\
**Input:** sessions_preprocessed.csv\
This notebook performs EDA on the session-level dataset, focusing on booking behavior, trip characteristics, cancellations, and timing patterns.
No data is saved, as this step is purely exploratory.\
**Output:** None (EDA only)

**Step 4 – RFM Segmentation**\
**Notebook:** 4 - TravelTide Users RFM segmentation.ipynb\
**Input:** users_RawTab.csv\
Users are segmented using the RFM framework (Recency, Frequency, Monetary value).
This segmentation is later used to identify users with different levels of engagement and value.\
**Note:** User-level EDA was not performed strictly before this step. Instead, the user EDA notebook was used iteratively throughout the project and is listed at the end of the workflow.\
**Output:** user_RFM.csv

**Step 5 – Unsupervised ML Segmentation (Exploratory)**\
**Notebook:** 5 - TravelTide Users ML Segmentation.ipynb\
**Input:** users_RawTab.csv\
Several unsupervised learning algorithms are tested to explore alternative segmentation approaches.
Due to low silhouette scores and limited interpretability, this approach is abandoned in favor of rule-based segmentations.\
**Output:** None

**Step 6 – User-Level EDA and Final Segmentation**\
**Notebook:** 6 - TravelTide UsersEDA.ipynb\
**Input:** users_RawTab.csv, user_RFM.csv\
This notebook performs multiple tasks:
- User-level exploratory data analysis
- Additional feature engineering to support analysis and visualization
- Creation of presentation-ready charts
- Execution of a second segmentation based on Booking and Travel Behaviour, referred to throughout the notebook as manual_segmentation
- Renaming of this segmentation column to BTB_segmentation

The final dataset combines:
- User-level features
- RFM segmentation
- Booking & Travel Behaviour segmentation

**Output:** users_FinalTab.csv


# Contact information
filippopedrini95@gmail.com


