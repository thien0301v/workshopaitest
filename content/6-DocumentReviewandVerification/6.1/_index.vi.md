---
title : "Cài đặt và yêu cầu cho Amazon S3 bucket"
date : "`r Sys.Date()`"
weight : 1
chapter : false
---

- Chúng ta sẽ cần một Amazon S3 bucket, sẽ được sử dụng để lưu trữ dữ liệu cho các công nhân A2I. Bucket này đã được tạo như một phần của CloudFormation stack. Tên của S3 bucket nên theo mẫu `idp-a2i-xxxxxxxx`. Hãy truy cập vào bảng điều khiển Amazon S3 để tìm tên bucket.
Đi đến S3
    ![s1](/images/6/s1.png)
    ![s2](/images/6/s2.png)

### Cài đặt quy trình làm việc xem xét con người A2I
- Đi đến bảng điều khiển **Amazon SageMaker** và nhấp vào tùy chọn quy trình làm việc xem xét con người dưới Augmented AI trong bảng điều khiển bên trái. Sau đó nhấp vào nút Tạo quy trình làm việc xem xét con người.
    ![shu](/images/6/A2IHumanRWCreate.png)
- Cung cấp một Tên cho quy trình làm việc xem xét con người. Giá trị S3 bucket phải theo mẫu `s3://idp-a2i-xxxxxx/`. 
    ![s3](/images/6/s3.png)
- Trong IAM Role, chọn Tạo vai trò mới và sau đó nhập tên của S3 bucket (không bao gồm s3://, chẳng hạn như `idp-a2i-xxxxxx`).
    ![s4](/images/6/s4.png)
    ![s5](/images/6/s5.png)
    ![s6](/images/6/s6.png)
- Dưới loại nhiệm vụ, chọn tùy chọn Textract - Trích xuất cặp khóa-giá trị.
    ![s7](/images/6/s7.png)
- Tiếp theo, dưới mục Trích xuất biểu mẫu Amazon Textract - Các điều kiện để kích hoạt xem xét con người, chọn ô Kích hoạt xem xét con người cho tất cả các khóa biểu mẫu được xác định bởi Amazon Textract với điểm tin cậy trong một khoảng nhất định và nhập các giá trị như bên dưới. Bạn cũng có thể tùy chỉnh mẫu nhiệm vụ của người lao động, nhưng để phục vụ cho mục đích demo này, hãy chọn Tạo từ mẫu mặc định và nhập tên mẫu (ví dụ: `idp-a2i-template`).
    ![s8](/images/6/s8.png)
    ![s9](/images/6/s9.png)
- Dưới **Worker task template design** nhập **Task description**. Bạn cũng có thể tùy chỉnh **Instructions** như dưới đây.
    ![s10](/images/6/s10.png)
- Dưới phần  **Workers** section, chọn **Private** worker type. Click on the create a **new team** link to create a new Private Team.
    ![s11](/images/6/s11.png)
    ![s12](/images/6/s12.png)
- Dưới **Add workers**, chọn **Invite new workers by email**. Trong phần **Email addresses** nhập email của bạn. Dưới tên tổ chức, nhập **tên công ty của bạn**. For **Contact Email** ử dụng email của bạn để nhận hướng dẫn. Để các trường khác ở mặc định và nhấp vào **Create Private Team**.
    ![s13](/images/6/s13.png)
    ![s14](/images/6/s14.png)
- Quay lại **Create Human flow** và làm mới:
    ![s15](/images/6/s15.png)
- Nhấp vào **Create** để hoàn thành việc tạo quy trình làm việc xem xét con người. Sau khi được tạo, quy trình làm việc sẽ hoạt động và sẵn sàng để sử dụng.
  

  
  
    
  
  


