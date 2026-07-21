---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 41
chapter: false
pre: " <b> 1.5.5. </b> "
---

### Mục tiêu tuần 5:

* Xây dựng các API Endpoint cho Dashboard: overview, traffic, alerts, protocols, health, anomaly.
* Tạo dữ liệu giả (Seed Data) tự động khi khởi động server.
* Viết Blog 1 về tối ưu chi phí với S3 và Kinesis Firehose.

### Các công việc đã triển khai trong tuần:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Code API: GET /api/dashboard/overview (KPI tổng quan) | 19/05/2026 | 19/05/2026 | |
| 3 | - Code API: GET /api/security/alerts, GET /api/dashboard/map | 20/05/2026 | 20/05/2026 | |
| 4 | - Code API: GET /api/dashboard/protocols, /infrastructure/health | 21/05/2026 | 21/05/2026 | |
| 5 | - Xây dựng hàm seedDatabase() tự động bơm 6 Alert + 200 TrafficLog | 22/05/2026 | 22/05/2026 | |
| 6 | - Viết Blog 1: Tối ưu chi phí Big Data Log bằng S3 và Kinesis Firehose | 23/05/2026 | 23/05/2026 | |

### Kết quả đạt được:

* Hoàn thành 10 API Endpoint phục vụ toàn bộ Dashboard.
* Hệ thống tự động seed 4 User, 6 Alert (với geo_location), 200 TrafficLog khi khởi động.
* Hoàn thành Blog 1 và đăng lên AWS Study Group.
