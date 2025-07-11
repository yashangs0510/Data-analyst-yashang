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

#### 🧪 Case Study #1: Traditional vs Cloud Computing

| Criteria        | Traditional Computing           | Cloud Computing                 |
|----------------|----------------------------------|----------------------------------|
| Infrastructure | On-premise servers               | Internet-based resources         |
| Cost Structure | High CapEx (upfront costs)       | Low CapEx, pay-as-you-go         |
| Provisioning   | Long provisioning time           | Quick provisioning               |

**Explanation:**  
Traditional IT requires large investments in hardware and maintenance. Cloud computing enables cost efficiency and speed by offering scalable, on-demand infrastructure.


- **Case Study #2: Cloud Deployment Models**
  - **Public Cloud:** Fully hosted by cloud providers, accessible via the internet
  - **Private Cloud:** Internal or vendor-hosted for exclusive use
  - **Hybrid Cloud:** Combines public and private for flexibility
  - **Community Cloud:** Shared across organizations with common needs

  **Explanation:** The student chose a **Hybrid Cloud** model, balancing security for sensitive tasks (private) and scalability for public-facing apps (public).

#### 🧪 Case Study #3: Cloud Service Models

| Model | Control Level | Responsibility                         |
|-------|---------------|------------------------------------------|
| IaaS  | High          | User manages OS, runtime, application   |
| PaaS  | Medium        | User manages app and data               |
| SaaS  | Low           | Vendor manages everything               |

**Explanation:**  
EC2 (IaaS) was chosen for fine-grained control, and Elastic Beanstalk (PaaS) for simplified deployment. This shows thoughtful application of service models.


- **Module 1 Knowledge Check:**
  ✅ **Score: 100%** 

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/m1.png)

### 💰 Module 2: AWS Cost Analysis

- **Summary:** Focused on AWS pricing fundamentals, total cost of ownership (TCO), support plans, and usage of AWS Pricing Calculator.

---

#### 🧪 Case Study #4: Total Cost of Ownership – Delaware North

**Result:**  
Using AWS reduced upfront infrastructure investments, minimized operational overhead, and provided measurable cost savings in terms of:
- Reduced physical server maintenance
- Lower electricity and hardware costs
- Decreased need for in-house IT management

**Explanation:**  
AWS shifts costs from capital expenditure (CapEx) to operational expenditure (OpEx), allowing businesses to pay for what they use. Delaware North benefited by reducing overprovisioning and scaling based on actual demand.

---

#### 🧪 Case Study #5: AWS Pricing Calculator

**Result:**  
Used AWS Pricing Calculator to estimate monthly costs for three scenarios:
- **New Workload**
- **Lift-and-Shift Migration**
- **Optimized Architecture**

Each pricing estimate showed:
- Clear hourly/monthly breakdowns
- Regional cost variations
- Service-specific billing

**Explanation:**  
The calculator provided cost transparency. It helped plan for budgeting and cost optimization by comparing usage patterns, regions, and reserved vs on-demand pricing options.

---

#### 🧪 Case Study #6: Support Plan

**Result:**  
For the HR department, the **AWS Business Support Plan** was selected.

**Justification:**  
This plan offered 24x7 access to cloud engineers, faster response times, and architectural guidance – essential for business-critical workloads and ensuring compliance in HR systems.

---

#### ✅ Module 2 Knowledge Check

- **Score:** 100%

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/m2.drawio.png)

### 🌍 Module 3: AWS Global Infrastructure

- **Summary:** Focused on understanding AWS Regions, Availability Zones, Edge Locations, and how AWS designs global infrastructure for resilience, low latency, and compliance.

---

#### 🧪 Case Study #7: AWS Global Infrastructure

**Result:**
- Designed an architecture using **multiple regions** (e.g., N. Virginia and Tokyo) for redundancy.
- Incorporated:
  - **S3 Cross-Region Replication** to ensure data backup across continents
  - **Route 53** for latency-based DNS routing
  - **CloudFront** to distribute content globally via **Edge Locations**
- Compared three infrastructure elements:
- 
| Infrastructure Element | Dataset Location                | Dataset Access                   | Dataset Privacy            |
|------------------------|----------------------------------|-----------------------------------|-----------------------------|
| Regional Edge Cache    | Temporarily cached closer to users | Accelerated data delivery         | Minimal data stored         |
| Edge Location          | Cached for local delivery         | Optimized access via low-latency  | Encrypted storage           |
| Region                 | Fully hosted AWS region           | All services (storage, compute)   | Compliant and secure        |

**Explanation:**  
By leveraging AWS’s global network, the architecture ensures low-latency content delivery, redundancy, and regulatory compliance. Users get faster access regardless of geographic location, and critical datasets remain secure and highly available.


