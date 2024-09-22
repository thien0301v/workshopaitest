---
title : "Getting Started"
date : "`r Sys.Date()`"
weight : 1
chapter : false

---

Trong notebook đầu tiên, chúng ta sẽ tải lên các sao kê ngân hàng, hóa đơn và biên lai này vào một bucket Amazon S3, sử dụng Amazon Textract để trích xuất văn bản thô từ các tài liệu, gắn nhãn dữ liệu phù hợp, và sau đó huấn luyện một bộ phân loại tùy chỉnh của **Amazon Comprehend** với dữ liệu đã được gắn nhãn.

1. Mở notebook đầu tiên có tiêu đề ``01-idp-prep-document-classification.ipynb``. Bạn sẽ được nhắc chọn một image và kernel. Chọn các tùy chọn như hình dưới đây và nhấn **Select** .
   ![envir](/images/3.clas/envir.png)
Notebook sẽ tự động gắn vào một instance **ml.t3.medium** (với 2vCPU và 4GiB bộ nhớ). Nếu không, nhấp vào "Switch instance type" và chọn **ml.t3.medium** từ danh sách các loại instance.

>⚠️ ``ml.t3.medium`` là loại instance được ưu tiên. Vui lòng KHÔNG chọn bất kỳ loại instance nào khác vì có thể dẫn đến chi phí không mong muốn cho tài khoản.
