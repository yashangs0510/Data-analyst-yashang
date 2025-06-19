# Data-analyst-yashang
### Descriptive Analysis 
**Project Description**: Descriptive Analysis of Year-over-Year Trends in Average Fee Paid and Employee Count by City (2024–2025)
**Project Title**: Understanding Average Fee Paid and Employee Count by City in Vancouver, Animal Services.
**Objective**: The objective of this visualization is to perform a descriptive analysis of business license data using AWS Data Analytics Platform (DAP). By plotting the average fee paid and the average number of employees per city from 2024 to 2025, the dashboard aims to reveal temporal and regional trends that can assist city planners and business analysts in understanding fee structures and workforce distribution across municipalities.
**Dataset** : This dataset includes business licence records from 2024 onwards with Animal Services.The data was uploaded to an AWS S3 bucket as the raw input for the pipeline.
**Methodology**:
1-	Data Collection and Preparation: 
o	Load the dataset using data analysis tools: Secure Storage Setup (S3 Bucket) used
o	Performed data cleaning to address missing values, correct data types, and remove duplicates: AWS Glue DataBrew service used
2-	Descriptive Statistics:
my Business license data is collected and inserted into the Amazon S3 bucket 'cov-raw-mah'. Within the subdirectories, the data is stored by year, month, and week for retrieval in both CSV and JSON format
A dedicated security group `COV-VS-Mah` managed access rules, ensuring secure connectivity for compute instances during processing. IAM roles and access analyzers monitor data interactions. 
AWS Glue DataBrew was used to profile and clean the business license dataset. The job succeeded with 100% valid values and no missing data across 22 columns. A transformation recipe was applied and executed successfully, producing two clean outputs for analytics, ensuring high data quality and consistency for further processing.
