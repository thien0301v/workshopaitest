---
title : "Phân loại tài liệu với endpoint thời gian thực (tùy chọn)"
date : "`r Sys.Date()`"
weight : 7
chapter : false
---
Bước tiếp theo là sử dụng endpoint thời gian thực của **Amazon Comprehend** để phân loại các tài liệu này. Chúng ta sử dụng hàm `comprehend.classify_document()` với văn bản tài liệu đã được trích xuất và endpoint suy diễn làm các tham số đầu vào. Để phân loại một tài liệu mẫu, chúng ta sẽ chuyển đổi tài liệu thành `ByteArray` và sau đó sử dụng API `classify_document` của **Textract** để phân loại nó. Vì `classify_document` là một API thời gian thực (đồng bộ), chúng ta sẽ gọi nó với byte tài liệu của tài liệu mẫu trên. Một lần nữa, như trước đây, chúng ta sẽ để **Amazon Comprehend** sử dụng **Amazon Textract** trong nền để đọc tài liệu và sau đó phân loại nó. Vì chúng ta cho phép Comprehend sử dụng **Amazon Textract** trong nền để trích xuất văn bản, chúng ta sẽ bị giới hạn sử dụng tài liệu một trang.

Khi endpoint đã được tạo, chúng ta sẽ sử dụng một loạt tài liệu trong thư mục `/samples/mixedbag/` và cố gắng phân loại chúng thành tài liệu sao kê ngân hàng, hóa đơn và biên lai tương ứng.
    ![s29](/images/3.clas/s29.png)
Hãy xem một trong những tài liệu:
    ![s30](/images/3.clas/s30.png)
Để phân loại tài liệu mẫu này, chúng ta sẽ trước tiên chuyển đổi tài liệu thành `ByteArray` và sau đó sử dụng API `classify_document` của Textract để phân loại nó. Vì `classify_document` là một API thời gian thực (đồng bộ), chúng ta sẽ gọi nó với byte tài liệu của tài liệu mẫu trên. Một lần nữa, như trước đây, chúng ta sẽ để **Amazon Comprehend** sử dụng **Amazon Textract** trong nền để đọc tài liệu và sau đó phân loại nó. Vì chúng ta cho phép *Comprehend* sử dụng **Amazon Textract** trong nền để trích xuất văn bản, chúng ta sẽ bị giới hạn sử dụng tài liệu một trang.
    ![s31](/images/3.clas/s31.png)
Bây giờ hãy chạy suy diễn trên tài liệu mẫu của chúng ta:
    ![s32](/images/3.clas/s32.png)
Lưu ý rằng Comprehend sẽ trả về tất cả các loại tài liệu với điểm số tin cậy liên kết với mỗi loại trong một mảng các cặp khóa-giá trị (Tên-Điểm số), chúng ta có thể chọn chỉ loại tài liệu có điểm số tin cậy cao nhất từ phản hồi của endpoint.
### Kết luận
Trong notebook này, chúng ta đã huấn luyện một bộ phân loại tùy chỉnh của Amazon Comprehend bằng cách sử dụng các tài liệu mẫu của chúng ta, bằng cách trích xuất văn bản từ các tài liệu sử dụng Amazon Textract và gán nhãn dữ liệu vào định dạng tệp CSV cho tập dữ liệu huấn luyện. Sau đó, chúng ta đã huấn luyện một bộ phân loại tùy chỉnh của Amazon Comprehend với văn bản đã trích xuất và tạo một endpoint thời gian thực của Amazon Comprehend để thực hiện phân loại một tập hợp tài liệu không xác định.

Trong notebook tiếp theo, chúng ta sẽ xem xét một số phương pháp để trích xuất những hiểu biết quan trọng từ các tài liệu của chúng ta bằng cách sử dụng Amazon Textract.