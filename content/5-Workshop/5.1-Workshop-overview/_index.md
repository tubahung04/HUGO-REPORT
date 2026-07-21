---
title: "1. Overview & Architecture"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### 1. Context & Problem Statement
In large-scale Cloud environments, log data (VPC Flow Logs, CloudTrail) is massive. Manual analysis to find dangerous IPs or detect network intrusions is impossible. Meanwhile, built-in AWS Console monitoring tools (like CloudWatch Dashboard) lack customization for specific departments (Admin, SecOps, Manager).

**Solution**: Build a **Hybrid Architecture** system combining:
* **MERN Stack Web App**: Custom SOC Dashboard interface with 4-role access control (NetAdmin, SecOps, Manager, SystemAdmin), security alert management, global attack map.
* **AWS Serverless Data Pipeline**: 9 AWS services processing Big Data Logs behind the scenes without impacting main server performance.

### 2. Architecture Diagram
![AWS Data Pipeline Architecture](/images/Diagram.png)

### 3. Role of 9 AWS Services in the Project

| No. | Service | Role |
|-----|---------|------|
| 1 | **Amazon EC2** | Virtual server hosting and running the application. EC2 is also where network traffic is generated for data collection, monitoring, and analysis. |
| 2 | **Amazon VPC Flow Logs** | Collects and records all network traffic logs within the VPC, including source/destination IP, ports, protocols, and ACCEPT/REJECT status. |
| 3 | **AWS CloudTrail** | Records all administrative activities and operations on the AWS account, supporting auditing, monitoring, and security incident investigation. |
| 4 | **Amazon S3** | Centralized Data Lake storing all collected log files for analysis, querying, and long-term storage. |
| 5 | **Amazon Kinesis Data Firehose** | Data Pipeline automatically receiving, processing, and transferring log data to Amazon S3 in real-time. |
| 6 | **AWS Lambda** | Serverless computing service that processes, filters, and formats log data before storing in S3, standardizing data and removing unnecessary information. |
| 7 | **Amazon GuardDuty** | Uses AI and Machine Learning to automatically detect security threats: port scanning, unauthorized access, malware, and anomalous behavior. |
| 8 | **Amazon Athena** | Queries log data on S3 using SQL without building or managing databases, enabling fast and cost-effective analysis. |
| 9 | **Amazon QuickSight** | BI tool for data visualization, building charts, reports, and Dashboards for system analysis and monitoring. |

### 4. Web App Features Built

| Feature | Description |
|---------|-------------|
| **Login & RBAC** | 4 roles: NetAdmin, SecOps, Manager, SystemAdmin. Each role has different access permissions. |
| **KPI Dashboard** | Displays total traffic (GB), GuardDuty alerts count, Lookout anomalies count. |
| **Traffic Chart** | Line chart showing Bytes Sent/Received in real-time. |
| **Protocol Pie Chart** | Pie chart analyzing protocol ratios (TCP, HTTP, HTTPS, UDP, ICMP). |
| **Attack Map** | Global map showing geographic locations of attacking IPs (Brute Force, DDoS, Malware...). |
| **Security Alert Table** | Alert management table with statuses (New, In Progress, Resolved, False Positive). |
| **AI Anomaly Detection** | Chart comparing Forecast vs Actual to detect anomaly points. |
| **Top IP Console** | Top 10 IPs consuming most bandwidth, filterable by protocol. |
| **Infrastructure Health** | Real-time CPU, RAM, Disk usage monitoring. |

### 5. Security & IAM
* **Principle of Least Privilege**: AWS services communicate via IAM Roles with minimum permissions.
* **JWT Authentication**: Web App uses JSON Web Token for user authentication and authorization.
* **Role-Based Access Control (RBAC)**: Only SecOps and SystemAdmin can change security alert statuses.
* **Password Hashing**: User passwords are encrypted with bcrypt before storing in MongoDB.
