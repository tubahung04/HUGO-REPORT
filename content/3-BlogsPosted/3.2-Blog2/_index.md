---
title: "Blog 2: Serverless Data Querying with Amazon Athena and Web App Integration"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

### Context
After having an S3 Data Lake filled with JSON log files (as shared in Blog 1), how can the Node.js Backend system retrieve the Top 5 IP addresses showing anomalous signs (constantly REJECTED)?

### Solution with Amazon Athena
Instead of provisioning and operating an expensive SQL Server or Elasticsearch system, I used **Amazon Athena**.
Athena is a Serverless service that allows running SQL queries directly against static files stored in S3.
SELECT srcAddr, COUNT(*) as hit_count FROM vpc_flow_logs WHERE action = 'REJECT' GROUP BY srcAddr ORDER BY hit_count DESC LIMIT 5;

### Integration into the MERN Stack System
In the Hybrid architecture of the project, my React Frontend displays a beautiful SOC Dashboard. When users want to view security reports, the Node.js Backend uses the aws-sdk to send SQL queries to Athena.
Athena charges based on Data Scanned - usually costing less than $0.01 per query. The results are then returned to the Backend and rendered on React.
The combination of a traditional Web App and AWS Analytics has brought incredible power to the system!
