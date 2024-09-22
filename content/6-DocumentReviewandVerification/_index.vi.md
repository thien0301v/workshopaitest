---
title : "Xem xét và Xác minh Tài liệu"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
---
### Overview
**Amazon Augmented AI (Amazon A2I)** giúp đơn giản hóa việc xây dựng các quy trình làm việc cần thiết cho việc xem xét dự đoán của máy học (ML) bởi con người. Amazon A2I mang đến sự xem xét của con người cho tất cả các nhà phát triển, loại bỏ những công việc nặng nề không phân biệt liên quan đến việc xây dựng hệ thống xem xét con người hoặc quản lý số lượng lớn người đánh giá.

Amazon A2I cung cấp các quy trình làm việc xem xét con người tích hợp cho các trường hợp sử dụng máy học phổ biến, chẳng hạn như quản lý nội dung và trích xuất văn bản từ tài liệu, giúp dễ dàng xem xét các dự đoán từ Amazon Rekognition và Amazon Textract. Bạn cũng có thể tạo các quy trình làm việc của riêng mình cho các mô hình máy học được xây dựng trên Amazon SageMaker hoặc bất kỳ công cụ nào khác. Sử dụng Amazon A2I, bạn có thể cho phép người đánh giá can thiệp khi một mô hình không thể đưa ra dự đoán với độ tin cậy cao hoặc để kiểm tra dự đoán của nó một cách liên tục.

### Tài nguyên cần thiết cho A2I
Để tích hợp Amazon A2I vào quy trình làm việc xem xét con người của bạn, bạn cần ba tài nguyên. Mở rộng các phần dưới đây để tìm hiểu thêm về từng tài nguyên.
#### Worker task template
A **worker task template** để tạo giao diện người dùng cho người lao động. Giao diện người lao động hiển thị dữ liệu đầu vào của bạn, chẳng hạn như tài liệu hoặc hình ảnh, và hướng dẫn cho người lao động. Nó cũng cung cấp các công cụ tương tác mà người lao động sử dụng để hoàn thành nhiệm vụ của bạn.
#### Human review workflow
A **human review workflow**, còn được gọi là định nghĩa luồng. Bạn sử dụng định nghĩa luồng để cấu hình lực lượng lao động con người của mình và cung cấp thông tin về cách thực hiện nhiệm vụ xem xét con người. Đối với các loại nhiệm vụ tích hợp sẵn, bạn cũng sử dụng định nghĩa luồng để xác định các điều kiện mà vòng lặp xem xét con người được kích hoạt. Ví dụ, với Amazon Textract, có thể phân tích văn bản trong một tài liệu bằng cách sử dụng máy học. Bạn có thể sử dụng định nghĩa luồng để chỉ định rằng một tài liệu sẽ được gửi cho một người để xem xét quản lý nội dung nếu điểm số tin cậy của đầu ra từ Amazon Textract thấp cho bất kỳ hoặc tất cả các phần văn bản được trả về bởi Textract. Bạn có thể tạo định nghĩa luồng trong bảng điều khiển Amazon Augmented AI hoặc với các API **Amazon A2I**.
#### Human loop
A **human loop** để bắt đầu quy trình làm việc xem xét con người của bạn. Khi bạn sử dụng một trong các loại nhiệm vụ tích hợp sẵn, dịch vụ AWS tương ứng sẽ tạo và bắt đầu một vòng lặp con người thay mặt bạn khi các điều kiện được chỉ định trong định nghĩa luồng của bạn được đáp ứng hoặc cho mỗi đối tượng nếu không có điều kiện nào được chỉ định. Khi một vòng lặp con người được kích hoạt, các nhiệm vụ xem xét con người sẽ được gửi đến người lao động như đã chỉ định trong định nghĩa luồng.

Khi sử dụng một loại nhiệm vụ tùy chỉnh, bạn bắt đầu một vòng lặp con người bằng cách sử dụng API **Amazon Augmented AI Runtime**. Khi bạn gọi StartHumanLoop trong ứng dụng tùy chỉnh của mình, một nhiệm vụ sẽ được gửi đến những người đánh giá con người.
