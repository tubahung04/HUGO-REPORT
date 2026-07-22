---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AWS Observability & Security Dashboard
## Giải pháp phân tích An ninh kết hợp (Hybrid): Web App MERN Stack và AWS Data Pipeline

### 1. Tóm tắt điều hành
AWS Observability & Security Dashboard là một nền tảng giám sát tập trung (SOC) được thiết kế theo kiến trúc Lai (Hybrid Architecture). Ứng dụng tận dụng sức mạnh của hệ sinh thái **MERN Stack (MongoDB, Express, React, Node.js)** để xây dựng giao diện người dùng và quản lý dữ liệu ứng dụng (Users, Roles, Alert Statuses). Đồng thời, hệ thống kết nối trực tiếp với **AWS Serverless Data Pipeline** (Kinesis, S3, Athena, GuardDuty) thông qua AWS SDK để thu thập và phân tích dữ liệu log cực lớn theo thời gian thực. Bằng cách kết hợp này, dự án mang đến trải nghiệm phần mềm mượt mà nhưng vẫn tận dụng được sức mạnh Big Data của đám mây.

### 2. Tuyên bố vấn đề
*Vấn đề hiện tại*
Trong các môi trường Cloud quy mô lớn, dữ liệu log (VPC Flow Logs, CloudTrail) rất khổng lồ. Việc phân tích thủ công để tìm IP ngốn băng thông hoặc phát hiện xâm nhập mạng là bất khả thi. Các công cụ truyền thống gặp hai rào cản: 
1. Chi phí duy trì hạ tầng SQL đắt đỏ khi xử lý Big Data.
2. Thiếu một giao diện (UI) tùy chỉnh linh hoạt phù hợp với nhu cầu của từng bộ phận (Admin, SecOps).

*Giải pháp*
Dự án áp dụng phương pháp chia để trị (Decoupled):
- **Phần Web (Frontend + Backend Node.js + MongoDB)**: Đảm nhận giao diện, cơ chế Đăng nhập (JWT), Phân quyền (RBAC) và lưu trữ trạng thái của các cảnh báo sự cố. MongoDB giúp truy xuất dữ liệu ứng dụng cực nhanh và dễ tùy biến.
- **Phần AWS (Data Pipeline)**: Đảm nhận phần "nặng nhọc" nhất là thu thập và phân tích Logs. Kinesis Firehose đẩy log vào S3. Amazon Athena thực hiện truy vấn SQL trên S3. Node.js sẽ gọi API của Athena để lấy kết quả (Ví dụ: Top IP truy cập) và trả về cho React hiển thị.

*Lợi ích và hoàn vốn đầu tư (ROI)*
Kiến trúc Hybrid tối ưu hóa chi phí đến mức tối đa. MongoDB lưu dữ liệu nhẹ của ứng dụng hoàn toàn miễn phí, trong khi AWS chỉ tính tiền theo lượng dữ liệu quét (Pay-as-you-go). Sự kết hợp này phô diễn năng lực lập trình toàn diện của một Software Engineer: Vừa biết xây dựng phần mềm Fullstack, vừa biết cách tích hợp và xử lý dữ liệu lớn trên AWS.

### 3. Kiến trúc giải pháp
Dự án là sự giao thoa hoàn hảo giữa kỹ thuật Software Engineering và Cloud Architecture.
![AWS Data Pipeline Architecture](../images/2-Proposal/sodo1.png)

*Luồng dữ liệu AWS (Data Engine)*
- **Amazon S3**: Lưu trữ dữ liệu Log (Data Lake).
- **Amazon Kinesis Firehose**: Streaming dữ liệu log từ hạ tầng.
- **AWS Lambda**: Xử lý, làm sạch và biến đổi dữ liệu trước khi vào S3.
- **Amazon Athena**: Truy vấn phân tích dữ liệu lớn trên S3.
- **Amazon GuardDuty**: Dò tìm và phát hiện IP độc hại.
- **Amazon QuickSight**: Thiết kế BI Dashboard và nhúng (Embed) vào React.

*Ứng dụng Web (Web App)*
- **Frontend (ReactJS + TailwindCSS)**: Giao diện Glassmorphism, Recharts (Biểu đồ) và react-simple-maps (Bản đồ Threat Map).
- **Backend (Node.js)**: API Gateway kết nối với MongoDB (xác thực User) và gọi **AWS SDK** (truy xuất Athena/GuardDuty).
- **Database (MongoDB)**: Quản lý thông tin User, RBAC Roles, JWT Token và trạng thái Ticket sự cố.

### 4. Triển khai kỹ thuật
*Các giai đoạn triển khai*
1. **Thiết lập Web**: Khởi tạo React, Node.js và MongoDB. Xây dựng Authentication (JWT) và RBAC.
2. **Thiết lập AWS Pipeline**: Bật VPC Flow Logs/CloudTrail, cấu hình Kinesis Firehose đẩy vào S3 qua Lambda Processor.
3. **Tích hợp Backend - AWS**: Lập trình Node.js sử dụng AWS SDK để kết nối Athena, truy xuất danh sách Top IP và GuardDuty Findings.
4. **Phát triển UI**: Vẽ biểu đồ Recharts, hiển thị Bản đồ thế giới quét radar tại các IP độc hại. Nhúng QuickSight.
5. **Hoàn thiện**: Kiểm thử End-to-End toàn bộ luồng từ MongoDB đến AWS S3. Viết tài liệu.

