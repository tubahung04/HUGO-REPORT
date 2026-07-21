---
title: "Blog 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Tạo tài nguyên 3D cho game bằng AI mã nguồn mở trên AWS – Điều mình học được sau khi đọc AWS Blog

Xin chào mọi người,

Trong quá trình tìm hiểu về AWS, mình thường đọc các bài viết trên **AWS GameTech Blog** để xem các doanh nghiệp đang ứng dụng Cloud vào quy trình phát triển game như thế nào. Gần đây mình đọc được bài viết ["Open-source 3D game asset generation using AWS"](https://aws.amazon.com/vi/blogs/gametech/open-source-3d-game-asset-generation-using-aws/) và thấy đây là một chủ đề khá thú vị, đặc biệt với những ai quan tâm đến Generative AI hoặc phát triển game.

Ban đầu mình nghĩ bài viết sẽ chủ yếu giới thiệu một vài mô hình AI tạo hình ảnh 3D. Tuy nhiên, sau khi đọc xong mình nhận ra điều tác giả muốn nhấn mạnh không phải là từng mô hình AI riêng lẻ, mà là cách kết hợp các công nghệ mã nguồn mở với hạ tầng AWS để xây dựng một quy trình tạo tài nguyên 3D nhanh hơn, linh hoạt hơn và tiết kiệm chi phí hơn.
![Blog 2](/images/Blog/blog2.jpg)
### Tạo tài nguyên 3D vẫn là một trong những công đoạn tốn nhiều thời gian

Điều mình thấy thú vị đầu tiên là bài viết nhắc đến một vấn đề mà hầu như studio game nào cũng gặp phải. Việc xây dựng các mô hình 3D cho nhân vật, vũ khí hay vật thể trong game thường mất rất nhiều thời gian và đòi hỏi đội ngũ artist có kinh nghiệm.

Thông thường, quá trình này phải trải qua nhiều bước từ lên ý tưởng, tạo hình, chỉnh sửa, tối ưu mô hình cho đến khi có thể đưa vào game. Với các dự án lớn, số lượng asset cần tạo có thể lên đến hàng nghìn mô hình nên đây là công đoạn tiêu tốn rất nhiều nguồn lực.

Chính vì vậy, việc ứng dụng AI để hỗ trợ tạo asset đang trở thành xu hướng được nhiều studio quan tâm.

### Giải pháp: Kết hợp AI mã nguồn mở với hạ tầng AWS

Điều mình thích ở bài viết là AWS không giới thiệu một dịch vụ độc quyền để tạo mô hình 3D. Thay vào đó, bài viết hướng dẫn cách triển khai các mô hình AI mã nguồn mở trên AWS để xây dựng một pipeline tạo asset hoàn chỉnh.

Thay vì phải tự đầu tư hạ tầng GPU, người phát triển có thể sử dụng các dịch vụ tính toán của AWS để triển khai mô hình AI, sinh ra mô hình 3D từ dữ liệu đầu vào, sau đó tiếp tục chỉnh sửa và tối ưu trước khi đưa vào game. Nhờ đó, toàn bộ quy trình trở nên linh hoạt hơn và dễ mở rộng khi nhu cầu xử lý tăng lên.

### AI hỗ trợ artist thay vì thay thế artist

Một điểm mình khá thích là bài viết không hề nói AI sẽ thay thế người thiết kế. Ngược lại, AWS nhấn mạnh rằng AI chỉ giúp rút ngắn những công đoạn lặp đi lặp lại hoặc tạo ra bản nháp ban đầu để artist tiếp tục hoàn thiện.

Điều này giúp đội ngũ thiết kế dành nhiều thời gian hơn cho việc sáng tạo, tinh chỉnh chi tiết và xây dựng phong cách nghệ thuật riêng của trò chơi thay vì mất hàng giờ cho những thao tác thủ công. Theo mình, đây cũng là hướng ứng dụng AI thực tế nhất hiện nay: AI đóng vai trò hỗ trợ để tăng năng suất chứ không thay thế hoàn toàn con người.

### AWS giúp mở rộng quy trình tạo asset dễ dàng hơn

Một điều mình học được từ bài viết là khi kết hợp AI với Cloud, khả năng mở rộng trở nên đơn giản hơn rất nhiều. Nếu số lượng asset cần tạo tăng lên, nhóm phát triển chỉ cần mở rộng tài nguyên tính toán trên AWS thay vì phải đầu tư thêm máy chủ vật lý hoặc GPU mới.

Bên cạnh đó, việc sử dụng các mô hình mã nguồn mở cũng giúp doanh nghiệp chủ động lựa chọn công nghệ phù hợp với nhu cầu của mình mà không bị phụ thuộc vào một nền tảng duy nhất. Theo mình, đây là một lợi thế khá lớn khi xây dựng các hệ thống AI phục vụ sản xuất nội dung.

### Một ví dụ thực tế về Generative AI trong Game Development

Điều mình thích ở bài viết là AWS không chỉ giới thiệu các mô hình AI mà còn cho thấy cách kết hợp nhiều thành phần để xây dựng một quy trình hoàn chỉnh.

Qua bài viết, mình hiểu rõ hơn rằng Generative AI không chỉ dùng để tạo văn bản hay hình ảnh mà còn có thể hỗ trợ tạo ra các mô hình 3D phục vụ phát triển game. Khi được triển khai trên AWS, toàn bộ quy trình từ xử lý dữ liệu, chạy mô hình AI đến tạo asset đều có thể được tự động hóa và mở rộng theo nhu cầu của dự án.

### Góc nhìn cá nhân

Sau khi đọc xong bài blog, mình nhận ra rằng Generative AI đang dần thay đổi quy trình phát triển game theo hướng hỗ trợ con người nhiều hơn thay vì thay thế hoàn toàn.

Điều mình học được không phải là cách sử dụng một mô hình AI cụ thể mà là tư duy xây dựng một pipeline, trong đó AI đảm nhận những phần việc lặp đi lặp lại, còn con người tập trung vào sáng tạo và kiểm soát chất lượng. Bài viết cũng giúp mình hiểu rõ hơn vai trò của AWS trong việc cung cấp hạ tầng để triển khai các mô hình AI mã nguồn mở. Nhờ khả năng mở rộng linh hoạt và hệ sinh thái dịch vụ đa dạng, AWS giúp việc ứng dụng Generative AI vào quy trình phát triển game trở nên thực tế và dễ triển khai hơn.

### Kết luận

Đối với mình, đây không chỉ là một bài viết về AI tạo mô hình 3D mà còn là một ví dụ thực tế về cách AWS hỗ trợ các studio game xây dựng quy trình sản xuất nội dung hiện đại.

Nếu mọi người đang tìm hiểu về AWS, Generative AI, hoặc cách ứng dụng AI mã nguồn mở trong phát triển game, mình nghĩ đây là một bài viết rất đáng đọc. Nó không chỉ giới thiệu công nghệ mà còn mang đến góc nhìn thực tế về cách kết hợp AI với Cloud để tối ưu quy trình làm việc, tăng năng suất và vẫn giữ được vai trò quan trọng của con người trong quá trình sáng tạo.

**Link bài viết:** <https://www.facebook.com/groups/awsstudygroupfcj/permalink/2209938356437791/?rdid=qsIJDHyGiMQbo6DE#>