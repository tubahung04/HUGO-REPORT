---
title: "Worklog Tuần 11"
date: 2026-06-29
weight: 20
chapter: false
pre: " <b> 1.11.11. </b> "
---

### Các công việc đã triển khai trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| :--- | :--- | :--- | :--- |
| Thứ Hai | Khởi tạo máy chủ **EC2** để host ứng dụng. Setup project backend **Node.js/Express** và kết nối database **MongoDB**. | 29/06/2026 | 29/06/2026 |
| Thứ Ba | Bật **CloudWatch**, **VPC Flow Logs** và **CloudTrail** để bắt đầu thu thập log hệ thống và lưu lượng mạng thực tế. | 30/06/2026 | 30/06/2026 |
| Thứ Tư | Xây dựng Data Pipeline: Cấu hình **Kinesis Firehose** và code **Lambda Processor** để xử lý log trước khi đẩy vào **S3 Data Lake**. | 01/07/2026 | 01/07/2026 |
| Thứ Năm | Kích hoạt **GuardDuty** để dò quét lỗ hổng và dùng **EventBridge** để bắt các sự kiện (findings) bảo mật. | 02/07/2026 | 02/07/2026 |
| Thứ Sáu | Code **Alert Sync Lambda**: Tự động trigger từ EventBridge và bắn API `POST /api/internal/alerts` để lưu cảnh báo vào MongoDB. | 03/07/2026 | 03/07/2026 |
| Thứ Bảy | Hoàn thiện các REST API trên Node.js, tích hợp bảo mật **JWT** và phân quyền **RBAC** (admin, manager, secops...). | 04/07/2026 | 04/07/2026 |
| Chủ Nhật | Test luồng end-to-end bảo mật: Giả lập tấn công để GuardDuty phát hiện -> EventBridge -> Lambda -> Database. | 05/07/2026 | 05/07/2026 |

### Kết quả đạt được:
* Hoàn thành luồng Data Pipeline thu thập và lưu trữ log tự động về S3.
* Server Node.js và MongoDB đã chạy ổn định trên EC2.
* Luồng tự động hóa an ninh hoạt động trơn tru: Cảnh báo từ AWS GuardDuty được đồng bộ tức thì về database của ứng dụng web.
