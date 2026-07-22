---
title: "Worklog Week 11"
date: 2026-06-29
weight: 20
chapter: false
pre: " <b> 1.11.11. </b> "
---

### Tasks carried out this week:

| Day | Task | Start Date | Completion Date |
| :--- | :--- | :--- | :--- |
| Mon | Provisioned an **EC2** instance to host the application. Initialized the **Node.js/Express** backend and connected to **MongoDB**. | 29/06/2026 | 29/06/2026 |
| Tue | Enabled **CloudWatch**, **VPC Flow Logs**, and **CloudTrail** to start capturing system metrics and real network traffic. | 30/06/2026 | 30/06/2026 |
| Wed | Built the Data Pipeline: Configured **Kinesis Firehose** and wrote a **Lambda Processor** to transform logs before dumping them into the **S3 Data Lake**. | 01/07/2026 | 01/07/2026 |
| Thu | Activated **GuardDuty** for threat detection and configured **EventBridge** rules to catch security findings. | 02/07/2026 | 02/07/2026 |
| Fri | Coded the **Alert Sync Lambda**: Triggered by EventBridge to send a `POST /api/internal/alerts` request, saving alerts directly into MongoDB. | 03/07/2026 | 03/07/2026 |
| Sat | Finalized the REST APIs in Node.js, implementing **JWT** authentication and **RBAC** for different roles (admin, manager, secops). | 04/07/2026 | 04/07/2026 |
| Sun | Tested the end-to-end security flow: Simulated a threat to verify the GuardDuty -> EventBridge -> Lambda -> Database pipeline. | 05/07/2026 | 05/07/2026 |

### Results achieved:
* Successfully established an automated Data Pipeline streaming logs into the S3 Data Lake.
* The Node.js server and MongoDB are running stably on the EC2 instance.
* Security automation works flawlessly: AWS GuardDuty findings are instantly synced to the web app's database.
