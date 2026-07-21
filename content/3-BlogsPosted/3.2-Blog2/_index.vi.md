---
title: "Blog 2: Truy vấn dữ liệu Serverless với Amazon Athena và hiển thị lên Web App"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

### Bối cảnh
Sau khi có một kho S3 Data Lake chứa đầy các file log JSON (như đã chia sẻ ở Blog 1), làm sao để hệ thống Backend Node.js có thể lấy được danh sách Top 5 IP đang có dấu hiệu bất thường (bị REJECT liên tục)?

### Giải pháp với Amazon Athena
Thay vì phải cài đặt và vận hành một hệ thống SQL Server hay Elasticsearch đắt đỏ, tôi sử dụng **Amazon Athena**. 
Athena là dịch vụ Serverless cho phép chạy trực tiếp các câu lệnh SQL trên các file tĩnh lưu ở S3.
SELECT srcAddr, COUNT(*) as hit_count FROM vpc_flow_logs WHERE action = 'REJECT' GROUP BY srcAddr ORDER BY hit_count DESC LIMIT 5;

### Tích hợp vào hệ thống MERN Stack
Trong kiến trúc Lai (Hybrid) của dự án, Frontend React của tôi sẽ hiển thị giao diện SOC Dashboard đẹp mắt. Khi người dùng muốn xem báo cáo an ninh, Backend Node.js sẽ dùng aws-sdk để gửi câu query SQL lên Athena.
Athena sẽ tính toán dựa trên lượng dữ liệu quét (Data Scanned) - thường chỉ tốn chưa tới $0.01 cho mỗi lần query. Kết quả sau đó được trả về Backend và hiển thị lên React.
Sự kết hợp giữa Web App truyền thống và AWS Analytics đã mang lại một sức mạnh đáng kinh ngạc cho hệ thống!
