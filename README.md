# Stat Tracking System Documentation
High-level overview of [team stat tracking system](https://github.com/kchenTTP/team_stat_tracking.git).


---
## Data Pipeline Diagram & Overview
![data pipeline diagram](./images/stat-tracking-system-diagram.png)


### **Data Extraction**
- Download monthly system wide event data from content management system (CSM)
  - Manual download csv files
  - Or, periodically scrape csv files


### **Data Transformation Pipeline**
#### *Data Cleaning (Pandas)*
- Drop unused columns
- Fix incorrect datatypes
- Drop duplicated rows
- Handle CMS data exporting errors
- Data imputation

#### *Airtable Data Extraction (Airtable API)*
- Extract class information from Airtable database

#### *String Matching & Genre Classification*
- Match class title strings from CMS data to Airtable data[^1]
- Classify every class to different genres[^2]

#### *Data Transformation*
- Add columns for additional information that is missing from CMS data

#### *Data Loading (BigQuery Python API)*
- Load processed data and additional supporting data into BigQuery using star schema model


### **Data Warehouse**
- BigQuery

### **Data Analysis Pipeline**
#### *Data Transformation*
- Connect to BigQuery
- Aggregate data
- Plot charts

#### **Dashboard**
- Streamlit interactive dashboard
- Authentication layer to limit access to team members
- Generate data reports[^3]


---

## *Future Features*
[^1]: String matching with fuzzy match or KNN.
[^2]: Classify each class to their own genre with KNN & clustering techniques
[^3]: Generate Excel or pdf reports for downloading