#### ✅ Module 3 Knowledge Check

- **Score:** 100%

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/m3.drawio.png)

### 🔐 Module 4: AWS IAM
 
- **Summary:** Focused on access control, shared responsibility model, and hands-on IAM configuration using AWS best practices.

---

#### 🧪 Case Study #8: Who Is Responsible?

| Layer       | UCW Responsibility                                  | AWS Responsibility                                            |
|-------------|-----------------------------------------------------|---------------------------------------------------------------|
| **EC2**     | Installing, configuring, and managing instances      | Maintaining physical infrastructure and virtualization layer  |
| **Platform**| Managing runtime, middleware, and OS updates        | N/A                                                           |
| **Software**| Developing and deploying secure code                | N/A                                                           |
| **Dataset** | Ensuring secure use and classification of data      | Secure storage and compliance of underlying infrastructure    |

**Explanation:**  
The case highlights the **Shared Responsibility Model**. While AWS secures the cloud itself (hardware, infrastructure), the user (UCW in this case) is responsible for **securing what is in the cloud**, including access policies, patching, and data classification.

---

#### 🧪 Case Study #9: IAM Practice – Lab 1

**Result:**
- Created IAM users, groups, and roles
- Attached custom policies for **least privilege access**
- Enabled **MFA (Multi-Factor Authentication)**
- Verified policies through **permission simulation**

**Explanation:**  
This hands-on practice demonstrated secure identity management:
- **Groups** simplified permission management across users
- **Policies** enforced restricted access
- **MFA** strengthened security posture for privileged accounts

---

#### ✅ Module 4 Knowledge Check

- **Score:** 100%

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/m4.drawio.png)

### 🛡️ Module 5: AWS VPC

- **Summary:** This module focused on networking basics, custom VPC creation, subnetting, routing, and securing cloud resources with firewalls and route tables.

---

#### 🧪 Case Study #10: Build Your VPC (Lab 2)

**Result:**
- Created a **custom VPC** with:
  - One public subnet
  - One private subnet
  - Associated route tables and internet gateway
- Verified connectivity and subnet association via the VPC dashboard.

**Explanation:**  
This lab demonstrated foundational networking setup in AWS. By separating public and private subnets, it enforces security boundaries:
- **Public subnet** for internet-facing components (e.g., load balancers, bastion hosts)
- **Private subnet** for internal application and database layers  
Security groups and route tables were correctly applied to control traffic flow between components.

---

#### ✅ Module 5 Knowledge Check

- **Score:** 80%

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/m5.drawio.png)

### ⚡ Module 6: AWS Lambda

- **Summary:** Introduced to serverless computing concepts, AWS Lambda architecture, triggers, permissions, and cost-effectiveness in event-driven design.

---

#### 🧪 Case Study #11: Create an AWS Lambda Function

**Result:**
- Successfully created and deployed a Lambda function named `myLambdaAPI`.
- The function was triggered via test events and executed properly without the need for server provisioning.
- Configuration included runtime selection, permissions, and code inline editor.

**Explanation:**  
This hands-on activity showcased how **AWS Lambda** enables developers to run code in response to events (e.g., file uploads, API calls) **without managing infrastructure**. Key advantages observed:
- **Automatic scaling**
- **Sub-second billing**
- **Tight integration** with other AWS services (e.g., CloudWatch, API Gateway)

The Lambda function performed simple logic execution and validated how serverless architecture removes the burden of provisioning and scaling.

---

#### ✅ Module 6 Knowledge Check

- **Score:** 90%

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/m6.drawio.png)

### 💾 Module 7: AWS EBS

-- **Summary:** Introduced to serverless computing concepts, AWS Lambda architecture, triggers, permissions, and cost-effectiveness in event-driven design.

---

#### 🧪 Case Study #11: Create an AWS Lambda Function

**Result:**
- Successfully created and deployed a Lambda function named `myLambdaAPI`.
- The function was triggered via test events and executed properly without the need for server provisioning.
- Configuration included runtime selection, permissions, and code inline editor.

**Explanation:**  
This hands-on activity showcased how **AWS Lambda** enables developers to run code in response to events (e.g., file uploads, API calls) **without managing infrastructure**. Key advantages observed:
- **Automatic scaling**
- **Sub-second billing**
- **Tight integration** with other AWS services (e.g., CloudWatch, API Gateway)

The Lambda function performed simple logic execution and validated how serverless architecture removes the burden of provisioning and scaling.

---

#### ✅ Module 7 Knowledge Check

- **Score:** 90%

![image](https://raw.githubusercontent.com/yashangs0510/Data-analyst-yashang/main/images/m7.drawio.png)

