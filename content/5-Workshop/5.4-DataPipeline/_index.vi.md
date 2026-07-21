---
title: "4. Cấu hình AWS Data Pipeline"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

Phần này trình bày cách tôi cấu hình 6 dịch vụ AWS tạo thành đường ống xử lý dữ liệu log từ đầu đến cuối.

### 1. Amazon EC2 - Máy chủ ứng dụng

EC2 đóng vai trò là máy chủ ảo (Server) lưu trữ và vận hành ứng dụng. Đây cũng chính là nơi phát sinh lưu lượng mạng (Network Traffic) để phục vụ việc thu thập và phân tích dữ liệu.

**Cấu hình đã sử dụng:**
* Instance Name: `Web-AI-Server`
* Instance Type: `t3.micro`
* AMI: Amazon Linux 2023
* Security Group: Cho phép HTTP (80), HTTPS (443), SSH (22)

![EC2 Instance](/images/Workshop/ec2.png)

### 2. Amazon VPC Flow Logs - Thu thập Log mạng

VPC Flow Logs thu thập và ghi lại toàn bộ nhật ký lưu lượng mạng giữa các tài nguyên trong Amazon VPC. Dữ liệu bao gồm: IP nguồn, IP đích, cổng kết nối, giao thức và trạng thái cho phép hoặc từ chối.

**Cách cấu hình:**
1. Mở **VPC Console** → chọn VPC đang chứa EC2 (Ví dụ: `vpc-0091f85a09d4344af`).
2. Chọn tab **Flow logs** → **Create flow log**.
3. Filter: `All` (ghi cả ACCEPT và REJECT).
4. Destination: `Send to an Amazon S3 bucket`.
5. S3 bucket ARN: `arn:aws:s3:::my-aws-bucket-nhom-2026`.
6. Maximum aggregation interval: `1 minute`.

![VPC Flow Logs](/images/Workshop/vpc.png)

### 3. AWS CloudTrail - Theo dõi hoạt động quản trị

CloudTrail ghi nhận toàn bộ các hoạt động quản trị và thao tác trên tài khoản AWS. Mọi lệnh gọi API (tạo EC2, xóa S3, thay đổi IAM...) đều được CloudTrail lưu lại.

* Trail S3 Bucket: `aws-cloudtrail-logs-765332581301-68340ac5`

### 4. Amazon S3 - Data Lake

S3 đóng vai trò là kho lưu trữ dữ liệu tập trung (Data Lake), lưu trữ toàn bộ các tệp nhật ký được thu thập từ VPC Flow Logs, CloudTrail và Kinesis Firehose. Dữ liệu này phục vụ cho việc phân tích dài hạn bằng Athena.

* Bucket: `my-aws-bucket-nhom-2026`

![S3 Data Lake](/images/Workshop/s3.png)

### 5. Amazon Kinesis Data Firehose - Đường ống dữ liệu

Kinesis Firehose hoạt động như một đường ống truyền dữ liệu (Data Pipeline). Thay vì ghi từng dòng log vào S3, Firehose gom nhóm (batch) các bản ghi lại và ghi một lần, giúp giảm chi phí PUT request đáng kể.

**Luồng hoạt động:**
```
VPC Flow Logs → CloudWatch → Kinesis Firehose → Lambda (lọc) → S3 Data Lake
```

![Kinesis Firehose](/images/Workshop/firehose.png)

### 6. AWS Lambda - Xử lý và lọc dữ liệu

Lambda là dịch vụ điện toán Serverless, thực hiện việc xử lý, lọc và định dạng dữ liệu nhật ký trước khi lưu vào S3. Hàm Lambda `my-log-filter` nhận dữ liệu từ Firehose, giải mã Base64, loại bỏ các bản ghi Control Message và chỉ giữ lại dữ liệu hữu ích.

**Code Lambda (Node.js):**
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
