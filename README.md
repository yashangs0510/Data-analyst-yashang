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

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/2.png)
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/ec2.png)
### 2. 🧹 Data Profiling and Cleaning (AWS Glue DataBrew)

- **Profiling with DataBrew**:
  - Dataset was profiled using AWS Glue DataBrew to assess data quality.
  - Results showed 100% valid values across 22 columns with no missing data — confirming readiness for transformation.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/3.png)

- **Cleaning and Transformation**:
  - Designed a DataBrew recipe for column normalization, data type casting, trimming text, and renaming fields for clarity.
  - Executed the recipe and exported clean datasets to a new S3 path for downstream analytics.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/4.png)

- **Output Verification**:
  - Cleaned datasets were validated against original business objectives, ensuring consistency, completeness, and format compliance.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/5.png)

### 3. ⚙️ ETL Implementation (AWS Glue Jobs)

- **ETL Job Design**:
  - Created two jobs using AWS Glue Studio's visual interface:
    - `COV-business-licence`: Initial cleansing of raw data.
    - `cov-enriching-mah`: Transformation and enrichment for analysis (e.g., tagging business status).
  
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/6.png)

- **Performance and Resources**:
  - Used 10 DPUs per job to ensure efficient processing.
  - Job runtime was optimized to under 2 minutes, with logs tracked via CloudWatch for visibility.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/7.png)

- **Data Cataloging**:
  - The outputs were registered in the AWS Glue Data Catalog (`cov-data-catalog-mah`) to enforce schema consistency.
  - This enabled downstream access via Athena and BI tools.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/Screenshot%202025-06-22%20131806.png)

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

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/8.png)

### 5. 📉 Data Evaluation and Monitoring

- **Cost Evaluation**:
  - Estimated yearly cost of $31.47 USD for the entire platform:
    - **Amazon S3**: $6.03/year for storage and access
    - **Glue DataBrew**: $25.44/year for data transformation
  
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/9.png)
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/10.png)
![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/11.png)


- **Monitoring with CloudWatch**:
  - Set up a billing alarm to monitor usage, triggering alerts if costs exceed $50 in any 6-hour window.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/12.png)

### 6. 📁 Documentation and Deliverables

- **Version Control and Traceability**:
  - GitHub is used to track all pipeline revisions, job logic, and documentation changes.
  - Data lifecycle management and tagging strategies are documented to support auditability and compliance.

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/15.png)




## ✅ Outcome

This cloud-native platform enables the City of Vancouver to generate near real-time insights into animal business licensing trends. With low-cost ingestion, automated ETL, and serverless querying, the system supports data-driven urban governance and compliance monitoring — laying the foundation for scalable municipal analytics.





# 📘 AWS Portfolio Assignment – Yashang Singh


### ✅ Module 1: AWS Deployment and Service Models

- **Summary:** Explored the evolution from traditional IT infrastructure to cloud computing and understood cloud service and deployment models.

- **Case Study #1: Traditional vs Cloud Computing**
  | Traditional Computing | Cloud Computing |
  |------------------------|------------------|
  | On-premise servers | Internet-based resources |
  | High CapEx (upfront costs) | Low CapEx, pay-as-you-go |
  | Long provisioning time | Quick provisioning |

  **Explanation:** Traditional IT requires large investments in hardware and maintenance. Cloud computing enables cost efficiency and speed by offering scalable, on-demand infrastructure.

- **Case Study #2: Cloud Deployment Models**
  - **Public Cloud:** Fully hosted by cloud providers, accessible via the internet
  - **Private Cloud:** Internal or vendor-hosted for exclusive use
  - **Hybrid Cloud:** Combines public and private for flexibility
  - **Community Cloud:** Shared across organizations with common needs

  **Explanation:** The student chose a **Hybrid Cloud** model, balancing security for sensitive tasks (private) and scalability for public-facing apps (public).

- **Case Study #3: Cloud Service Models**
  | Model | Control | Responsibility |
  |-------|---------|----------------|
  | IaaS  | High    | User manages OS, runtime, app |
  | PaaS  | Medium  | User manages app & data |
  | SaaS  | Low     | Vendor manages everything |

  **Explanation:** EC2 (IaaS) was chosen for fine-grained control, and Elastic Beanstalk (PaaS) for simplified deployment. This shows thoughtful application of service models.

- **Module 1 Knowledge Check:**
  ✅ **Score: 100%** 

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/m1.png)

### 💰 Module 2: AWS Cost Analysis

- **Summary:** Evaluated EC2 and S3 pricing across instance types and regions.
- **Result:**
  - **Spot Instances** for cost savings on flexible workloads
  - **Reserved Instances** for steady usage
  - Region-based savings (e.g., N. Virginia over Frankfurt)
- **Explanation:** Strategic pricing selection ensures efficiency in both compute and storage costs.

![image]()

### 🌍 Module 3: AWS Global Infrastructure

- **Summary:** Designed a high-availability global architecture.
- **Result:**
  - **S3 cross-region replication**
  - **CloudFront** for global content delivery
  - **Route 53** with latency-based routing
- **Explanation:** Leveraged AWS’s global infrastructure to minimize downtime and latency.

![image]()

### 🔐 Module 4: AWS IAM

- **Summary:** Configured IAM roles and policies for HR and Finance departments.
- **Result:**
  - Enforced **Least Privilege Access**
  - Enabled **MFA**
  - Used **Roles** for cross-account permissions
- **Explanation:** Secure and controlled access prevents misuse and improves account hygiene.

![image]()

### 🛡️ Module 5: AWS VPC

- **Summary:** Designed a secure 3-tier VPC architecture.
- **Result:**
  - **Public subnet:** Load Balancer, Bastion Host
  - **Private subnet:** App and DB layers
  - **NAT Gateway** for controlled internet access
- **Explanation:** Followed AWS security best practices by isolating layers and controlling access.

![image]()

### ⚡ Module 6: AWS Lambda

- **Summary:** Built a serverless image processing workflow triggered by S3.
- **Result:**
  - Auto-thumbnail creation
  - Output stored in a separate bucket
  - Near-zero cost with <1s execution
- **Explanation:** Demonstrated event-driven, scalable architecture using serverless computing.

![image]()

### 💾 Module 7: AWS EBS

- **Summary:** Tested EBS volume types for performance and backup.
- **Result:**
  - **gp3** for general workloads
  - **io1** for high-IOPS DBs
  - **Snapshots** for backups
- **Explanation:** Matched storage type to workload; snapshots enabled disaster recovery planning.

![image]()

