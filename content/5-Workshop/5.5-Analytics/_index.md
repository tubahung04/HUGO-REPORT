---
title: "5. Analysis & Security Monitoring"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

After data has been collected and stored in the S3 Data Lake, this section covers how to use the remaining 3 AWS services for analysis and monitoring.

### 1. Amazon Athena - SQL Queries on S3

Athena enables querying log data stored on S3 using SQL without building or managing databases. Cost is based only on Data Scanned.

**Example query: Find Top 10 most REJECTED IPs**
```sql
SELECT srcAddr, COUNT(*) as reject_count
FROM vpc_flow_logs
WHERE action = 'REJECT'
GROUP BY srcAddr
ORDER BY reject_count DESC
LIMIT 10;
```

**Example query: Traffic statistics by protocol**
```sql
SELECT protocol, COUNT(*) as total_connections, SUM(bytes) as total_bytes
FROM vpc_flow_logs
GROUP BY protocol
ORDER BY total_bytes DESC;
```

Results from Athena serve as the data source for Dashboard Web App charts (Protocol Pie Chart, Top IP Console...).

![Amazon Athena Query](/images/Workshop/athena.png)

### 2. Amazon GuardDuty - AI Threat Detection

GuardDuty uses Artificial Intelligence (AI) and Machine Learning to automatically detect security threats: port scanning, unauthorized access, malware, and anomalous behavior.

**Real-world test scenario:**
To verify GuardDuty works, I deliberately created a simulated security risk:
1. Logged into AWS Console using the **Root** account (violating security principles).
2. Accessed **Billing and Cost Management** service.
3. Called the `GetCostAndUsage` API.

**Result:** GuardDuty detected it immediately and generated a Finding:
> *"The API GetCostAndUsage was invoked using root credentials from IP address..."*

This proves GuardDuty monitors 24/7 and detects any anomalous behavior.

![GuardDuty Alert](/images/Workshop/guardduty.png)

### 3. Amazon QuickSight - Data Visualization

QuickSight is a Business Intelligence (BI) tool for data visualization, building charts and Dashboards. In this project, I used QuickSight to create network traffic analysis charts from the S3 Data Lake.

**Charts created:**
* Bar chart: Count of records per source IP (srcAddr).
* Pie chart: Network protocol distribution ratios (TCP, UDP, ICMP).

![QuickSight Dashboard](/images/Workshop/quicksight.png)
