# Data-analyst-yashang

## Descriptive Analysis

*Project Description*  
Descriptive Analysis of Year-over-Year Trends in Average Fee Paid and Employee Count by City (2024–2025)

*Project Title*  
Understanding Average Fee Paid and Employee Count by City in Vancouver, Animal Services.

*Objective*  
The objective of this visualization is to perform a descriptive analysis of business license data using AWS Data Analytics Platform (DAP).  
By plotting the average fee paid and the average number of employees per city from 2024 to 2025, the dashboard aims to reveal temporal and regional trends that can assist city planners and business analysts in understanding fee structures and workforce distribution across municipalities.

*Dataset*  
This dataset includes business licence records from 2024 onwards with Animal Services.  
The data was uploaded to an AWS S3 bucket as the raw input for the pipeline.

## Methodology

## 1. Data Collection and Preparation

### Documentation Contribution
- Contributed to **data lake architecture and analysis documentation**
- Documentation covers:
  - Tagging strategy  
  - Storage class policies  
  - Mapping of business questions (e.g., sentiment-performance correlation)

![image alt](https://github.com/yashangs0510/Data-analyst-yashang/blob/d0fb288c859414d855a4de9c336580b20ed32965/Images/Screenshot%202025-06-22%20115240.png)


- ## Folder Structure in S3
- *Load the dataset using data analysis tools:* Secure Storage Setup (S3 Bucket) used
- Set up **nine categorized folders** for structured HR datasets

## S3 Bucket Configuration
- Created **S3 bucket**: `hr-raw-mahh`
- Hosted in **US East (N. Virginia)** region

![image alt](https://github.com/yashangs0510/Data-analyst-yashang/blob/c128efd10a7148e9ad777121aaa424e33b6dd19f/Screenshot%202025-06-22%20111848.png)

## Security Configuration
- Configured **security group** for instance access and data flow

![image alt](https://github.com/yashangs0510/Data-analyst-yashang/blob/6f8ad8aaa53b561dccddf0eca38febfb367d1d59/Images/Screenshot%202025-06-22%20114547.png)

- ## EC2 Instance Setup
- Launched EC2 instance: **HRVS-MAH**
- Attached a **30 GiB EBS** volume

![image alt](https://github.com/yashangs0510/Data-analyst-yashang/blob/6f8ad8aaa53b561dccddf0eca38febfb367d1d59/Images/Screenshot%202025-06-22%20114414.png)

## 2. Data Cleaning and Profiling

### Data Cleaning Design using AWS Glue DataBrew
- Analyzed raw HR data to identify transformation needs (e.g., missing values, format inconsistencies).
- Designed cleaning workflows using Glue DataBrew’s no-code interface.
- Mapped transformation steps to HR business questions (e.g., sentiment vs. performance).

###  Data Cleaning Implementation
- Created reusable Glue DataBrew projects and recipes for selected datasets.
- Applied transformations such as:
  - Dropping empty columns
  - Standardizing text formats
  - Deriving sentiment scores
- Previewed results before full job execution.

![image alt](https://github.com/yashangs0510/Data-analyst-yashang/blob/63c998c15989849acd8d33855df4248c2dca45e4/Images/Screenshot%202025-06-22%20120338.png)

### 5. Job Execution and Output Storage
- Executed jobs on demand — fully serverless (no provisioning required).
- Output stored in a designated S3 bucket (`hr-cleaned-mahh`) for downstream analytics.
- Validated results by cross-checking transformed datasets with initial requirements.

![image alt](https://github.com/yashangs0510/Data-analyst-yashang/blob/63c998c15989849acd8d33855df4248c2dca45e4/Images/Screenshot%202025-06-22%20120352.png)

### 2. S3 Cost Evaluation
- Monitored usage and cost through AWS Cost Explorer and S3 Storage Class Analysis.
- Compared costs across storage classes (Standard vs. Intelligent-Tiering vs. Glacier).
- Estimated monthly storage costs for projected data volumes.
- Documented findings and cost charts in the project report for optimization insights.

![image alt](https://github.com/yashangs0510/Data-analyst-yashang/blob/79faf01097b3a589997aa26d12e4da338f368b18/Images/Screenshot%202025-06-22%20120511.png)
