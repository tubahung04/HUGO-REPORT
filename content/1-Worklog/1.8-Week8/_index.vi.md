---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 71
chapter: false
pre: " <b> 1.8.8. </b> "
---

### Mục tiêu tuần 8:

* Code component: AttackMap (bản đồ tấn công toàn cầu) và TopIPConsole.
* Hoàn thiện giao diện 3 tab (Dashboard, Security, Traffic) trên App.jsx.
* Tối ưu UI/UX: micro-animation, responsive layout.

### Các công việc đã triển khai trong tuần:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Code AttackMap.jsx (bản đồ hiển thị vị trí IP tấn công theo geo_location) | 09/06/2026 | 09/06/2026 | |
| 3 | - Code TopIPConsole.jsx (Top 10 IP, lọc theo protocol, hiệu ứng terminal) | 10/06/2026 | 10/06/2026 | |
| 4 | - Xây dựng App.jsx: Router, 3 tab, ProtectedRoute component | 11/06/2026 | 11/06/2026 | React Router |
| 5 | - Thêm micro-animation (fade-in, slide-in), hiệu ứng blur gradient nền | 12/06/2026 | 12/06/2026 | TailwindCSS |
| 6 | - Test toàn bộ Web App E2E: Login → Dashboard → Security → Traffic | 13/06/2026 | 13/06/2026 | |

### Kết quả đạt được:

* Hoàn thành toàn bộ 9 React Components cho SOC Dashboard.
* AttackMap hiển thị vị trí tấn công từ 6 quốc gia (China, UK, Russia, USA, Brazil, Australia).
* TopIPConsole hỗ trợ lọc theo giao thức (ALL, TCP, HTTP, UDP, ICMP) với giao diện terminal-style.
* Web App hoạt động hoàn chỉnh End-to-End.
