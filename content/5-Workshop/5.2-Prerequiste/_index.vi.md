---
title: "2. Điều kiện tiên quyết (Prerequisites)"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

Để thực hiện Workshop này, bạn cần chuẩn bị các công cụ và tài nguyên sau:

### 1. Tài khoản AWS & IAM User
Tuyệt đối **KHÔNG** sử dụng tài khoản Root để thực hành. (Như bạn đã thấy ở cảnh báo GuardDuty trong các bước sau, việc dùng Root để gọi API sẽ bị đánh dấu là rủi ro bảo mật).

**Các bước tạo IAM User hợp lý:**
1. Đăng nhập vào AWS bằng tài khoản Root, mở **IAM Console** -> **Users** -> **Create user**.
2. Đặt tên User (Ví dụ: `huynhtuan1`) và chọn **Provide user access to the AWS Management Console**.
3. Ở phần Set permissions, chọn **Attach policies directly** và cấp quyền `AdministratorAccess`.
4. Hoàn tất tạo User, copy mật khẩu và URL đăng nhập.
5. Đăng xuất tài khoản Root và **đăng nhập lại bằng IAM User vừa tạo**.

* Chọn Region: `us-east-1` (N. Virginia) hoặc `ap-southeast-1` (Singapore) cho toàn bộ bài Lab.

![Tạo IAM User](/images/Workshop/iam_user.jpg)

### 2. Công cụ
* Trình duyệt web (Chrome/Firefox).
* [AWS CLI](https://aws.amazon.com/cli/) đã được cài đặt và cấu hình bằng lệnh `aws configure` (sử dụng Access Key của IAM User vừa tạo).
* (Tùy chọn) Môi trường **AWS Cloud9** để chạy code.

*(Lưu ý: Đối với IAM Role của Lambda hoặc các dịch vụ khác, trong Workshop này chúng ta sẽ sử dụng cơ chế tạo Role tự động của AWS Console để tiết kiệm thời gian triển khai).*
