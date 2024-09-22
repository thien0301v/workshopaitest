---
title : "Trích xuất Tài liệu"
date : "`r Sys.Date()`"
weight : 4
chapter : false
---


### Trích xuất dữ liệu từ tài liệu bằng **Amazon Textract**
**Amazon Textract** là một dịch vụ máy học (ML) tự động trích xuất văn bản, chữ viết tay và dữ liệu từ các tài liệu quét. Nó vượt xa khả năng nhận diện ký tự quang học đơn giản (OCR) để xác định, hiểu và trích xuất dữ liệu từ các biểu mẫu và bảng. Hãy mở rộng các phần dưới đây để tìm hiểu ngắn gọn về khả năng trích xuất tài liệu của Amazon Textract.

### Phân tích phản hồi API của Amazon Textract
Bạn có thể trích xuất văn bản và thông tin dữ liệu có cấu trúc bằng cách sử dụng các API `DetectDocumentText` và `AnalyzeDocument` của **Amazon Textract**. Các API này trả về dữ liệu JSON chứa từ, dòng, biểu mẫu, bảng, thông tin hình học hoặc hộp giới hạn, mối quan hệ, v.v. Phản hồi JSON này có thể khó phân tích, đặc biệt là với các tài liệu lớn hoặc nhiều trang. Để làm điều này, chúng ta sẽ sử dụng một nhóm công cụ mang tên `amazon-textract-textractor` giúp dễ dàng lấy thông tin như từ, dòng, bảng và biểu mẫu từ tài liệu, và thu thập thông tin hộp giới hạn. Dưới đây là các tính năng có sẵn:

