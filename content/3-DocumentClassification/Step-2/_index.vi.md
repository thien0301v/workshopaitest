---
title : "Trích xuất văn bản từ tài liệu mẫu bằng Amazon Textract"
date : "`r Sys.Date()`"
weight : 2
chapter : false
---

Trong phần này, chúng ta sử dụng API ``detect_document_text`` của **Amazon Textract** để trích xuất thông tin văn bản thô cho tất cả các tài liệu trong S3. Chúng ta cũng sẽ gắn nhãn dữ liệu theo loại tài liệu. Dữ liệu đã được gắn nhãn này sẽ được sử dụng để huấn luyện bộ phân loại tùy chỉnh **Amazon Comprehend**. Chúng ta định nghĩa một hàm tiện ích sử dụng API  ``textract_extract_text`` để trích xuất văn bản từ một tài liệu, xác định loại tài liệu (hoặc thư mục trong S3) mà nó thuộc về, sau đó gắn nhãn dữ liệu và trả về một mảng[``<label>``, ``<document_text>``].
    ![s2](/images/3.clas/s2.png)

Thực thi tất cả các ô mã trong bước này để chuẩn bị dữ liệu đã gắn nhãn cho việc huấn luyện bộ phân loại **Comprehend**. Cuối bước này, chúng ta sẽ có một tập hợp `labeled_collection` ẵn sàng với dữ liệu đã gắn nhãn cần thiết cho việc phân loại bằng **Amazon Comprehend classification**. Lưu ý rằng một giả định lớn ở đây là chúng ta đã có một tập tài liệu lịch sử đã được gắn nhãn để có thể huấn luyện một mô hình phân loại tùy chỉnh.
    ![train](/images/3.clas/train.png)

