---
title: "Worklog Tuần 11"
date: 2024-01-01
weight: 20
chapter: false
pre: " <b> 1.11.11. </b> "
---

### Mục tiêu tuần 11:

* Tích hợp AWS SDK vào Backend Node.js để gọi Athena.
* Chụp ảnh minh họa toàn bộ quy trình AWS trên Console.
* Bắt đầu viết báo cáo Workshop trên Hugo template.

### Các công việc đã triển khai trong tuần:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Cài đặt @aws-sdk/client-athena vào Backend Node.js | 30/06/2026 | 30/06/2026 | AWS SDK v3 |
| 3 | - Code hàm queryAthena() gọi từ Backend lấy Top IP bị REJECT | 01/07/2026 | 01/07/2026 | |
| 4 | - Chụp ảnh minh họa: EC2, VPC, S3, Lambda, Firehose, Athena, QuickSight, GuardDuty | 02/07/2026 | 02/07/2026 | AWS Console |
| 5 | - Clone Hugo template (fcj-workshop-template), bắt đầu viết Workshop | 03/07/2026 | 03/07/2026 | Hugo Docs |
| 6 | - Viết phần 5.1 (Tổng quan) và 5.2 (Prerequisites) cho Workshop | 04/07/2026 | 04/07/2026 | |

### Kết quả đạt được:

* Backend Node.js có thể gọi Athena Query trực tiếp qua AWS SDK, trả kết quả về React Dashboard.
* Thu thập đủ ảnh minh họa thực tế cho tất cả 9 dịch vụ AWS từ Console.
* Workshop website chạy thành công trên http://localhost:1313 với Hugo.