- A [caller](https://github.com/aws-samples/amazon-textract-textractor/tree/master/caller)  cung cấp một bộ chức năng sẵn sàng sử dụng và các triển khai mẫu để tăng tốc độ đánh giá và phát triển cho bất kỳ dự án nào sử dụng Amazon Textract, giúp dễ dàng gọi **Amazon Textract** bất kể loại tệp và vị trí.
- A [response parser](https://github.com/aws-samples/amazon-textract-response-parser) giúp dễ dàng phân tích JSON trả về từ Amazon Textract. Thư viện này phân tích JSON và cung cấp các cấu trúc ngôn ngữ lập trình cụ thể để làm việc với các phần khác nhau của tài liệu.
- A [prettyprinter](https://github.com/aws-samples/amazon-textract-textractor/tree/master/prettyprinter) cung cấp các chức năng để định dạng đầu ra nhận được từ Amazon Textract theo các định dạng dễ tiêu thụ hơn như CSV hoặc markdown.
- An [overlayer](https://github.com/aws-samples/amazon-textract-textractor/tree/master/overlayer) cung cấp thông tin hình học hộp giới hạn có thể được sử dụng cho mục đích chú thích hoặc xóa.

### Getting Started with Lab
Trong phần này, chúng ta sẽ xem xét cách trích xuất thông tin từ các tài liệu. Mở notebook `02-idp-document-extraction.ipynb` trong **Amazon SageMaker Studio** và làm theo các bước dưới đây.
   ![s1](/images/4/s1.png)

### Step 1: Thiết lập notebook
Trong bước này, chúng ta sẽ chọn kernel như notebook trước đó sẽ được sử dụng trong notebook này.
   ![s2](/images/4/s2.png)
Sau đó chạy các script trong Bước 1. 

Hãy chọn một sao kê ngân hàng mà chúng ta đã phân loại trong bài tập trước.
   ![s3](/images/4/s3.png)
   ![s4](/images/4/s4.png)


### Bước 2: Trích xuất dữ liệu không có cấu trúc bằng **Amazon Textract**
Trong bước này, chúng ta sẽ chủ yếu xem xét cách trích xuất thông tin văn bản (DÒNG và TỪ) từ một trong các sao kê ngân hàng. Dữ liệu văn bản dưới dạng TỪ và DÒNG có thể được trích xuất từ các tài liệu bằng cách sử dụng API `DetectDocumentText` của Amazon Textract. Đoạn mã sau gọi API để trích xuất văn bản từ tài liệu.

Amazon Textract là một dịch vụ OCR được hỗ trợ bởi ML có khả năng phát hiện và trích xuất văn bản từ các tài liệu. Dữ liệu văn bản dưới dạng TỪ và DÒNG có thể được trích xuất từ các tài liệu bằng cách sử dụng API `DetectDocumentText` của Amazon Textract. Hãy trích xuất các từ và dòng từ sao kê ngân hàng.
   ![s5](/images/4/s5.png)
Như bạn có thể thấy, chúng ta đã có thể trích xuất DÒNG và TỪ từ tài liệu, nhưng chúng ta cũng đã mất một số định dạng cấu trúc trong tài liệu. Ví dụ, tài liệu chứa một vài bảng và chúng ta muốn trích xuất thông tin bảng trong cấu trúc bảng. Vì vậy, hãy làm điều đó tiếp theo.

### Bước 3: Trích xuất dữ liệu bảng bằng Amazon Textract
Trong bước này, chúng ta sẽ xem xét ngắn gọn cách trích xuất thông tin bảng từ sao kê ngân hàng. Sao kê ngân hàng của chúng ta có hai bảng.
   ![s6](/images/4/s6.png)
Như bạn có thể thấy, phản hồi từ **Amazon Textract** là một đối tượng JSON lớn chứa rất nhiều thông tin. Hãy phân tích dữ liệu bảng từ phản hồi này. Để làm điều này, chúng ta sẽ xem cách trích xuất các bảng bằng công cụ phân tích phản hồi Textract mà chúng ta đã cài đặt trước đó.
   ![s7](/images/4/s7.png)
Trong các ô mã ở trên, chúng ta đã sử dụng API `AnalyzeDocument` của Textract để trích xuất thông tin từ tài liệu và sau đó đã sử dụng trình phân tích phản hồi Textract để phân tích các bảng từ phản hồi JSON. Chúng ta có thể sử dụng các công cụ bổ sung để gọi API Textract và sử dụng công cụ trình bày đẹp để xem các bảng theo cách dễ đọc hơn một chút. Chúng ta sẽ xem cách trích xuất các bảng bằng công cụ trình bày đẹp của Textract. Chúng ta cũng sẽ sử dụng phương pháp `call_textract` từ công cụ Caller của Textract mà chúng ta đã cài đặt trước đó. Tập hợp các công cụ này giúp dễ dàng thực hiện các cuộc gọi API Textract và phân tích đầu ra JSON của nó. Trong các phần tiếp theo, chúng ta sẽ sử dụng những công cụ này để thực hiện các cuộc gọi API và sau đó để phân tích phản hồi JSON.
   ![s8](/images/4/s8.png)
Trong ô mã trên, chúng ta đã trích xuất các bảng dưới dạng danh sách Python và sau đó chuyển đổi chúng thành DataFrame của Pandas. Bạn cũng có thể trích xuất các bảng ở các định dạng khác như CSV, TSV, v.v. 
   ![s9](/images/4/s9.png)

### Step 4: Trích xuất dữ liệu biểu mẫu (khóa/giá trị) bằng Amazon Textract
Hãy xem cách Amazon Textract có thể được sử dụng để trích xuất dữ liệu biểu mẫu từ tài liệu. Trong ví dụ này, chúng ta sẽ sử dụng một biểu mẫu xác nhận việc làm mẫu.
   ![s10](/images/4/s10.png)
Trong ví dụ trước, tài liệu của chúng ta nằm trong S3 và chúng ta đã gọi Amazon Textract bằng cách chỉ định vị trí S3 của tài liệu. Trong trường hợp này, tài liệu của chúng ta nằm trên máy tính cục bộ, chúng ta có thể tải tài liệu này lên S3, hoặc chúng ta có thể sử dụng Byte Array của tài liệu từ môi trường cục bộ của chúng ta để gọi API. Hãy sử dụng Byte Array của tài liệu cho ví dụ này. Lưu ý rằng phương pháp này chỉ áp dụng cho API Textract đồng bộ (thời gian thực), vì các API không đồng bộ chỉ hỗ trợ tài liệu đặt trong S3. Trong ô mã dưới đây, trước tiên chúng ta chuyển đổi tài liệu thành một Byte array, và sau đó gọi API `AnalyzeDocument` với tính năng FORMS. Sau đó, chúng ta sử dụng công cụ phân tích phản hồi Textract để phân tích các cặp khóa/giá trị của biểu mẫu và in chúng ra.
   ![s11](/images/4/s11.png)
Và kết quả là:
   ![s12](/images/4/s12.png)

### Bước 5: Trích xuất dựa trên truy vấn bằng Amazon Textract
Khi xử lý một tài liệu bằng Amazon Textract, bạn có thể thêm các truy vấn vào phân tích của mình để chỉ định thông tin mà bạn cần. Điều này bao gồm việc truyền một câu hỏi, chẳng hạn như "Số an sinh xã hội của khách hàng là gì?" đến Amazon Textract. Amazon Textract sau đó sẽ tìm thông tin trong tài liệu cho câu hỏi đó và trả về trong một cấu trúc phản hồi tách biệt với phần còn lại của thông tin trong tài liệu. Các truy vấn có thể được xử lý riêng lẻ hoặc kết hợp với bất kỳ FeatureType nào khác, chẳng hạn như BẢNG hoặc BIỂU MẪU. Các truy vấn có thể là một công cụ mạnh mẽ trong những tình huống mà chỉ một vài thông tin quan trọng cần thiết từ một tài liệu.

Hãy để lại một vài truy vấn để trích xuất từ biểu mẫu xác nhận việc làm của chúng ta.
   ![s13](/images/4/s13.png)
   ![s14](/images/4/s14.png)

### Bước 6: Phát hiện chữ ký với Amazon Textract
Amazon Textract có thể phát hiện sự hiện diện của chữ ký trong các tài liệu. API AnalyzeDocument có bốn loại tính năng sau - Biểu mẫu, Bảng, Truy vấn và Chữ ký. Tính năng Chữ ký có thể được sử dụng riêng lẻ hoặc kết hợp với các loại tính năng khác. Khi được sử dụng riêng lẻ, loại tính năng Chữ ký cung cấp phản hồi json bao gồm a) vị trí và điểm số tin cậy của các chữ ký được phát hiện và b) văn bản thô (từ và dòng) từ tài liệu. Nếu tính năng Chữ ký được sử dụng cùng với tính năng Biểu mẫu mà trích xuất các cặp khóa giá trị trong một biểu mẫu, chữ ký được phát hiện sẽ được liên kết với giá trị của khóa liên quan. Tương tự, khi được sử dụng cùng với loại tính năng Bảng, chữ ký được phát hiện sẽ được liên kết với một ô trong bảng.

Hãy thử phát hiện chữ ký trong biểu mẫu xác nhận việc làm của chúng ta.
   ![s15](/images/4/s15.png)

Textract đã phát hiện ba chữ ký trong tài liệu cùng với thông tin hộp giới hạn và điểm số tin cậy của chúng.

### Trích xuất hóa đơn/biên lai bằng Amazon Textract
Bây giờ hãy xem API `AnalyzeExpense` để trích xuất thông tin từ một tài liệu hóa đơn.
   ![s16](/images/4/s16.png)

Điều quan trọng cần lưu ý là Textract cung cấp khả năng trích xuất riêng biệt "các mục dòng" trong hóa đơn và "Summary" của hóa đơn.
   ![s17](/images/4/s17.png)
   ![s18](/images/4/s18.png)

### Bước 8: Trích xuất tài liệu danh tính bằng Amazon Textract
Để xem cách trích xuất tài liệu danh tính hoạt động với **Amazon Textract**, chúng ta sẽ sử dụng một tài liệu hộ chiếu mẫu. Hộ chiếu là một tài liệu đặc biệt, tức là một tài liệu danh tính. Để trích xuất thông tin từ hộ chiếu và giấy phép lái xe của Hoa Kỳ, API `AnalyzeID` của Amazon Textract có thể được sử dụng.
   ![s19](/images/4/s19.png)
Chúng ta sẽ sử dụng công cụ `call_textract_analyzeid` từ thư viện `amazon-textract-textractor`.
   ![s20](/images/4/s20.png)

Lưu ý rằng trong lệnh gọi đến `call_textract_analyzeid` bạn cũng có thể truyền một đường dẫn S3 vào tham số `document_pages` as
`call_textract_analyzeid(document_pages=["s3://bucket/prefix/doc.png"])`

Hãy xem thông tin đã trích xuất từ tài liệu hộ chiếu. Lưu ý rằng các khóa được chuẩn hóa, điều này giúp dễ dàng phân tích thông tin cần thiết từ phản hồi JSON từ Textract.
   ![s21](/images/4/s21.png)








