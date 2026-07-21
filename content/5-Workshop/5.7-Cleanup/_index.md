---
title: "7. Resource Clean-up"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

After completing the Workshop, clean up AWS resources to avoid incurring costs.

### 1. Delete EC2 Instance
1. Go to **EC2 Console** → **Instances**.
2. Select `Web-AI-Server` → **Instance state** → **Terminate instance**.

### 2. Disable VPC Flow Logs
1. Go to **VPC Console** → select VPC.
2. **Flow logs** tab → select Flow log → **Actions** → **Delete flow log**.

### 3. Delete S3 Bucket
1. Go to **S3 Console** → select `my-aws-bucket-nhom-2026`.
2. **Empty** bucket first (delete all objects), then **Delete** bucket.

### 4. Delete Kinesis Firehose Stream
1. Go to **Kinesis Console** → **Delivery streams**.
2. Select stream → **Delete**.

### 5. Delete Lambda Function
1. Go to **Lambda Console** → select `my-log-filter`.
2. **Actions** → **Delete**.

### 6. Disable GuardDuty
1. Go to **GuardDuty Console** → **Settings**.
2. **Suspend GuardDuty** or **Disable GuardDuty**.

### 7. Stop Local Web App
```bash
# Stop Backend
Ctrl + C (in terminal running npm start)

# Stop Frontend
Ctrl + C (in terminal running npm run dev)
```

> **Note:** Athena and QuickSight don't incur charges when not in use. Athena only charges per query, and QuickSight can be unsubscribed in Account settings.
