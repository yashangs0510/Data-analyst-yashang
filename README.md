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

### 1. 🔁 Data Ingestion Setup

- **Amazon S3 Bucket Creation**: 
  - Initialized a versioned S3 bucket named `cov-raw-mah`.
  - Data was organized using a time-based folder hierarchy (`year/quarter/month/week`) to support granular access and retention strategies.
  
- **Data Upload and Formats**:
  - Raw business license data uploaded in both `.csv` and `.json` formats to accommodate varying ingestion and analysis needs.
  - Daily write frequency and monthly read setup enabled automated refresh and stable performance.

![S3 Bucket Screenshot](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/1.png)

- **Security & Testing**:
  - Created a dedicated security group `COV-VS-Mah` for controlled access.
  - IAM roles and access analyzers were applied to manage permission boundaries.
  - An EC2 instance (`COVVS`) was briefly used to test and validate ingestion scripts before transitioning to a fully serverless architecture.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/d1cffa871c4bfa5d9dd03499dfb751435b02c564/images/2.png)
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/9d7925d02ff80a429046a14eeb26bdaea1492d7b/images/ec2.png)
### 2. 🧹 Data Profiling and Cleaning (AWS Glue DataBrew)

- **Profiling with DataBrew**:
  - Dataset was profiled using AWS Glue DataBrew to assess data quality.
  - Results showed 100% valid values across 22 columns with no missing data — confirming readiness for transformation.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/d1cffa871c4bfa5d9dd03499dfb751435b02c564/images/3.png)

- **Cleaning and Transformation**:
  - Designed a DataBrew recipe for column normalization, data type casting, trimming text, and renaming fields for clarity.
  - Executed the recipe and exported clean datasets to a new S3 path for downstream analytics.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/d1cffa871c4bfa5d9dd03499dfb751435b02c564/images/4.png)

- **Output Verification**:
  - Cleaned datasets were validated against original business objectives, ensuring consistency, completeness, and format compliance.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/d1cffa871c4bfa5d9dd03499dfb751435b02c564/images/5.png)

### 3. ⚙️ ETL Implementation (AWS Glue Jobs)

- **ETL Job Design**:
  - Created two jobs using AWS Glue Studio's visual interface:
    - `COV-business-licence`: Initial cleansing of raw data.
    - `cov-enriching-mah`: Transformation and enrichment for analysis (e.g., tagging business status).
  
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/9d7925d02ff80a429046a14eeb26bdaea1492d7b/images/6.png)

- **Performance and Resources**:
  - Used 10 DPUs per job to ensure efficient processing.
  - Job runtime was optimized to under 2 minutes, with logs tracked via CloudWatch for visibility.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/9d7925d02ff80a429046a14eeb26bdaea1492d7b/images/7.png)

- **Data Cataloging**:
  - The outputs were registered in the AWS Glue Data Catalog (`cov-data-catalog-mah`) to enforce schema consistency.
  - This enabled downstream access via Athena and BI tools.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/252c4a55023b6c860fe7417a5201d800f5c6dba8/images/Screenshot%202025-06-22%20131806.png)

### 4. 🔍 Querying and Reporting (AWS Athena)

- **Athena Integration**:
  - Created external tables in Athena by querying the Data Catalog.
  - Wrote serverless SQL queries to extract fields like `license_number`, `trade_name`, and `status`.

- **Analytical Insights**:
  - Retrieved 516 records representing historical trends, cancellations, and renewals.
  - These queries informed city service decisions regarding business activity hotspots and seasonal fluctuations.

- **Performance and Cost Control**:
  - Leveraged Athena’s **pay-per-query model** to reduce overhead.
  - Queries were partitioned and optimized for fast execution and minimal cost.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/252c4a55023b6c860fe7417a5201d800f5c6dba8/images/8.png)

### 5. 📉 Data Evaluation and Monitoring

- **Cost Evaluation**:
  - Estimated yearly cost of $31.47 USD for the entire platform:
    - **Amazon S3**: $6.03/year for storage and access
    - **Glue DataBrew**: $25.44/year for data transformation
  
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/252c4a55023b6c860fe7417a5201d800f5c6dba8/images/9.png)
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/252c4a55023b6c860fe7417a5201d800f5c6dba8/images/10.png)
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/252c4a55023b6c860fe7417a5201d800f5c6dba8/images/11.png)


- **Monitoring with CloudWatch**:
  - Set up a billing alarm to monitor usage, triggering alerts if costs exceed $50 in any 6-hour window.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/blob/c14d05d4ac6ab59fc96f83059b95ca91ee6e64f5/images/12.png)

### 6. 📁 Documentation and Deliverables

- **Visual Documentation**:
  - Diagrams of the data lake architecture, job flowcharts, and DataBrew screenshots are stored in the `/docs` folder.
  - Markdown files include transformation logic, SQL queries, cost breakdowns, and architecture justifications.

- **Version Control and Traceability**:
  - GitHub is used to track all pipeline revisions, job logic, and documentation changes.
  - Data lifecycle management and tagging strategies are documented to support auditability and compliance.

---

## ✅ Outcome

This cloud-native platform enables the City of Vancouver to generate near real-time insights into animal business licensing trends. With low-cost ingestion, automated ETL, and serverless querying, the system supports data-driven urban governance and compliance monitoring — laying the foundation for scalable municipal analytics.
