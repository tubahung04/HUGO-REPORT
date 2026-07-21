---
title: "Blog 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Hypermonk Games và cách xây dựng nền tảng phân tích dữ liệu game trên AWS – Điều mình học được sau khi đọc AWS Blog

Xin chào mọi người,

Trong quá trình tìm hiểu về AWS, mình thường đọc các bài viết trên **AWS GameTech Blog** để hiểu cách các doanh nghiệp ứng dụng dịch vụ AWS vào những bài toán thực tế. Gần đây mình đọc được bài viết ["Hypermonk Games transforms mobile game development with data powered by AWS"](https://aws.amazon.com/blogs/gametech/hypermonk-games-transforms-mobile-game-development-with-data-powered-by-aws/) và thấy đây là một bài viết khá đáng tham khảo đối với những bạn quan tâm đến kiến trúc dữ liệu (Data Architecture) hoặc phát triển game trên nền tảng Cloud.

Ban đầu mình nghĩ bài viết sẽ chỉ giới thiệu các dịch vụ AWS mà Hypermonk Games sử dụng. Tuy nhiên, sau khi đọc xong, mình nhận ra điều tác giả muốn nhấn mạnh không phải là từng dịch vụ riêng lẻ, mà là cách kết hợp chúng để xây dựng một hệ thống phân tích dữ liệu hoàn chỉnh, giúp đội ngũ phát triển đưa ra quyết định dựa trên dữ liệu thay vì cảm tính.
![Blog 3](/images/Blog/blog3.jpg)

### Dữ liệu người chơi – Tài sản quan trọng của một tựa game

Điều mình ấn tượng đầu tiên là cách Hypermonk Games xem dữ liệu người chơi như một tài sản quan trọng. Mỗi hành động của người chơi như bắt đầu màn chơi, hoàn thành nhiệm vụ, xem quảng cáo hay mua vật phẩm đều tạo ra dữ liệu có giá trị.

Nếu không có một hệ thống thu thập và phân tích phù hợp, lượng dữ liệu này sẽ rất khó khai thác. Việc tìm hiểu hành vi người chơi, đánh giá hiệu quả của các sự kiện trong game hoặc tối ưu doanh thu sẽ mất rất nhiều thời gian và dễ đưa ra những quyết định thiếu chính xác.

### Giải pháp: Xây dựng nền tảng phân tích dữ liệu trên AWS

Điều mình thấy thú vị là Hypermonk Games đã xây dựng một nền tảng nội bộ mang tên **Orange** dựa trên các dịch vụ AWS.

Dữ liệu từ game được gửi theo thời gian thực thông qua **Amazon Kinesis**, sau đó được xử lý bằng **AWS Lambda** trước khi lưu vào **Amazon S3** và **Amazon DynamoDB**. Các dịch vụ như **Amazon Athena**, **Amazon EventBridge** và **Amazon SQS** được sử dụng để truy vấn dữ liệu, điều phối sự kiện và xử lý các tác vụ bất đồng bộ.

Nhờ kiến trúc này, đội ngũ phát triển có thể theo dõi hành vi người chơi gần như theo thời gian thực, dễ dàng thực hiện A/B Testing, đánh giá hiệu quả của các chiến dịch quảng cáo cũng như tối ưu trải nghiệm trong game.

### Tự động hóa giúp tối ưu vận hành và giảm chi phí

Theo mình, điểm hay của bài viết không chỉ nằm ở khả năng thu thập dữ liệu mà còn ở cách Hypermonk Games tối ưu hệ thống sau khi đưa vào vận hành.

Bài viết chia sẻ rằng họ đã áp dụng các chính sách lưu trữ trên **Amazon S3** để giảm đáng kể chi phí lưu trữ dữ liệu lâu dài, đồng thời điều chỉnh cấu hình **Amazon DynamoDB** dựa trên lưu lượng sử dụng thực tế để tối ưu chi phí vận hành.

Điều này cho thấy khi xây dựng hệ thống trên Cloud, việc tối ưu chi phí cũng quan trọng không kém việc xây dựng được một kiến trúc hoạt động ổn định.

### Một ví dụ thực tế về kiến trúc dữ liệu trên AWS

Một điều mình thích ở bài viết là tác giả không chỉ giới thiệu từng dịch vụ AWS riêng lẻ mà còn cho thấy cách kết hợp nhiều dịch vụ để tạo thành một hệ thống hoàn chỉnh.

Qua bài viết, mình hiểu rõ hơn cách các thành phần như **Amazon Kinesis**, **AWS Lambda**, **Amazon S3**, **Amazon Athena**, **Amazon DynamoDB**, **Amazon EventBridge** và **Amazon SQS** phối hợp với nhau để xây dựng một pipeline dữ liệu có khả năng mở rộng, đáp ứng lượng lớn sự kiện phát sinh từ game.

### Góc nhìn cá nhân

Sau khi đọc xong bài blog, mình nhận ra rằng dữ liệu không chỉ phục vụ cho việc thống kê mà còn đóng vai trò quan trọng trong quá trình phát triển sản phẩm.

Thay vì đưa ra quyết định dựa trên cảm nhận, các nhà phát triển có thể dựa vào dữ liệu thực tế để tối ưu gameplay, cải thiện trải nghiệm người chơi và nâng cao hiệu quả kinh doanh. Bài viết cũng giúp mình hiểu rõ hơn về cách AWS hỗ trợ doanh nghiệp xây dựng các hệ thống phân tích dữ liệu có khả năng mở rộng và tối ưu chi phí.

### Kết luận

Đối với mình, bài viết này không chỉ giới thiệu cách Hypermonk Games sử dụng AWS mà còn mang đến góc nhìn thực tế về việc xây dựng một nền tảng dữ liệu phục vụ phát triển game hiện đại.

Nếu mọi người đang tìm hiểu về AWS, Data Engineering hoặc các kiến trúc xử lý dữ liệu theo thời gian thực, mình nghĩ đây là một bài viết rất đáng đọc. Cảm ơn mọi người đã dành thời gian đọc bài chia sẻ của mình. Nếu anh/chị hoặc các bạn đã từng xây dựng hệ thống phân tích dữ liệu trên AWS hoặc có kinh nghiệm về Data Pipeline, mình rất mong được lắng nghe thêm những chia sẻ từ mọi người.

**Link bài viết gốc:** <https://www.facebook.com/groups/awsstudygroupfcj/permalink/2209746196457007/?rdid=5qxZq6kRlOs3vf1O#>