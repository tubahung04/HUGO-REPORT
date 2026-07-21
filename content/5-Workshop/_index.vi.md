---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Thực hành: Xây dựng SOC Dashboard kết hợp MERN Stack và AWS Data Pipeline

Workshop này trình bày chi tiết quá trình tôi **tự tay xây dựng** một hệ thống giám sát an ninh mạng (SOC - Security Operations Center) hoàn chỉnh. Hệ thống kết hợp giữa:

* **Web App MERN Stack** (MongoDB, Express, React, Node.js): Xây dựng giao diện Dashboard, hệ thống phân quyền (4 vai trò), quản lý cảnh báo bảo mật.
* **AWS Serverless Data Pipeline** (9 dịch vụ): Thu thập, xử lý và phân tích dữ liệu log mạng quy mô lớn.

Mục tiêu của dự án: Chứng minh khả năng thiết kế một kiến trúc Lai (Hybrid) nơi Web App truyền thống và Cloud Serverless hỗ trợ lẫn nhau.

1. [Tổng quan & Kiến trúc](5.1-Workshop-overview/)
2. [Điều kiện tiên quyết](5.2-Prerequiste/)
3. [Xây dựng Web App - MERN Stack](5.3-Logging/)
4. [Cấu hình AWS Data Pipeline](5.4-DataPipeline/)
5. [Phân tích & Giám sát bảo mật](5.5-Analytics/)
6. [Tích hợp AWS vào Web App](5.6-WebIntegration/)
7. [Dọn dẹp tài nguyên](5.7-Cleanup/)
