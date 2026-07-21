---
title: "Blog 3: Giám sát an ninh đám mây tự động bằng Amazon GuardDuty"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

### Tầm quan trọng của An ninh Đám mây
Trong quá trình triển khai dự án, tôi nhận ra rằng việc chỉ lưu trữ Log là chưa đủ. Các kỹ sư hệ thống cần được cảnh báo ngay lập tức nếu có ai đó đang cố gắng thâm nhập vào tài khoản AWS của họ.

### Sức mạnh của Amazon GuardDuty
Tôi đã cấu hình **Amazon GuardDuty** - một dịch vụ phát hiện mối đe dọa sử dụng Trí tuệ nhân tạo (AI) và Machine Learning. GuardDuty liên tục phân tích VPC Flow Logs và CloudTrail để tìm kiếm các dấu hiệu bất thường.
Trong một kịch bản kiểm thử, tôi đã cố tình sử dụng thông tin xác thực Root (Root credentials) để gọi API GetCostAndUsage. Gần như ngay lập tức, GuardDuty đã phát hiện và tạo ra một cảnh báo (Finding):
> "The API GetCostAndUsage was invoked using root credentials."

### Bài học rút ra
Việc sử dụng tài khoản Root cho các tác vụ hàng ngày là một lỗ hổng bảo mật cực kỳ nghiêm trọng. Qua dự án này, tôi đã áp dụng nguyên tắc **Quyền tối thiểu (Principle of Least Privilege)**: chỉ tạo các IAM User cụ thể, gán cho họ đúng những quyền cần thiết thay vì dùng quyền Root. GuardDuty đóng vai trò như một người bảo vệ thầm lặng, giúp đảm bảo toàn bộ hệ thống AWS luôn an toàn 24/7.
