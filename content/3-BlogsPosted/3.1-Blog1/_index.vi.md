---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AI có thể tự kiểm thử game với Amazon Bedrock – Điều mình học được sau khi đọc AWS Blog

Xin chào mọi người,

Trong quá trình tìm hiểu về AWS, mình thường đọc các bài viết trên **AWS GameTech Blog** để xem các doanh nghiệp đang ứng dụng dịch vụ AWS như thế nào vào những bài toán thực tế. Gần đây mình đọc được bài viết ["Building an AI game testing agent with Amazon Bedrock"](https://aws.amazon.com/vi/blogs/gametech/building-an-ai-game-testing-agent-with-amazon-bedrock/) và thấy đây là một chủ đề khá thú vị, đặc biệt với những ai đang quan tâm đến Generative AI hoặc AI Agent.

Ban đầu mình nghĩ bài viết sẽ chủ yếu giới thiệu về Amazon Bedrock hoặc các mô hình AI mà AWS đang cung cấp. Nhưng sau khi đọc xong, điều mình thấy giá trị nhất lại không nằm ở công nghệ riêng lẻ mà là cách AWS kết hợp AI với quy trình kiểm thử game để tự động hóa một công việc vốn rất tốn thời gian.
![Blog 1](/images/Blog/blog1.jpg)
### Kiểm thử game không chỉ đơn giản là "chơi game"

Trước khi đọc bài viết này, mình từng nghĩ kiểm thử game chủ yếu là vào game chơi thử rồi tìm lỗi. Nhưng thực tế công việc của đội ngũ QA phức tạp hơn rất nhiều. Sau mỗi lần game được cập nhật, họ phải thực hiện lại rất nhiều thao tác như di chuyển đến từng khu vực, nói chuyện với NPC, hoàn thành nhiệm vụ, kiểm tra điều kiện kích hoạt các sự kiện rồi xác nhận xem mọi thứ có hoạt động đúng như thiết kế hay không.

Khi quy mô của game ngày càng lớn thì lượng kịch bản cần kiểm thử cũng tăng theo. Việc thực hiện toàn bộ các bước này bằng con người không chỉ mất nhiều thời gian mà còn rất dễ bỏ sót lỗi. Đó cũng là bài toán mà nhóm phát triển trong bài viết muốn giải quyết.

### Giải pháp: Xây dựng AI Game Testing Agent với Amazon Bedrock

Điều mình thích ở bài viết là nhóm phát triển không đơn giản đưa AI vào để "chơi game". **Amazon Bedrock** được sử dụng như bộ não của hệ thống, giúp AI hiểu mục tiêu cần hoàn thành rồi tự lên kế hoạch cho từng hành động tiếp theo.

Sau mỗi bước thực hiện, AI sẽ quan sát kết quả trong game, đánh giá xem mục tiêu đã đạt được hay chưa rồi tiếp tục đưa ra quyết định tiếp theo. Toàn bộ quá trình này diễn ra giống như cách một tester thật đang kiểm tra game thay vì chỉ thực hiện những lệnh được lập trình sẵn.

Qua ví dụ này mình hiểu rõ hơn khái niệm **AI Agent** mà AWS đang nhắc đến trong thời gian gần đây. AI không chỉ tạo ra câu trả lời mà còn có khả năng lập kế hoạch, suy luận và hoàn thành một chuỗi công việc.

### Điều mình ấn tượng nhất là cách AI phối hợp với hệ thống

Điểm mình thấy đáng học nhất của bài viết là **Amazon Bedrock không trực tiếp điều khiển game.**

Game Engine vẫn hoạt động bình thường, còn AI chỉ giao tiếp thông qua các API hoặc các công cụ mà đội ngũ phát triển xây dựng sẵn. Điều này giúp mỗi thành phần có một nhiệm vụ riêng: AI chịu trách nhiệm suy luận và ra quyết định, trong khi game vẫn đảm nhận việc xử lý gameplay.

Theo mình, đây là một cách thiết kế rất hợp lý vì sau này nếu muốn thay đổi mô hình AI hoặc mở rộng thêm tính năng thì cũng không cần sửa toàn bộ hệ thống game. Đây cũng là lần đầu tiên mình hình dung rõ hơn về mô hình **AI Agent + Tool Use** mà AWS đang phát triển.

### AI Agent không chỉ dành cho ngành game

Đọc xong bài viết mình nhận ra kiến trúc này hoàn toàn có thể áp dụng sang nhiều lĩnh vực khác. Nếu một AI Agent có thể tự chơi game để kiểm thử thì về bản chất nó cũng có thể tự động kiểm thử website, ứng dụng di động hoặc phần mềm doanh nghiệp. Chỉ cần thay đổi bộ công cụ mà AI được phép sử dụng thì quy trình làm việc vẫn gần như giữ nguyên.

Điều này cho thấy AI Agent không phải là một giải pháp dành riêng cho GameTech mà hoàn toàn có thể trở thành một phần trong quá trình tự động hóa của rất nhiều doanh nghiệp.

### Góc nhìn cá nhân

Sau khi đọc xong bài blog, mình nhận ra giá trị lớn nhất của Generative AI không nằm ở việc trả lời câu hỏi hay tạo nội dung, mà nằm ở khả năng phối hợp với các hệ thống hiện có để thực hiện những công việc thực tế.

Amazon Bedrock trong bài viết không chỉ cung cấp một mô hình AI mà còn đóng vai trò là nền tảng để xây dựng những AI Agent có thể lập kế hoạch, sử dụng công cụ và tự hoàn thành nhiệm vụ. Đây là điểm khiến mình thấy khác biệt so với cách nhiều người vẫn nghĩ về AI hiện nay.

Bài viết cũng giúp mình hiểu rõ hơn rằng khi xây dựng một hệ thống AI, điều quan trọng không chỉ là lựa chọn mô hình mạnh nhất mà còn là cách thiết kế kiến trúc để AI có thể tương tác với các dịch vụ và ứng dụng khác trong toàn bộ hệ thống.

### Kết luận

Đối với mình, đây không đơn thuần là một bài viết giới thiệu Amazon Bedrock mà là một ví dụ rất thực tế về cách AWS ứng dụng Generative AI để giải quyết một bài toán trong quá trình phát triển game.

Qua bài viết, mình hiểu rõ hơn về cách AI Agent hoạt động, cách Amazon Bedrock phối hợp với các công cụ khác và tư duy thiết kế một hệ thống AI có khả năng tự động thực hiện công việc. Nếu mọi người đang tìm hiểu về Amazon Bedrock, Generative AI hoặc AI Agent trên AWS, mình nghĩ đây là một bài viết rất đáng đọc vì nó cho thấy cách công nghệ này được ứng dụng trong thực tế chứ không chỉ dừng lại ở lý thuyết.

**Link bài viết gốc:** <https://www.facebook.com/groups/awsstudygroupfcj/permalink/2209936013104692/?rdid=YKexzZWKzXL0I33t>