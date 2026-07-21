---
title: "6. Integrating AWS into the Web App"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

This section best demonstrates the **Hybrid Architecture** nature of the project. Data from AWS Data Pipeline is integrated back into the MERN Stack Web App.

### 1. End-to-End Data Flow

```
[EC2 Traffic] → [VPC Flow Logs] → [CloudWatch] → [Kinesis Firehose] → [Lambda Filter] → [S3 Data Lake]
                                                                                              ↓
[React Dashboard] ← [Node.js Backend] ← [Athena SQL Query] ← ← ← ← ← ← ← ← ← ← ← ← ← ←
```

The Web App acts as the **Presentation Layer**, while AWS acts as the **Data Processing Layer**.

### 2. How the Web App Calls AWS Data

The Node.js Backend uses the `@aws-sdk/client-athena` library to send SQL queries to Athena. Athena processes data from the S3 Data Lake and returns results. The Backend formats and serves them to React via REST API.

```javascript
// Example: Backend calls Athena for Top IPs
const { AthenaClient, StartQueryExecutionCommand } = require('@aws-sdk/client-athena');

const queryTopIPs = async () => {
  const client = new AthenaClient({ region: 'ap-southeast-1' });
  const command = new StartQueryExecutionCommand({
    QueryString: "SELECT srcAddr, COUNT(*) as hits FROM vpc_flow_logs WHERE action='REJECT' GROUP BY srcAddr ORDER BY hits DESC LIMIT 10",
    ResultConfiguration: { OutputLocation: 's3://my-aws-bucket-nhom-2026/athena-results/' }
  });
  return await client.send(command);
};
```

### 3. Mapping Between AWS and React Components

| React Component | AWS Data Source |
|-----------------|---------------|
| **KPICards** | Aggregated from TrafficLog (MongoDB) + GuardDuty Finding count |
| **TrafficChart** | VPC Flow Logs → Athena → Backend API |
| **ProtocolPieChart** | VPC Flow Logs analyzed by protocol via Athena |
| **AttackMap** | Alert data combined with geo_location (simulated from GuardDuty Findings) |
| **AlertTable** | GuardDuty Findings → MongoDB Alert collection |
| **AIAnomalyChart** | Lookout for Metrics / CloudWatch anomaly data |
| **TopIPConsole** | VPC Flow Logs → Athena GROUP BY srcAddr |
| **InfraHealth** | EC2 CloudWatch Metrics (CPU, Memory, Disk) |

### 4. Advantages of the Hybrid Architecture

* **Separation of concerns**: Web App handles UI, AWS handles Big Data processing.
* **Cost savings**: No need for 24/7 SQL Server, only pay when querying Athena.
* **Easy to scale**: Adding new log sources only requires configuring a new Firehose, no Web App code changes.
* **Security**: Sensitive data in S3 is protected by IAM, Web App only receives processed results.
