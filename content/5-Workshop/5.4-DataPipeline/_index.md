---
title: "4. Configuring AWS Data Pipeline"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

This section details how I configured 6 AWS services to create an end-to-end log data processing pipeline.

### 1. Amazon EC2 - Application Server

EC2 acts as a virtual server hosting and running the application. It is also where network traffic is generated for data collection and analysis.

**Configuration used:**
* Instance Name: `Web-AI-Server`
* Instance Type: `t3.micro`
* AMI: Amazon Linux 2023
* Security Group: Allow HTTP (80), HTTPS (443), SSH (22)

![EC2 Instance](/images/Workshop/ec2.png)

### 2. Amazon VPC Flow Logs - Network Log Collection

VPC Flow Logs collects and records all network traffic logs within the Amazon VPC. Data includes: source IP, destination IP, ports, protocols, and ACCEPT/REJECT status.

**Configuration steps:**
1. Open **VPC Console** → select the VPC containing EC2 (e.g., `vpc-0091f85a09d4344af`).
2. Select **Flow logs** tab → **Create flow log**.
3. Filter: `All` (record both ACCEPT and REJECT).
4. Destination: `Send to an Amazon S3 bucket`.
5. S3 bucket ARN: `arn:aws:s3:::my-aws-bucket-nhom-2026`.
6. Maximum aggregation interval: `1 minute`.

![VPC Flow Logs](/images/Workshop/vpc.png)

### 3. AWS CloudTrail - Admin Activity Tracking

CloudTrail records all administrative activities and operations on the AWS account. Every API call (create EC2, delete S3, change IAM...) is captured by CloudTrail.

* Trail S3 Bucket: `aws-cloudtrail-logs-765332581301-68340ac5`
![CloudTrail](/images/Workshop/cloudtrail.jpg)

### 4. Amazon S3 - Data Lake

S3 acts as the centralized Data Lake, storing all log files collected from VPC Flow Logs, CloudTrail, and Kinesis Firehose. This data serves long-term analysis via Athena.

* Bucket: `my-aws-bucket-nhom-2026`

![S3 Data Lake](/images/Workshop/s3.png)

### 5. Amazon Kinesis Data Firehose - Data Pipeline

Kinesis Firehose acts as a data pipeline. Instead of writing each log line to S3, Firehose batches records and writes once, significantly reducing PUT request costs.

**Data flow:**
```
VPC Flow Logs → CloudWatch → Kinesis Firehose → Lambda (filter) → S3 Data Lake
```

![Kinesis Firehose](/images/Workshop/firehose.png)

### 6. AWS Lambda - Data Processing and Filtering

Lambda is a Serverless computing service that processes, filters, and formats log data before storing in S3. The `my-log-filter` Lambda function receives data from Firehose, decodes Base64, removes Control Messages, and keeps only useful data.

**Lambda Code (Node.js):**
```javascript
exports.handler = async (event) => {
  const output = event.records.map(record => {
    const payload = Buffer.from(record.data, 'base64').toString('utf8');
    try {
      const data = JSON.parse(payload);
      if (data.messageType === 'CONTROL_MESSAGE') {
        return { recordId: record.recordId, result: 'Dropped' };
      }
      return { 
        recordId: record.recordId, 
        result: 'Ok',
        data: Buffer.from(JSON.stringify(data) + '\n').toString('base64')
      };
    } catch (e) {
      return { recordId: record.recordId, result: 'Ok', data: record.data };
    }
  });
  return { records: output };
};
```

![Lambda Function](/images/Workshop/lamda.png)
