# Stat Tracking System Documentation
System overview of [team stat tracking system](https://github.com/kchenTTP/team_stat_tracking.git).


---
## Data Pipeline Diagram & Overview
![data pipeline diagram](./images/stat-tracking-system-diagram.png)


### **Data Extraction**
- Download monthly system wide event data from online content management system (CMS)
  - Manually download csv files
  - *Future update: schedule monthly data scraping after internal CMS update stats for previous month (Prefect)* [^1]


### **Data Transformation Pipeline**
- *Future update: schedule monthly data transformation & database writing & back-up after monthly data has been scraped*
#### *Data Cleaning*
- Data scrubbing
- Fix incorrect datatype
- Error Handling
  - Fix CMS data exporting errors
  - Compare warehouse data to handle naming error
- Data imputation
- Handle edge cases

#### *Airtable Data Extraction*
- Scrape class information from internal Airtable database due to API limitations
- *Future update: store airtable data in warehouse + scheduled scraping to automate class name adjustments*

#### *Future update: String Matching & Genre Classification*
- Match class title strings from CMS data to Airtable data to ensure data integrity[^2]
- *Future update: add additional column that specifies the category/genre of each class and categorize CMS data to support more detailed analysis in the future* [^3]

#### *Data Transformation*
- Add columns for additional information missing from CMS data

#### *Data Loading*
- Save processed data and additional supporting data into SQL data warehouse


### **Data Warehouse**
- SQL database (star schema model) updated monthly whenever CMS gets all information from team


### **Data Analysis Pipeline**
#### *Data Transformation + Analysis*
- Aggregate, filter, analyze stats from SQL database
- plot charts for dashboard to support analysis

#### *Dashboard*
- Streamlit interactive dashboard
- *Future update: Authentication layer to limit access to team members*
- *Future update: Generate data reports*[^4]


---

## *Future Features*
[^1]: Due to internal system using multiple versions of CMS (Drupal), the API is unreliable. Web scraping is required to retrieve system data  
[^2]: String matching with fuzzy match, KNN, or other matching algorithm  
[^3]: Classify each class to their own genre with KNN, decision trees, or other multi-class classification algorithms to support more detailed analysis in the future  
[^4]: Generate Excel or pdf reports of data dashboard
