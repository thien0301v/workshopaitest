---
title : "Tạo endpoint thời gian thực cho Amazon Comprehend (tùy chọn)"
date : "`r Sys.Date()`"
weight : 6
chapter : false
---

Để sử dụng mô hình bộ phân loại tùy chỉnh của Amazon Comprehend, chúng ta cần tạo một endpoint thời gian thực. Các endpoint thời gian thực có thể được tạo ra thông qua mã lập trình bằng cách sử dụng client Boto3 của Comprehend hoặc bằng tay thông qua bảng điều khiển. Để tìm hiểu cách tạo một endpoint thời gian thực bằng bảng điều khiển, hãy tham khảo tài liệu. Chúng ta sử dụng API CreateEndpoint thông qua phương thức `comprehend.create_endpoint()` của Boto3 để tạo endpoint thời gian thực.

Khi bộ phân loại tùy chỉnh của chúng ta đã được huấn luyện hoàn toàn (tức là trạng thái = TRAINED), chúng ta có thể tạo một endpoint thời gian thực. Chúng ta sẽ sử dụng endpoint này để phân loại tài liệu trong thời gian thực. Các khối mã sau đây sử dụng client Boto3 của Comprehend để tạo một endpoint, nhưng bạn cũng có thể tạo một endpoint bằng tay qua bảng điều khiển. Hướng dẫn về cách làm điều đó có thể được tìm thấy trong phần tiếp theo.
    ![s27](/images/3.clas/s27.png)


Có thể mất khoảng 15 phút để endpoint được tạo. Khi endpoint được tạo thành công, bạn có thể bắt đầu phân loại các tài liệu (đây là bộ tài liệu không xác định của chúng ta) trong thư mục `/samples/mixedbag`. Hãy nhớ rằng mục tiêu của chúng ta là phân loại các tài liệu không xác định này thành các loại sao kê ngân hàng, hóa đơn và biên lai tương ứng.
    ![s28](/images/3.clas/s28.png)

