---
title : "Tạo công việc huấn luyện phân loại cho Amazon Comprehend"
date : "`r Sys.Date()`"
weight : 4
chapter : false
---

Bây giờ chúng ta đã trích xuất văn bản từ các tài liệu và cũng đã gắn nhãn cho chúng, chúng ta sẽ tạo dữ liệu huấn luyện để huấn luyện một mô hình phân loại tùy chỉnh của Amazon Comprehend. Tập dữ liệu của chúng ta có 100 mẫu của mỗi loại tài liệu, vì vậy chúng ta sẽ có khoảng 300 dòng dữ liệu đã được gắn nhãn.

Chúng ta sẽ sử dụng tính năng Phân loại tùy chỉnh của **Amazon Comprehend** để huấn luyện mô hình của riêng mình nhằm phân loại các tài liệu. Chúng ta sử dụng API `CreateDocumentClassifier` để tạo một bộ phân loại sẽ huấn luyện một mô hình tùy chỉnh bằng cách sử dụng tệp CSV chứa dữ liệu đã được gắn nhãn mà chúng ta đã tạo ở trên. Dữ liệu huấn luyện bao gồm văn bản đã được trích xuất, được trích xuất bằng Amazon Textract, và sau đó đã được gắn nhãn. Các ô mã dưới đây sử dụng hàm `create_document_classifier` từ **SDK Python boto3** để khởi tạo quá trình huấn luyện mô hình.

#### Tạo công việc huấn luyện Phân loại tùy chỉnh cho Amazon Comprehend
Chúng ta sẽ sử dụng tính năng Phân loại tùy chỉnh của Amazon Comprehend để huấn luyện mô hình phân loại tài liệu của mình. Chúng ta sẽ sử dụng API `CreateDocumentClassifier` của **Amazon Comprehend** để tạo một bộ phân loại nhằm huấn luyện mô hình tùy chỉnh bằng cách sử dụng tệp CSV chứa dữ liệu đã được gắn nhãn mà chúng ta đã tạo ở trên. Dữ liệu huấn luyện chứa văn bản đã được trích xuất bằng **Amazon Textract**, và sau đó đã được gắn nhãn.
    ![s16](/images/3.clas/s16.png)

Lưu ý rằng bạn cũng có thể tạo một bộ phân loại tùy chỉnh bằng cách sử dụng giao diện **Amazon Comprehend** console theo cách thủ công. Tham khảo tài liệu hướng dẫn để tìm hiểu thêm về cách tạo một bộ phân loại tùy chỉnh bằng console. Tiếp tục thực hiện các ô mã còn lại trong bước này. Quá trình huấn luyện bộ phân loại tùy chỉnh có thể mất khoảng 30 phút.
    ![s17](/images/3.clas/s17.png)