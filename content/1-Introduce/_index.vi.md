---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false

---

### **Tổng quan**
Sơ đồ kiến trúc dưới đây hiển thị các giai đoạn của quy trình xử lý tài liệu thông minh. Nó bắt đầu với giai đoạn thu thập dữ liệu để lưu trữ an toàn và tổng hợp các loại tài liệu khác nhau (pdf, jpeg, png, tiff), định dạng và bố cục. Giai đoạn tiếp theo là phân loại, đây là nơi bạn phân loại các tài liệu của mình (ví dụ như hợp đồng, biểu mẫu yêu cầu bồi thường, hóa đơn, biên lai, v.v.) tiếp theo là trích xuất tài liệu. Trong giai đoạn trích xuất, bạn có thể trích xuất thông tin kinh doanh có ý nghĩa từ các tài liệu của mình. Dữ liệu được trích xuất này thường được sử dụng để thu thập thông tin qua phân tích dữ liệu, hoặc gửi tới các hệ thống hạ nguồn như cơ sở dữ liệu hoặc hệ thống giao dịch. Giai đoạn tiếp theo là làm giàu dữ liệu, tại giai đoạn này, các tài liệu có thể được làm giàu bằng cách xóa dữ liệu PII, trích xuất các thuật ngữ tùy chỉnh trong doanh nghiệp, v.v. Cuối cùng, trong giai đoạn đánh giá/xác minh, bạn có thể đưa thêm lực lượng lao động con người để đánh giá tài liệu nhằm đảm bảo kết quả chính xác.
 ![s1](/images/2.prerequisite/idp_arc_2.png)

### Trước khi bắt đầu
Hãy xem qua một cái nhìn tổng quan ngắn gọn về **Amazon Textract**, **Amazon Comprehend**, và **Amazon Augmented AI (A2I)**. Đây là các dịch vụ AI của AWS sẽ được sử dụng trong workshop này.

### Amazon Textract
**Amazon Textract** là một dịch vụ học máy tự động trích xuất văn bản, chữ viết tay và dữ liệu từ các tài liệu đã quét. Nó không chỉ dừng lại ở việc nhận dạng ký tự quang học (OCR) đơn giản, mà còn có khả năng nhận biết, hiểu và trích xuất dữ liệu từ các biểu mẫu và bảng. Hiện nay, nhiều công ty trích xuất dữ liệu thủ công từ các tài liệu đã quét như PDF, hình ảnh, bảng và biểu mẫu, hoặc thông qua phần mềm OCR đơn giản yêu cầu cấu hình thủ công (thường phải cập nhật khi biểu mẫu thay đổi). Để vượt qua các quy trình thủ công và tốn kém này, Textract sử dụng học máy để đọc và xử lý mọi loại tài liệu, trích xuất chính xác văn bản, chữ viết tay, bảng và dữ liệu khác mà không cần nỗ lực thủ công. Bạn có thể nhanh chóng tự động hóa quy trình xử lý tài liệu và hành động dựa trên thông tin đã trích xuất, cho dù bạn đang tự động hóa quy trình xử lý khoản vay hay trích xuất thông tin từ hóa đơn và biên lai. Textract có thể trích xuất dữ liệu trong vài phút thay vì hàng giờ hoặc ngày. Ngoài ra, bạn có thể thêm các đánh giá của con người với Amazon Augmented AI để giám sát các mô hình của mình và kiểm tra dữ liệu nhạy cảm.

### Amazon Comprehend
**Amazon Comprehend** là một dịch vụ xử lý ngôn ngữ tự nhiên (NLP-natural-language processing) sử dụng học máy để khám phá thông tin từ dữ liệu không có cấu trúc. Dịch vụ này có thể xác định các yếu tố quan trọng trong dữ liệu, bao gồm các tham chiếu đến ngôn ngữ, con người, địa điểm, và các tệp văn bản có thể được phân loại theo các chủ đề liên quan. Bạn có thể tự động và chính xác phát hiện cảm xúc của con người từ nội dung do người dùng tạo ra (chẳng hạn như đánh giá sản phẩm, bài đăng trên mạng xã hội, v.v.) theo thời gian thực. Điều này giúp thúc đẩy quyết định thông minh hơn và cải thiện trải nghiệm khách hàng. Amazon Comprehend không chỉ xác định nội dung có chứa thông tin cá nhân (PII), mà còn có thể xóa và che giấu nội dung đó. Comprehend hoàn toàn được quản lý, vì vậy bạn có thể bắt đầu nhanh chóng và xử lý hàng triệu tài liệu trong vài phút bằng cách tận dụng sức mạnh của học máy.

### Amazon Augmented AI (A2I)
**Amazon Augmented AI** là một dịch vụ học máy giúp dễ dàng xây dựng các quy trình làm việc cần thiết để có sự đánh giá của con người. Amazon A2I đưa việc đánh giá của con người đến tất cả các nhà phát triển, loại bỏ các công việc nặng nhọc không phân biệt liên quan đến việc xây dựng hệ thống đánh giá của con người hoặc quản lý số lượng lớn người đánh giá, cho dù hệ thống đó chạy trên AWS hay không. Amazon A2I tích hợp với cả Amazon Textract và Amazon Comprehend để cung cấp cho bạn khả năng đưa vào các bước đánh giá của con người trong quy trình xử lý tài liệu thông minh của mình.
