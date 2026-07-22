---
title: "Project Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AWS Observability & Security Dashboard
## A Hybrid Security Analytics Solution: MERN Stack Web App and AWS Data Pipeline

### 1. Executive Summary
The AWS Observability & Security Dashboard is a centralized Security Operations Center (SOC) designed using a Hybrid Architecture. The application leverages the power of the **MERN Stack (MongoDB, Express, React, Node.js)** to build the user interface and manage application data (Users, Roles, Alert Statuses). Simultaneously, the system connects directly to an **AWS Serverless Data Pipeline** (Kinesis, S3, Athena, GuardDuty) via the AWS SDK to collect and analyze massive log data in real-time. By combining these, the project delivers a smooth software experience while harnessing the Big Data capabilities of the cloud.

### 2. Problem Statement
*Current Problems*
In large-scale Cloud environments, log data (VPC Flow Logs, CloudTrail) is enormous. Manually analyzing this to find bandwidth-consuming IPs or detect network intrusions is impossible. Traditional tools face two hurdles:
1. Expensive SQL infrastructure costs when processing Big Data.
2. Lack of a flexible, customizable UI tailored to the needs of different departments (Admin, SecOps).

*Proposed Solution*
The project adopts a decoupled approach:
- **Web Component (Frontend + Node.js Backend + MongoDB)**: Handles the UI, Authentication (JWT), Role-Based Access Control (RBAC), and stores the status of incident alerts. MongoDB enables lightning-fast and highly customizable application data retrieval.
- **AWS Component (Data Pipeline)**: Handles the "heavy lifting" of Log collection and analysis. Kinesis Firehose streams logs to S3. Amazon Athena performs SQL queries on S3. Node.js calls Athena's API to fetch results (e.g., Top accessed IPs) and returns them to React for rendering.

*Benefits and ROI*
The Hybrid architecture optimizes costs to the maximum. MongoDB stores lightweight application data completely for free, while AWS charges only for data scanned (Pay-as-you-go). This combination showcases the comprehensive programming capabilities of a Software Engineer: capable of building Fullstack software while integrating and processing big data on AWS.

### 3. Solution Architecture
The project is a perfect intersection of Software Engineering and Cloud Architecture.

![AWS Data Pipeline Architecture](/images/2-Proposal/sodo1.png)

*AWS Data Flow (Data Engine)*
- **Amazon S3**: Stores Log data (Data Lake).
- **Amazon Kinesis Firehose**: Real-time log data streaming.
- **AWS Lambda**: Processes, cleanses, and transforms data before S3.
- **Amazon Athena**: Serverless Big Data SQL querying on S3.
- **Amazon GuardDuty**: Detects and identifies malicious IPs.
- **Amazon QuickSight**: BI Dashboard design embedded into React.

*Web Application (Web App)*
- **Frontend (ReactJS + TailwindCSS)**: Glassmorphism UI, Recharts (Charts), and react-simple-maps (Threat Map).
- **Backend (Node.js)**: API Gateway connecting to MongoDB (User Auth) and calling **AWS SDK** (fetching Athena/GuardDuty data).
- **Database (MongoDB)**: Manages User information, RBAC Roles, JWT Tokens, and Incident Ticket statuses.

### 4. Technical Implementation
*Implementation Phases*
1. **Web Setup**: Initialize React, Node.js, and MongoDB. Build Authentication (JWT) and RBAC.
2. **AWS Pipeline Setup**: Enable VPC Flow Logs/CloudTrail, configure Kinesis Firehose to stream to S3 via a Lambda Processor.
3. **Backend - AWS Integration**: Program Node.js using the AWS SDK to connect to Athena, retrieving the Top IP list and GuardDuty Findings.
4. **UI Development**: Draw Recharts graphs, display the World Map scanning radar at malicious IPs. Embed QuickSight.
5. **Completion**: End-to-End testing of the entire flow from MongoDB to AWS S3. Write documentation.

### 5. Roadmap & Milestones (12 Weeks)
- *Month 1 (Weeks 1-4)*: Design the Hybrid architecture, initialize the MERN Stack project, design the DB Schema, and complete JWT Login and RBAC.
- *Month 2 (Weeks 5-8)*: Build the AWS Data Pipeline (Kinesis -> Lambda -> S3). Node.js calls the AWS SDK to query Athena and populates the Network Traffic table on the Web.
- *Month 3 (Weeks 9-12)*: Integrate GuardDuty onto the Threat Map. Use MongoDB to create an Alert Management feature (changing incident statuses). Embed QuickSight. Final report.

### 6. Budget Estimation

The project is fully deployed within the **$200 AWS Free Tier Credit** provided by the internship program. To optimize costs, the EC2 Instance is strictly **turned on only when in use** and **turned off when idle**. Below is the actual cost calculation table:

| Service | Estimated Cost | Notes |
| :--- | :--- | :--- |
| **Amazon EC2 (t3.micro)** | ~$8.00 | On/off on demand (~770 actual hours × $0.0104/hour). First 750 hours/month are free (Free Tier), excess is charged. |
| **Amazon S3 (Data Lake)** | ~$2.50 | Storage for 50GB log data ($0.023/GB/month) + PUT/GET requests ($0.50) |
| **Amazon Kinesis Firehose** | ~$5.00 | Processing ~100GB data ingestion ($0.029/GB after the first 500MB free) |
| **AWS Lambda (my-log-filter)** | ~$0.50 | ~500,000 invocations × $0.20/1M requests. First 1M requests per month are free. |
| **Amazon Athena** | ~$1.50 | ~300 queries × ~1MB data scanned per query ($5/TB). Total ~300MB scanned. |
| **Amazon QuickSight** | ~$24.00 | 1 Author license ($24/month). Subscribed only in the final month for demo Dashboard creation. |
| **Amazon GuardDuty** | ~$8.00 | Analyzing VPC Flow Logs (~$1.15/GB after the first 500MB free) + CloudTrail Events. |
| **AWS CloudTrail** | ~$2.00 | 1 free Trail. Additional costs arise from S3 storage for trail logs. |
| **VPC Flow Logs** | ~$3.00 | Pushing logs to CloudWatch Logs ($0.50/GB ingested) + S3 storage. Estimated ~6GB logs over 12 weeks. |
| **MongoDB Atlas (M0 Free Tier)**| $0.00 | Using forever-free M0 cluster (512MB storage, sufficient for User, Alert, and TrafficLog data). |
| **Web App Hosting (on EC2)** | $0.00 | Web App is deployed directly on the EC2 Instance above, incurring no separate hosting costs. |
| **TOTAL** | **~$54.50** | Remaining **~$145.50** from the $200 Credit |
### 7. Risk Assessment
*Risk Matrix*
- AWS Credentials leak from the Node.js application (Impact: Very High, Probability: Medium).
- Web UI lagging when simultaneously rendering Recharts and react-simple-maps (Impact: Medium, Probability: Medium).

*Mitigation Strategies*
- Use IAM Roles instead of hardcoded Access Keys. Place all configuration in a `.env` file and push to `.gitignore`.
- Use `useMemo` and `useCallback` in React Frontend to prevent unnecessary map re-renders.

### 8. Expected Outcomes
WebAws serves as a perfect testament to Software Engineering (MERN) and Cloud Computing (AWS) skills. It is not just a static interface but a powerful Portal, capable of sophisticated access control via MongoDB while having the processing muscle to handle massive log volumes through the AWS Serverless ecosystem.
