---
title: "Blog 1: Cost Optimization for Big Data Logs with S3 and Kinesis Firehose"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

### Introduction
When building the **AWS Observability & Security Dashboard**, one of the biggest challenges was processing massive amounts of data (Big Data) from VPC Flow Logs and CloudTrail without breaking the bank. Instead of using traditional databases, I designed a completely Serverless Data Pipeline.

### Architectural Solution
I used a combination of **Amazon Kinesis Data Firehose** and **Amazon S3**:
1. **Collection and Batching**: Kinesis Firehose doesn't write single log lines immediately to S3. Instead, it batches the network flows into large chunks (e.g., once a minute). This reduces the number of PUT requests to S3 by thousands of times, saving massive costs.
2. **Cleaning with Lambda**: Before writing to S3, Firehose automatically invokes the my-log-filter Lambda function to format the logs into standard JSON.
3. **Cold Storage on S3**: The cleaned data is pushed into the my-aws-bucket-nhom-2026 bucket. S3 is the cheapest and most durable Object Storage on AWS.

### Results
By applying this model, my Backend system (MERN Stack) doesn't have to carry the heavy lifting of data processing. All Big Data processing is handled seamlessly by AWS for just a few cents a month (Pay-as-you-go). This is a standard architecture for Cloud data processing!
