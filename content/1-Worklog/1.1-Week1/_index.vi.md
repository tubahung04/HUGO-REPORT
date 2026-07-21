---
title: "Worklog Tuần 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Làm quen với các thành viên trong First Cloud AI Journey (FCAJ) và nắm rõ nội quy chương trình thực tập.
* Xây dựng nền tảng vững chắc về các dịch vụ AWS cốt lõi: tạo tài khoản, quản lý chi phí, IAM và VPC, EC2.

### Các công việc đã triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                       | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                 |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------- |
| Thứ 2 | - Giới thiệu bản thân với các thành viên FCAJ <br> - Đọc nội quy và các quy định của chương trình thực tập                                                  | 20/04/2026   | 20/04/2026      |                                                                                   |
| Thứ 3 | - Tạo **Tài khoản AWS** đầu tiên <br> - Tìm hiểu cách quản lý mức chi phí sử dụng với **AWS Budgets** <br> - Tìm hiểu cách yêu cầu hỗ trợ qua **AWS Support** | 21/04/2026   | 21/04/2026      | <https://cloudjourney.awsstudygroup.com/vi/1-explore/>                          |
| Thứ 4 | - Tìm hiểu **AWS Identity and Access Management (IAM)**: users, groups, policies và nguyên tắc least-privilege                                              | 22/04/2026   | 22/04/2026      | <https://000002.awsstudygroup.com/vi/>                                          |
| Thứ 5 | - Tìm hiểu **Amazon VPC**: subnet, route table, internet gateway và các mẫu thiết kế mạng cơ bản                                                            | 23/04/2026   | 23/04/2026      | <https://000003.awsstudygroup.com/vi/>                                          |
| Thứ 6 | - **Thực hành:** Khởi tạo và triển khai ứng dụng trên **Amazon EC2** <br> - Tìm hiểu cách cấp quyền cho ứng dụng truy cập dịch vụ AWS thông qua **IAM Role**  | 24/04/2026   | 24/04/2026      | <https://000004.awsstudygroup.com/vi/> <br> <https://000048.awsstudygroup.com/vi/> |


### Kết quả đạt được tuần 1:

* Tạo và cấu hình thành công tài khoản AWS đầu tiên, bao gồm cả các thiết lập bảo mật cho root user.
* Hiểu được cách theo dõi, kiểm soát chi phí hàng tháng bằng **AWS Budgets**, và cách gửi yêu cầu hỗ trợ qua **AWS Support**.
* Nắm được kiến thức nền tảng về **IAM**: tạo user/group, gắn policy và áp dụng nguyên tắc least-privilege.
* Hiểu rõ các thành phần của **Amazon VPC** (subnet, route table, internet gateway) và vai trò của chúng trong việc xây dựng nền tảng mạng cho các workload trên AWS.
* Thực hành khởi tạo **EC2 instance**, kết nối và triển khai một ứng dụng đơn giản.
* Hiểu được cách **IAM Role** cho phép ứng dụng chạy trên EC2 truy cập an toàn vào các dịch vụ AWS khác mà không cần lưu trữ credentials trực tiếp.
* Có được bức tranh rõ ràng hơn về cách tài khoản, identity, network và compute trên AWS kết nối với nhau, tạo thành nền tảng cho bất kỳ kiến trúc cloud nào.