---
title : "Xử lý Tài liệu Thông minh với AWS AI Services"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Xử lý Tài liệu thông minh với AWS AI Services
### Tổng quan
Các tài liệu chứa nhiều thông tin quý giá và có nhiều hình thức, cấu trúc khác nhau. Trong hầu hết các trường hợp, bạn phải xử lý thủ công các tài liệu này để trích xuất thông tin và hiểu biết. Việc này tốn thời gian, dễ xảy ra lỗi, tốn kém và khó mở rộng quy mô. Không chỉ cần trích xuất thông tin từ các tài liệu một cách nhanh chóng, bạn còn muốn tự động hóa các quy trình kinh doanh hiện đang phụ thuộc vào các đầu vào và sự can thiệp thủ công qua nhiều loại tệp và định dạng khác nhau.
### Mục tiêu của Workshop

Mục tiêu của workshop này là cung cấp cho bạn trải nghiệm thực tế trong việc hiểu và xây dựng các thành phần cần thiết để thiết lập một quy trình làm việc **IDP** với **AWS AI services**. Bạn sẽ học cách triển khai các giai đoạn khác nhau của một quy trình làm việc **IDP** bằng cách:

- Sử dụng **Amazon SageMaker Studio** như một môi trường phát triển tích hợp (IDE)
- Học các kiến thức cơ bản về **Amazon Textract** và các API khác nhau có thể được sử dụng để trích xuất văn bản và xác định các mối quan hệ từ nội dung tài liệu.
- Huấn luyện một bộ phân loại tùy chỉnh với **Amazon Comprehend** và sử dụng nó để phân loại tài liệu.
- Huấn luyện một trình nhận dạng thực thể tùy chỉnh với **Amazon Comprehend** và sử dụng nó để phát hiện các thực thể cụ thể trong doanh nghiệp.
- Thực hiện làm giàu tài liệu bằng cách sử dụng các thực thể tùy chỉnh và xóa bỏ tài liệu bằng cách sử dụng dữ liệu hình học do **Amazon Textract** tạo ra.
- Học cách cấu hình các vòng lặp đánh giá con người của **Amazon Augmented AI** để xem xét thông tin đã trích xuất.
### Chi phí của Workshop
Bạn có thể sử dụng ngay các chức năng và dịch vụ AWS cần thiết trong workshop này và thử nghiệm miễn phí trên một tài khoản AWS mới. 
### Sau khi hoàn thành Workshop
Nếu bạn không còn sử dụng các chức năng đã triển khai sau workshop, bạn vẫn có thể phát sinh chi phí. Bạn có thể tìm thêm thông tin về vấn đề này và cách xóa các thành phần đã tạo trong phần [Clean up](7-cleanup/)

### Nội dung
 1. [Introduction ](1-Introduce/)
 2. [Preparation](2-prerequiste/)
 3. [Document Classification](3-DocumentClassification/)
 4. [Manage session logs](4-DocumentExtraction/)
 5. [Port Forwarding](5-DocumentExtractionandEnrichment/)
 6. [DocumentReviewandVerification](6-DocumentReviewandVerification/)
 7. [Clean up](7-cleanup/)