### 5. Lộ trình & Mốc triển khai (12 Tuần)
- *Tháng 1 (Tuần 1-4)*: Thiết kế kiến trúc Hybrid, khởi tạo dự án MERN Stack, thiết kế DB Schema, hoàn thiện Login JWT và Phân quyền (RBAC).
- *Tháng 2 (Tuần 5-8)*: Xây dựng AWS Data Pipeline (Kinesis -> Lambda -> S3). Node.js gọi AWS SDK truy vấn Athena đổ dữ liệu lên bảng Network Traffic ở Web.
- *Tháng 3 (Tuần 9-12)*: Tích hợp GuardDuty lên Bản đồ Threat Map. Sử dụng MongoDB để tạo tính năng Đổi trạng thái sự cố (Alert Management). Nhúng QuickSight. Báo cáo tổng kết.

### 6. Ước tính ngân sách

Dự án được triển khai hoàn toàn trong phạm vi **$200 AWS Free Tier Credit** được cấp bởi chương trình thực tập. Để tiết kiệm chi phí, EC2 Instance chỉ được **bật khi cần sử dụng** và **tắt khi không dùng**. Dưới đây là bảng tính toán chi phí thực tế:

| Dịch vụ | Chi phí ước tính | Ghi chú |
| :--- | :--- | :--- |
| **Amazon EC2 (t3.micro)** | ~$8.00 | Bật/tắt theo nhu cầu (~770 giờ thực tế × $0.0104/giờ). 750 giờ/tháng đầu miễn phí (Free Tier), phần dư tính phí. |
| **Amazon S3 (Data Lake)** | ~$2.50 | Lưu trữ 50GB log data ($0.023/GB/tháng) + PUT/GET requests ($0.50) |
| **Amazon Kinesis Firehose** | ~$5.00 | Xử lý ~100GB data ingestion ($0.029/GB cho 500MB đầu tiên miễn phí) |
| **AWS Lambda (my-log-filter)** | ~$0.50 | ~500,000 lần gọi × $0.20/1M requests. 1M requests đầu tiên miễn phí mỗi tháng |
| **Amazon Athena** | ~$1.50 | ~300 lần query × ~1MB data scanned mỗi lần ($5/TB). Tổng ~300MB scanned |
| **Amazon QuickSight** | ~$24.00 | 1 Author license ($24/tháng). Chỉ đăng ký 1 tháng cuối để tạo Dashboard demo |
| **Amazon GuardDuty** | ~$8.00 | Phân tích VPC Flow Logs (~$1.15/GB cho 500MB đầu tiên miễn phí) + CloudTrail Events |
| **AWS CloudTrail** | ~$2.00 | 1 Trail miễn phí. Chi phí phát sinh từ S3 storage cho trail logs |
| **VPC Flow Logs** | ~$3.00 | Đẩy log về CloudWatch Logs ($0.50/GB ingested) + S3 storage. Ước tính ~6GB log trong 12 tuần |
| **MongoDB Atlas (M0 Free Tier)**| $0.00 | Sử dụng cluster M0 miễn phí vĩnh viễn (512MB storage, đủ cho dữ liệu User, Alert, TrafficLog) |
| **Web App Hosting (trên EC2)** | $0.00 | Web App được deploy trực tiếp trên EC2 Instance ở trên, không tốn thêm chi phí riêng |
| **TỔNG CỘNG** | **~$54.50** | Còn dư **~$145.50** trong $200 Credit |

### 7. Đánh giá rủi ro
*Ma trận rủi ro*
- Lộ AWS Credentials từ ứng dụng Node.js (Ảnh hưởng: Rất cao, Xác suất: Trung bình).
- Giao diện Web bị đứng khi render đồng thời Recharts và react-simple-maps (Ảnh hưởng: Trung bình, Xác suất: Trung bình).

*Chiến lược giảm thiểu*
- Sử dụng IAM Roles thay vì Access Key cứng. Đưa toàn bộ cấu hình vào file `.env` và đẩy lên `.gitignore`.
- Dùng `useMemo`, `useCallback` ở React Frontend để tránh re-render bản đồ không cần thiết.

### 8. Kết quả kỳ vọng
WebAws đóng vai trò là một minh chứng hoàn hảo về kỹ năng Software Engineering (MERN) và Cloud Computing (AWS). Nó không chỉ là một giao diện tĩnh mà là một Cổng thông tin (Portal) mạnh mẽ, có khả năng phân quyền tinh vi qua MongoDB và đồng thời có đủ sức mạnh để xử lý khối lượng Log khổng lồ thông qua hệ sinh thái AWS Serverless.
