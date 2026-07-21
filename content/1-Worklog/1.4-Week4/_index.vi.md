---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 31
chapter: false
pre: " <b> 1.4.4. </b> "
---

### Mục tiêu tuần 4:

* Khởi tạo dự án Backend: Node.js + Express + MongoDB.
* Thiết kế Database Schema cho MongoDB (User, Alert, TrafficLog).
* Xây dựng hệ thống Authentication (JWT) và Role-Based Access Control (RBAC).

### Các công việc đã triển khai trong tuần:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Khởi tạo dự án Node.js, cài đặt Express, Mongoose, bcryptjs, jsonwebtoken | 12/05/2026 | 12/05/2026 | npm |
| 3 | - Thiết kế 3 MongoDB Schema: User, Alert, TrafficLog | 13/05/2026 | 13/05/2026 | Mongoose Docs |
| 4 | - Code API đăng nhập: POST /api/auth/login với JWT Token | 14/05/2026 | 14/05/2026 | JWT.io |
| 5 | - Xây dựng middleware phân quyền: verifyToken, checkRole | 15/05/2026 | 15/05/2026 | |
| 6 | - Thiết kế 4 vai trò (NetAdmin, SecOps, Manager, SystemAdmin) và test RBAC | 16/05/2026 | 16/05/2026 | |

### Kết quả đạt được:

* Backend server hoạt động tại http://localhost:5000, kết nối MongoDB (database: aws_monitor) thành công.
* Hệ thống JWT Authentication hoàn chỉnh: Đăng nhập → Nhận Token → Gửi Token ở Header cho mọi API.
* RBAC hoạt động: Chỉ SecOps và SystemAdmin mới được phép thay đổi trạng thái cảnh báo bảo mật.
