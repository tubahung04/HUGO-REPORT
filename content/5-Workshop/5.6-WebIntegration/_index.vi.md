---
title: "6. Tích hợp AWS vào Web App"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

Đây là phần thể hiện rõ nhất tính chất **Kiến trúc Lai (Hybrid)** của dự án. Dữ liệu từ AWS Data Pipeline được tích hợp ngược vào Web App MERN Stack.

### 1. Luồng dữ liệu End-to-End

```
[EC2 Traffic] → [VPC Flow Logs] → [CloudWatch] → [Kinesis Firehose] → [Lambda Filter] → [S3 Data Lake]
                                                                                              ↓
[React Dashboard] ← [Node.js Backend] ← [Athena SQL Query] ← ← ← ← ← ← ← ← ← ← ← ← ← ←
```

Web App đóng vai trò **lớp hiển thị (Presentation Layer)**, trong khi AWS đóng vai trò **lớp xử lý dữ liệu (Data Processing Layer)**.

### 2. Cách Web App gọi dữ liệu từ AWS

Backend Node.js sử dụng thư viện `@aws-sdk/client-athena` để gửi câu truy vấn SQL lên Athena. Athena tính toán dựa trên dữ liệu trong S3 Data Lake rồi trả kết quả về. Backend format lại rồi trả cho React qua REST API.

```javascript
// Ví dụ: Backend gọi Athena lấy Top IP
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

### 3. Tương quan giữa AWS và từng Component React

| Component React | Nguồn dữ liệu AWS |
|-----------------|-------------------|
| **KPICards** | Tổng hợp từ TrafficLog (MongoDB) + số Finding từ GuardDuty |
| **TrafficChart** | VPC Flow Logs → Athena → Backend API |
| **ProtocolPieChart** | VPC Flow Logs phân tích theo protocol qua Athena |
| **AttackMap** | Dữ liệu Alert kết hợp geo_location (mô phỏng từ GuardDuty Findings) |
| **AlertTable** | GuardDuty Findings → MongoDB Alert collection |
| **AIAnomalyChart** | Lookout for Metrics / CloudWatch anomaly data |
| **TopIPConsole** | VPC Flow Logs → Athena GROUP BY srcAddr |
| **InfraHealth** | EC2 CloudWatch Metrics (CPU, Memory, Disk) |

### 4. Ưu điểm của Kiến trúc Lai

* **Tách biệt trách nhiệm**: Web App lo giao diện, AWS lo xử lý Big Data.
* **Tiết kiệm chi phí**: Không cần chạy SQL Server 24/7, chỉ trả tiền khi query Athena.
* **Mở rộng dễ dàng**: Thêm nguồn log mới chỉ cần cấu hình thêm Firehose, không cần sửa code Web App.
* **Bảo mật**: Dữ liệu nhạy cảm ở S3 được bảo vệ bằng IAM, Web App chỉ lấy kết quả đã xử lý.
