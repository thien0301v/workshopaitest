---
title : "Phân loại tài liệu"
date : "`r Sys.Date()`"
weight : 3
chapter : false
---

### Tổng quan

Phân loại tài liệu là một quá trình hai bước. Đầu tiên, bạn huấn luyện một bộ phân loại tùy chỉnh để nhận biết các loại tài liệu mà bạn quan tâm. Sau đó, bạn gửi các tài liệu chưa được gắn nhãn để phân loại.

Để huấn luyện bộ phân loại, bạn chỉ định các tùy chọn mong muốn và gửi tài liệu cho Amazon Comprehend để sử dụng làm tài liệu huấn luyện. Dựa trên các tùy chọn bạn đã chỉ định, Amazon Comprehend tạo ra một mô hình học máy tùy chỉnh (bộ phân loại) được huấn luyện dựa trên các tài liệu bạn cung cấp. Mô hình tùy chỉnh này sẽ kiểm tra từng tài liệu bạn gửi. Sau đó, nó sẽ trả về loại cụ thể đại diện tốt nhất cho nội dung (nếu bạn sử dụng chế độ đa loại) hoặc tập hợp các loại phù hợp (nếu bạn sử dụng chế độ đa nhãn).

Trong bài thực hành này, chúng ta sẽ tiến hành thực hành phân loại tài liệu sử dụng Amazon Comprehend Custom Classification. Chúng ta sẽ sử dụng Amazon Textract để trích xuất văn bản từ các tài liệu, gắn nhãn chúng, và sau đó sử dụng dữ liệu này để huấn luyện bộ phân loại tùy chỉnh của Amazon Comprehend. Mục tiêu của chúng ta là - với một nhóm tài liệu chưa biết, chúng ta muốn phân loại được đâu là sao kê ngân hàng, đâu là hóa đơn và đâu là biên lai. Để chuẩn bị dữ liệu huấn luyện, chúng ta sẽ sử dụng các sao kê ngân hàng, hóa đơn và biên lai có sẵn.

![arch](/images/3.clas/arch.png) 

### Bộ tài liệu mẫu
#### Sao kê ngân hàng
Hình ảnh dưới đây là trang đầu tiên của một sao kê ngân hàng tiêu chuẩn gồm nhiều trang, với các chi tiết như tên khách hàng, địa chỉ, tổng hợp tài khoản, số dư hiện tại, v.v.
![bank](/images/3.clas/bank-doc.png)

#### Hóa đơn
Hình ảnh dưới đây là một hóa đơn thanh toán tiêu chuẩn với các chi tiết như thông tin doanh nghiệp, người nhận hóa đơn, sản phẩm, mã hóa đơn, v.v.
![invoice](/images/3.clas/invoice-doc.png)

#### Biên lai
Hình ảnh dưới đây là một biên lai cửa hàng tiêu chuẩn với các chi tiết như các mặt hàng đã mua, thông tin cửa hàng, giá bán lẻ cho mỗi mặt hàng, thuế suất bán hàng, v.v.
![receipt](/images/3.clas/receipt-doc.png)
