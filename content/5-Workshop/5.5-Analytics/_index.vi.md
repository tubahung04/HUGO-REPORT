---
title: "5. Phân tích & Giám sát bảo mật"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

Sau khi dữ liệu đã được thu thập và lưu trữ trong S3 Data Lake, phần này trình bày cách sử dụng 3 dịch vụ AWS còn lại để phân tích và giám sát.

### 1. Amazon Athena - Truy vấn SQL trên S3

Athena cho phép truy vấn dữ liệu nhật ký được lưu trữ trên S3 bằng SQL mà không cần xây dựng hay quản lý cơ sở dữ liệu. Chi phí chỉ tính trên lượng dữ liệu quét (Data Scanned).

**Ví dụ truy vấn: Tìm Top 10 IP bị REJECT nhiều nhất**
```sql
SELECT srcAddr, COUNT(*) as reject_count
FROM vpc_flow_logs
WHERE action = 'REJECT'
GROUP BY srcAddr
ORDER BY reject_count DESC
LIMIT 10;
```

**Ví dụ truy vấn: Thống kê lưu lượng theo giao thức**
```sql
SELECT protocol, COUNT(*) as total_connections, SUM(bytes) as total_bytes
FROM vpc_flow_logs
GROUP BY protocol
ORDER BY total_bytes DESC;
```

Kết quả từ Athena chính là nguồn dữ liệu cho các biểu đồ trên Dashboard Web App (Protocol Pie Chart, Top IP Console...).

![Amazon Athena Query](/images/Workshop/athena.png)

### 2. Amazon GuardDuty - Phát hiện mối đe dọa bằng AI

GuardDuty sử dụng trí tuệ nhân tạo (AI) và Machine Learning để tự động phát hiện các mối đe dọa bảo mật: quét cổng (Port Scanning), truy cập trái phép, phần mềm độc hại (Malware) và hành vi bất thường.

**Kịch bản kiểm thử thực tế:**
Để kiểm chứng GuardDuty hoạt động, tôi đã cố tình tạo một rủi ro bảo mật mô phỏng:
1. Đăng nhập AWS Console bằng tài khoản **Root** (vi phạm nguyên tắc bảo mật).
2. Truy cập dịch vụ **Billing and Cost Management**.
3. Gọi API `GetCostAndUsage`.

**Kết quả:** GuardDuty phát hiện ngay lập tức và tạo cảnh báo (Finding):
> *"The API GetCostAndUsage was invoked using root credentials from IP address..."*

Điều này chứng minh GuardDuty luôn giám sát 24/7 và phát hiện mọi hành vi bất thường.

![GuardDuty Alert](/images/Workshop/guardduty.png)

### 3. Amazon QuickSight - Trực quan hóa dữ liệu

QuickSight là công cụ Business Intelligence (BI) dùng để trực quan hóa dữ liệu, xây dựng biểu đồ và Dashboard. Trong dự án, tôi sử dụng QuickSight để tạo các biểu đồ phân tích lưu lượng mạng từ S3 Data Lake.

**Các biểu đồ đã tạo:**
* Biểu đồ cột: Đếm số lượng bản ghi theo từng IP nguồn (srcAddr).
* Biểu đồ tròn: Tỷ lệ phân bổ giao thức mạng (TCP, UDP, ICMP).

![QuickSight Dashboard](/images/Workshop/quicksight.png)
