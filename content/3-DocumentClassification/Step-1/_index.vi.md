---
title : "Cài đặt notebook và tải tài liệu mẫu lên Amazon S3"
date : "`r Sys.Date()`"
weight : 1
chapter : false
---


Trong bước này, chúng ta sẽ cài đặt các thư viện cần thiết, nhập các mô-đun cần thiết và khởi tạo các biến. Chúng ta cũng sẽ tải các tài liệu mẫu từ kho lưu trữ của workshop và tải chúng lên bucket S3 của SageMaker để có thể xử lý. Lệnh ``curl``  dưới đây sẽ tải về tệp ``classification-training.zip`` này chứa dữ liệu cần thiết để huấn luyện bộ phân loại tùy chỉnh **Amazon Comprehend Classifier**.

1. Chạy từ Bước 1 đến 6
   ![run](/images/3.clas/run.png)

    ![down](/images/3.clas/download.png)
2. ITrong các ô mã tiếp theo, chúng ta sẽ giải nén tất cả các tệp từ tệp zip và sau đó tải chúng lên **Amazon S3**. Hoàn thành việc thực thi tất cả các ô mã trong bước này.
   ![step7](/images/3.clas/step7.png)
   ![step8](/images/3.clas/step8.png)
   Dữ liệu đã được tải lên S3 và có thể tìm thấy trong **AWS S3**.
   ![s3](/images/3.clas/s3.png)
Hoặc chúng ta có thể sử dụng mã trong tệp để trích xuất dữ liệu
   ![s3](/images/3.clas/c2.png)