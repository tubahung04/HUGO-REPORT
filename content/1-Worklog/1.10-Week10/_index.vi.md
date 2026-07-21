---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 91
chapter: false
pre: " <b> 1.10.10. </b> "
---

### Mục tiêu tuần 10:

* Cấu hình Amazon Athena: Tạo database, table truy vấn VPC Flow Logs trên S3.
* Cấu hình Amazon QuickSight: Tạo Dashboard trực quan hóa dữ liệu.
* Viết Blog 3 về Amazon GuardDuty.

### Các công việc đã triển khai trong tuần:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tạo Athena Database và Table trỏ về S3 Data Lake | 23/06/2026 | 23/06/2026 | AWS Athena Docs |
| 3 | - Chạy query SQL test: SELECT srcAddr, COUNT(*) ... WHERE action='REJECT' | 24/06/2026 | 24/06/2026 | |
| 4 | - Đăng ký QuickSight, kết nối Data Source với Athena | 25/06/2026 | 25/06/2026 | AWS QuickSight |
| 5 | - Tạo Dashboard trên QuickSight: Biểu đồ cột IP, biểu đồ tròn Protocol | 26/06/2026 | 26/06/2026 | |
| 6 | - Viết Blog 3: Giám sát an ninh đám mây bằng Amazon GuardDuty | 27/06/2026 | 27/06/2026 | |

### Kết quả đạt được:

* Athena truy vấn thành công dữ liệu VPC Flow Logs từ S3 với chi phí gần $0.
* QuickSight Dashboard hiển thị biểu đồ Count of Records by srcAddr, Protocol distribution.
* Hoàn thành Blog 3 về GuardDuty và đăng lên AWS Study Group.
