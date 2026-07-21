---
title: "1. Tổng quan & Kiến trúc (Overview)"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### 1. Bối cảnh & Bài toán
Trong các môi trường Cloud quy mô lớn, dữ liệu log (VPC Flow Logs, CloudTrail) rất khổng lồ. Việc phân tích thủ công để tìm IP nguy hiểm hoặc phát hiện xâm nhập mạng là bất khả thi. Đồng thời, các công cụ giám sát có sẵn trên AWS Console (như CloudWatch Dashboard) lại thiếu tính tùy biến cho từng bộ phận (Admin, SecOps, Manager).

**Giải pháp**: Xây dựng một hệ thống **Kiến trúc Lai (Hybrid)** kết hợp:
* **MERN Stack Web App**: Giao diện SOC Dashboard tùy chỉnh với hệ thống phân quyền 4 vai trò (NetAdmin, SecOps, Manager, SystemAdmin), quản lý cảnh báo bảo mật, bản đồ tấn công toàn cầu.
* **AWS Serverless Data Pipeline**: 9 dịch vụ AWS xử lý Big Data Log ngầm phía sau, không ảnh hưởng hiệu suất máy chủ chính.

### 2. Sơ đồ kiến trúc (Architecture Diagram)
![AWS Data Pipeline Architecture](/images/Diagram.png)

### 3. Vai trò của 9 dịch vụ AWS trong dự án

| STT | Dịch vụ | Vai trò |
|-----|---------|---------|
| 1 | **Amazon EC2** | Máy chủ ảo lưu trữ và vận hành ứng dụng. EC2 cũng là nơi phát sinh lưu lượng mạng (Network Traffic) để phục vụ việc thu thập, giám sát và phân tích dữ liệu trong hệ thống. |
| 2 | **Amazon VPC Flow Logs** | Thu thập và ghi lại toàn bộ nhật ký lưu lượng mạng giữa các tài nguyên trong VPC, bao gồm IP nguồn, IP đích, cổng kết nối, giao thức và trạng thái ACCEPT/REJECT. |
| 3 | **AWS CloudTrail** | Ghi nhận toàn bộ các hoạt động quản trị và thao tác trên tài khoản AWS, hỗ trợ kiểm toán, giám sát và điều tra sự cố bảo mật. |
| 4 | **Amazon S3** | Kho lưu trữ dữ liệu tập trung (Data Lake), lưu trữ toàn bộ các tệp nhật ký (Log Files) để phục vụ phân tích, truy vấn và lưu trữ lâu dài. |
| 5 | **Amazon Kinesis Data Firehose** | Đường ống truyền dữ liệu (Data Pipeline), tự động tiếp nhận, xử lý và chuyển dữ liệu nhật ký từ nguồn đến Amazon S3 theo thời gian thực. |
| 6 | **AWS Lambda** | Dịch vụ điện toán Serverless, xử lý, lọc và định dạng dữ liệu nhật ký trước khi lưu vào S3, giúp chuẩn hóa dữ liệu và loại bỏ thông tin không cần thiết. |
| 7 | **Amazon GuardDuty** | Sử dụng AI và Machine Learning để tự động phát hiện các mối đe dọa bảo mật: quét cổng, truy cập trái phép, phần mềm độc hại và hành vi bất thường. |
| 8 | **Amazon Athena** | Truy vấn dữ liệu nhật ký trên S3 bằng SQL mà không cần xây dựng hay quản lý cơ sở dữ liệu, phân tích nhanh chóng và tiết kiệm chi phí. |
| 9 | **Amazon QuickSight** | Công cụ BI trực quan hóa dữ liệu, xây dựng biểu đồ, báo cáo và Dashboard để phân tích và giám sát hệ thống. |

### 4. Các chức năng Web App đã xây dựng

| Chức năng | Mô tả |
|-----------|-------|
| **Login & Phân quyền (RBAC)** | 4 vai trò: NetAdmin, SecOps, Manager, SystemAdmin. Mỗi vai trò có quyền truy cập khác nhau. |
| **KPI Dashboard** | Hiển thị tổng lưu lượng (GB), số cảnh báo GuardDuty, số bất thường Lookout. |
| **Traffic Chart** | Biểu đồ đường hiển thị Bytes Sent/Received theo thời gian thực. |
| **Protocol Pie Chart** | Biểu đồ tròn phân tích tỷ lệ giao thức (TCP, HTTP, HTTPS, UDP, ICMP). |
| **Attack Map** | Bản đồ toàn cầu hiển thị vị trí địa lý của các IP tấn công (Brute Force, DDoS, Malware...). |
| **Security Alert Table** | Bảng quản lý cảnh báo bảo mật với trạng thái (New, In Progress, Resolved, False Positive). |
| **AI Anomaly Detection** | Biểu đồ so sánh Forecast vs Actual để phát hiện điểm bất thường (Anomaly). |
| **Top IP Console** | Bảng xếp hạng Top 10 IP tiêu thụ băng thông nhiều nhất, lọc theo giao thức. |
| **Infrastructure Health** | Theo dõi CPU, RAM, Disk usage của máy chủ theo thời gian thực. |

### 5. Bảo mật & IAM
* **Principle of Least Privilege**: Các dịch vụ AWS giao tiếp qua IAM Role chỉ được cấp quyền tối thiểu.
* **JWT Authentication**: Web App sử dụng JSON Web Token để xác thực và phân quyền người dùng.
* **Role-Based Access Control (RBAC)**: Chỉ SecOps và SystemAdmin mới được thay đổi trạng thái cảnh báo bảo mật.
* **Password Hashing**: Mật khẩu người dùng được mã hóa bằng bcrypt trước khi lưu vào MongoDB.
