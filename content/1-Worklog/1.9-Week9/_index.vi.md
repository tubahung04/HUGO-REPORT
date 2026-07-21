---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 81
chapter: false
pre: " <b> 1.9.9. </b> "
---

### Mục tiêu tuần 9:

* Cấu hình AWS Data Pipeline: VPC Flow Logs, CloudTrail, S3.
* Thiết lập Amazon Kinesis Data Firehose và viết hàm AWS Lambda lọc dữ liệu.
* Kích hoạt Amazon GuardDuty.

### Các công việc đã triển khai trong tuần:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Bật VPC Flow Logs: Filter=All, Destination=S3, Interval=1 min | 16/06/2026 | 16/06/2026 | AWS VPC Docs |
| 3 | - Cấu hình CloudTrail: Tạo Trail, đẩy log về S3 Bucket | 17/06/2026 | 17/06/2026 | AWS CloudTrail |
| 4 | - Tạo Kinesis Firehose stream, cấu hình Source → Transform (Lambda) → S3 | 18/06/2026 | 18/06/2026 | AWS Kinesis Docs |
| 5 | - Viết hàm Lambda `my-log-filter` (Node.js): Giải mã Base64, lọc CONTROL_MESSAGE | 19/06/2026 | 19/06/2026 | AWS Lambda Docs |
| 6 | - Kích hoạt Amazon GuardDuty, review các Finding mẫu | 20/06/2026 | 20/06/2026 | AWS GuardDuty |

### Kết quả đạt được:

* Data Pipeline hoạt động: VPC Flow Logs → CloudWatch → Kinesis Firehose → Lambda → S3.
* Hàm Lambda my-log-filter xử lý thành công: Lọc bỏ Control Message, giữ lại Data Message dạng JSON.
* GuardDuty đã phát hiện cảnh báo khi dùng Root credentials gọi API (test thành công).
