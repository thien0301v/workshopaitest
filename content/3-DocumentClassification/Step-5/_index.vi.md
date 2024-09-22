---
title : "Phân loại tài liệu với bộ phân loại tùy chỉnh của Amazon Comprehend"
date : "`r Sys.Date()`"
weight : 5
chapter : false
---

Trong bước này, chúng ta sẽ sử dụng mô hình phân loại tùy chỉnh của **Amazon Comprehend** để phân loại các tài liệu mẫu. Chúng ta sẽ sử dụng API `start_document_classification_job` để khởi chạy một công việc không đồng bộ nhằm phân loại các tài liệu. API này hỗ trợ các tài liệu ở định dạng gốc của chúng (PDF/PNG/JPG/TIF) và có thể sử dụng Amazon Textract ở chế độ nền để đọc văn bản từ các tài liệu và sau đó xác định loại tài liệu. Hãy bắt đầu bằng cách tải các tài liệu mẫu của chúng ta lên S3 bucket.
    ![s18](/images/3.clas/s18.png)
Phân loại không đồng bộ của Amazon Comprehend hoạt động với các tệp PDF, PNG, JPEG cũng như các tệp văn bản mã hóa UTF-8. Vì các tài liệu mẫu của chúng ta trong thư mục samples có định dạng PNG, chúng ta sẽ chỉ định một DocumentReadAction và sử dụng Amazon Textract với tùy chọn `TEXTRACT_DETECT_DOCUMENT_TEXT`. Điều này sẽ thông báo cho Amazon Comprehend sử dụng API `DetectDocumentText` của **Amazon Textract** để trích xuất văn bản và sau đó thực hiện phân loại. Đối với **InputFormat**, chúng ta sẽ sử dụng chế độ `ONE_DOC_PER_FILE`, có nghĩa là mỗi tệp là một tài liệu riêng lẻ (chế độ khác là `ONE_DOC_PER_LINE`, có nghĩa là mỗi dòng trong tệp văn bản là một tài liệu, điều này thích hợp cho các tài liệu nhỏ như đánh giá sản phẩm hoặc bản ghi cuộc trò chuyện dịch vụ khách hàng, v.v.).
    ![s20](/images/3.clas/s20.png)

### Kiểm tra trạng thái của công việc phân loại
Khối mã dưới đây sẽ kiểm tra trạng thái của công việc phân loại. Nếu công việc hoàn thành, nó sẽ tải xuống kết quả dự đoán. Kết quả là một tệp zip chứa kết quả suy luận cho mỗi tài liệu được phân loại. Tệp zip cũng sẽ chứa kết quả của quá trình **Textract** mà **Amazon Comprehend** đã thực hiện.
    ![s21](/images/3.clas/s21.png)
    ![s22](/images/3.clas/s22.png)

Tiếp tục chạy mã
    ![s23](/images/3.clas/s23.png)


Hãy xem kết quả phân loại của Amazon Comprehend. Chúng ta đã thu thập kết quả cho tất cả các tệp trong biến documents. Script ở trên sẽ tải xuống và giải nén tệp zip vào máy cục bộ, vì vậy bạn có thể điều hướng vào thư mục `classification-output` từ bảng duyệt tệp ở phía bên trái và kiểm tra các tệp một cách thủ công.
    ![s24](/images/3.clas/s24.png)
Các tài liệu của chúng ta trong thư mục `samples/mixedbag` hiện đã được phân loại. Chúng ta sẽ tải chúng lên S3 với nhãn tiền tố phù hợp.
    ![s25](/images/3.clas/s25.png)

Quá trình phân loại của **Amazon Comprehend** cũng đã tạo ra kết quả Textract từ các tài liệu (có trong thư mục `classification-output/amazon-textract-output`). Thư mục này chứa một thư mục cho mỗi tài liệu với phản hồi JSON của **Amazon Textract**. Hãy tải văn bản thô của mỗi tài liệu này vào khung dữ liệu. Chúng ta sẽ sử dụng công cụ pretty printer để lấy các dòng văn bản từ các tài liệu.
    ![s26](/images/3.clas/s26.png)

Tiếp tục với bài thực hành.