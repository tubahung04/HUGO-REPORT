---
title: "7. Dọn dẹp tài nguyên (Clean-up)"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

Sau khi hoàn thành Workshop, hãy dọn dẹp các tài nguyên AWS để tránh phát sinh chi phí.

### 1. Xóa EC2 Instance
1. Vào **EC2 Console** → **Instances**.
2. Chọn instance `Web-AI-Server` → **Instance state** → **Terminate instance**.

### 2. Tắt VPC Flow Logs
1. Vào **VPC Console** → chọn VPC.
2. Tab **Flow logs** → chọn Flow log → **Actions** → **Delete flow log**.

### 3. Xóa S3 Bucket
1. Vào **S3 Console** → chọn bucket `my-aws-bucket-nhom-2026`.
2. **Empty** bucket trước (xóa hết object), sau đó **Delete** bucket.

### 4. Xóa Kinesis Firehose Stream
1. Vào **Kinesis Console** → **Delivery streams**.
2. Chọn stream → **Delete**.

### 5. Xóa Lambda Function
1. Vào **Lambda Console** → chọn function `my-log-filter`.
2. **Actions** → **Delete**.

### 6. Tắt GuardDuty
1. Vào **GuardDuty Console** → **Settings**.
2. **Suspend GuardDuty** hoặc **Disable GuardDuty**.

### 7. Dừng Web App Local
```bash
# Dừng Backend
Ctrl + C (trong terminal chạy npm start)

# Dừng Frontend
Ctrl + C (trong terminal chạy npm run dev)
```

> **Lưu ý:** Athena và QuickSight không tốn phí khi không sử dụng. Athena chỉ tính tiền khi chạy query, QuickSight có thể hủy đăng ký ở mục Account settings.
