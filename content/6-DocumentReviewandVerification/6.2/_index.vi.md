---
title : "Xác minh"
date : "`r Sys.Date()`"
weight : 2
chapter : false
---
Bây giờ hãy quay lại notebook `04-idp-document-a2i.ipynb`. **Bắt đầu chạy các ô mã từ đầu. Bạn sẽ cần cung cấp một số thông tin khi tiến hành.**
- Nhập tên S3 bucket `idp-a2i-xxxxxx` để khởi tạo biến BUCKET. Chúng ta sẽ sử dụng biến BUCKET này trong suốt notebook.
    ![s16](/images/6/s16.png)
- Bạn sẽ cần cung cấp ARN của nhóm làm việc riêng tư mà bạn đã tạo trước đó. Để tìm ARN của nhóm làm việc, hãy nhấp vào Quy trình làm việc xem xét con người mà bạn đã tạo trước và sao chép ARN từ phần Tóm tắt trong mục Lực lượng lao động. Nó sẽ có dạng `<arn:aws:sagemaker:<region>:<account_id>:workteam/private-crowd/<team-name>`. Nhập giá trị này để khởi tạo `WORKTEAM_ARN` trong notebook.
    ![s17](/images/6/s17.png)
- Bây giờ chúng ta đã thiết lập định nghĩa Quy trình A2I, tất cả những gì còn lại là gọi Amazon Textract's Analyze Document API bao gồm các tham số A2I trong HumanLoopConfig. Cung cấp ARN quy trình A2I sẽ được **Amazon Textract** sử dụng. Bạn có thể tìm thấy ARN quy trình trong màn hình **Summary** lực lượng lao động xem xét con người.
    ![s18](/images/6/s18.png)
- Thực hiện ô mã để thực hiện `AnalyzeDocument`. Khi dữ liệu được trích xuất bằng Amazon Textract, các cặp khóa-giá trị sẽ xuất hiện trong cổng thông tin phân loại cho việc xem xét của con người.
    ![s19](/images/6/s19.png)
- Sau đó, hãy vào **Amazon SageMaKer** -> **Labeling workforces**
    ![s20](/images/6/s20.png)
- Nhấp vào URL đăng nhập cổng phân loại
    ![s21](/images/6/s21.png)
- Đăng nhập vào cổng phân loại/xem xét của con người. Bạn sẽ nhận được một email với liên kết đến cổng phân loại/xem xét con người với thông tin chi tiết về cách đăng nhập và một URL cổng. Làm theo hướng dẫn trong email, bạn sẽ cần đặt lại mật khẩu để đăng nhập. **Start Working**.
    ![s22](/images/6/s22.png)
- Bây giờ bạn có thể xem thông tin đã được trích xuất ở bên phải, để xác minh và thực hiện các thay đổi nếu cần. Gửi công việc khi hoàn thành. Bạn cũng có tùy chọn từ chối và phát hành nhiệm vụ nếu cần.
    ![s23](/images/6/s23.png)

### Conclusion
Trong notebook này, chúng ta đã tạo một quy trình xem xét con người A2I cho **Amazon Textract** bao gồm một nhóm làm việc riêng tư sử dụng **Amazon Augmented AI**. Sau đó, chúng ta đã sử dụng **Amazon Textract** để trích xuất dữ liệu từ một tài liệu mẫu và thêm một Vòng cấu hình con người cho việc xem xét của con người. Cuối cùng, chúng ta đã thực hiện một nhiệm vụ xem xét thủ công thông qua một cổng tùy chỉnh.