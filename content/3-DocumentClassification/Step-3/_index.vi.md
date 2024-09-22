---
title : "Chuẩn bị tập dữ liệu CSV để huấn luyện bộ phân loại tùy chỉnh Amazon Comprehend"
date : "`r Sys.Date()`"
weight : 3
chapter : false
---

Trong bước này, dữ liệu đã trích xuất sẽ được ghi vào tệp CSV và tải lên S3. Tệp này sẽ được sử dụng làm dữ liệu huấn luyện cho bước tiếp theo. Chúng ta sẽ huấn luyện một bộ phân loại tùy chỉnh của Amazon Comprehend ở chế độ phân loại đa lớp **(Multi-class)** bằng cách sử dụng tệp CSV. Hãy tham khảo tài liệu hướng dẫn chuẩn bị dữ liệu cho chế độ Multi-class để huấn luyện mô hình. Các tệp CSV là các tệp văn bản thuần mã hóa UTF-8 và phải tuân theo định dạng sau:
```
CLASS,Text of document 1
CLASS,Text of document 2
CLASS,Text of document 3
```
CHoàn thành việc thực thi các ô mã trong phần này để chuẩn bị tệp CSV và tải nó lên **S3**. Cuối bước này, chúng ta sẽ có dữ liệu huấn luyện ở định dạng CSV trong tệp có tên `comprehend_train_data.csv` với các lớp là `bank-statements`, `invoices` and `receipts`.

Bây giờ chúng ta đã trích xuất văn bản từ các tài liệu và cũng đã gắn nhãn cho chúng, chúng ta sẽ tạo dữ liệu huấn luyện để huấn luyện mô hình phân loại tùy chỉnh của **Amazon Comprehend**. Hãy xem qua dữ liệu đã được gắn nhãn. Chúng ta có 100 mẫu của mỗi loại tài liệu, vì vậy chúng ta sẽ có khoảng 300 dòng dữ liệu đã được gắn nhãn.
    ![s13](/images/3.clas/s13.png)

Chúng ta sẽ tạo tập dữ liệu huấn luyện từ văn bản đã trích xuất và tải nó lên **Amazon S3**. Tệp dữ liệu huấn luyện sẽ được viết ở định dạng CSV và sẽ được đặt tên là `comprehend_train_data.csv`. Lưu ý rằng bạn có thể có nhiều hơn một tệp CSV trong một S3 bucket để huấn luyện bộ phân loại tùy chỉnh của Comprehend. Nếu bạn có nhiều tệp, bạn có thể chỉ định thư mục chứa bucket/prefix khi gọi huấn luyện bộ phân loại tùy chỉnh. Amazon Comprehend sẽ tự động sử dụng tất cả các tệp dưới bucket/prefix để huấn luyện.

Các ô mã sau sẽ tải dữ liệu huấn luyện lên **S3** bucket và tạo một bộ phân loại tùy chỉnh của Comprehend. Bạn cũng có thể tạo bộ phân loại tùy chỉnh theo cách thủ công, vui lòng xem các phần tiếp theo để biết hướng dẫn chi tiết cách thực hiện điều đó.
    ![s14](/images/3.clas/s14.png)

Hoàn thành việc thực thi các ô mã trong phần này để chuẩn bị tệp CSV và tải nó lên S3. Cuối bước này, chúng ta sẽ có dữ liệu huấn luyện ở định dạng CSV trong tệp có tên ``comprehend_train_data.csv`` với các class `bank-statements`, `invoices` and `receipts`.
    ![s15](/images/3.clas/s15.png)