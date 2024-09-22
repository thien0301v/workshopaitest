---
title : "Trích xuất và làm phong phú tài liệu"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
---
>⚠️ YÊU CẦU TIÊN QUYẾT: Để thực hiện notebook này, hãy chắc chắn rằng bạn đã hoàn thành notebook đầu tiên `01-idp-document-classification.ipynb`
### Tổng quan
Tính đến thời điểm này, trong hai mô-đun trước, chúng ta đã phân loại tài liệu và xác định các tài liệu sao kê ngân hàng, hóa đơn và biên lai. Trong mô-đun này, chúng ta sẽ xem xét các thực thể mặc định của Amazon Comprehend và cũng sẽ đào tạo một bộ nhận diện thực thể tùy chỉnh của Amazon Comprehend và triển khai một endpoint với nó. Mục đích của bộ nhận diện thực thể tùy chỉnh là xác định các thực thể cụ thể và tạo ra siêu dữ liệu tùy chỉnh về tài liệu của chúng ta dưới định dạng CSV để sau này được phân tích theo trường hợp sử dụng kinh doanh. Ngoài ra, chúng ta cũng muốn xác định bất kỳ số tài khoản tiết kiệm và tài khoản kiểm tra nào trong các sao kê ngân hàng và thực hiện việc che đi chúng.
   ![arch2](/images/4/arch2.png)

### Nhận diện thực thể tên (NER) là gì?
Nhận diện thực thể tên (NER) là một nhiệm vụ con trong xử lý ngôn ngữ tự nhiên (NLP) liên quan đến việc sàng lọc qua dữ liệu văn bản để xác định các cụm danh từ gọi là thực thể tên và phân loại mỗi thực thể với một nhãn, chẳng hạn như người, tổ chức hoặc thương hiệu. Ví dụ, trong câu "Gần đây tôi đã đăng ký Amazon Prime", "Amazon Prime" là thực thể tên và có thể được phân loại là một thương hiệu.

### Bắt đầu
Mở notebook `03-idp-document-enrichment.ipynb` và làm theo các bước dưới đây.
   ![s1](/images/5/s1.png)
### Bước 1: Thiết lập notebook
Trong bước này, chúng ta sẽ nhập một số thư viện cần thiết sẽ được sử dụng trong suốt notebook này.
   ![s2](/images/5/s2.png)
### Bước 2: Thực hiện Nhận diện Thực thể Tên bằng Amazon Comprehend
Chúng ta đã phân loại tài liệu của mình theo các loại tài liệu tương ứng và lưu chúng vào S3. Tiếp theo, chúng ta sẽ thực hiện nhận diện thực thể cho 1 sao kê ngân hàng và 1 biên lai bằng cách sử dụng Amazon Comprehend NER; trong trường hợp này, Comprehend sẽ trích xuất các loại thực thể chung được xây dựng sẵn từ các tài liệu.

Chúng ta sẽ bắt đầu bằng cách tải văn bản tài liệu đã trích xuất từ S3 vào một dataframe và sau đó sử dụng API DetectEntities của Amazon Comprehend.
   ![s3](/images/5/s3.png)
Thực hiện trích xuất thực thể trên Sao kê Ngân hàng.

Bạn có thể thấy nhiều thực thể trong văn bản từ sao kê ngân hàng mẫu của chúng ta. Lưu ý rằng đây là các thực thể mặc định mà Amazon Comprehend đã phát hiện bằng cách sử dụng bộ nhận diện thực thể được đào tạo trước.

   ![s4](/images/5/s4.png)

Mặc dù việc trích xuất thực thể hoạt động khá tốt trong việc xác định các loại thực thể chung cho mọi thứ trong tài liệu, chúng ta cần các thực thể cụ thể được nhận diện cho trường hợp sử dụng của mình. Cụ thể, chúng ta cần xác định số tài khoản tiết kiệm và tài khoản kiểm tra của khách hàng; ví dụ, chúng ta muốn các loại thực thể là "CHECKING_AC" và "SAVINGS_AC".

Bộ nhận diện thực thể được xây dựng trước của Amazon Comprehend không nhận thức được các loại thực thể này, vì vậy chúng ta sẽ cần đào tạo và sử dụng một bộ nhận diện thực thể tùy chỉnh trong notebook này. Chúng ta cũng sẽ thực hiện một số làm phong phú tài liệu; ví dụ, trong sao kê ngân hàng, chúng ta muốn che đi số tài khoản của khách hàng. Chúng ta sẽ thảo luận thêm và thực hiện tất cả những điều này trong notebook tiếp theo.
### Bước 3: Đào tạo bộ nhận diện thực thể tùy chỉnh Amazon Comprehend
Chúng ta sẽ đào tạo một bộ nhận diện thực thể tùy chỉnh của Amazon Comprehend. Có hai cách để đào tạo một bộ nhận diện tùy chỉnh:

- [Using Annotations](https://docs.aws.amazon.com/comprehend/latest/dg/cer-annotation.html)
- [Using Entity Lists](https://docs.aws.amazon.com/comprehend/latest/dg/cer-entity-list.html)
Ghi chú sử dụng một tập hợp lớn các tệp PDF đã được chú thích. Những chú thích này có thể được tạo ra bằng dịch vụ như Amazon Ground Truth, nơi các nhân viên thực sự có thể xem xét các tệp của bạn và chú thích chúng. Phương pháp này khá phức tạp và nếu bạn muốn tìm hiểu thêm, hãy tham khảo blog này và blog này.

Trong trường hợp của chúng ta, chúng ta sẽ sử dụng Danh sách Thực thể, là một tệp CSV chứa các văn bản và loại thực thể tương ứng của chúng. Các thực thể trong tệp này sẽ được xác định cụ thể theo nhu cầu kinh doanh của chúng ta. Để phục vụ cho bài tập này, chúng ta đã cung cấp một danh sách thực thể dưới định dạng CSV trong thư mục `/entity-training/` có tên là `entitylist.csv`. Tệp này chứa loại thực thể tùy chỉnh cho số tài khoản của khách hàng. Chúng ta đã sử dụng CHECKING_AC và SAVINGS_AC làm các loại thực thể tùy chỉnh. Với điều này, chúng ta cuối cùng cần bộ nhận diện thực thể tùy chỉnh nhận diện các số tài khoản tiết kiệm và tài khoản kiểm tra.

Hãy xem danh sách thực thể của chúng ta.
   ![s5](/images/5/s5.png)
Hãy đào tạo một bộ nhận diện thực thể tùy chỉnh với Amazon Comprehend. Để đào tạo một bộ nhận diện thực thể tùy chỉnh, chúng ta sẽ cần danh sách thực thể và tập hợp các tài liệu để đào tạo mô hình. Chúng ta sẽ sử dụng cùng một tập hợp tài liệu mà chúng ta đã sử dụng trước đó để đào tạo bộ phân loại tùy chỉnh cho mục đích này.

Mỗi thực thể tùy chỉnh cần ít nhất 100 mẫu trong tập dữ liệu (các tài liệu) để phục vụ cho mục đích đào tạo, có nghĩa là bạn nên có ít nhất 100 tài liệu chứa các ví dụ về mỗi thực thể tùy chỉnh trong tập dữ liệu đào tạo của bạn. Ngoài ra, cần tối thiểu 250 sự trùng khớp thực thể cho mỗi thực thể trong danh sách thực thể để đào tạo một mô hình cho nhận diện thực thể tùy chỉnh. Chúng ta đã cung cấp một tập dữ liệu đào tạo có tên `entity_training_corpus.csv` có thể được sử dụng để đào tạo bộ nhận diện thực thể cùng với danh sách thực thể. Lưu ý rằng tập dữ liệu này được tạo ra theo cách tương tự như cách mà chúng ta đã tạo dữ liệu đào tạo cho việc đào tạo bộ phân loại tùy chỉnh trong notebook đầu tiên. Với hai tập dữ liệu này, chúng ta sẽ sử dụng API `CreateEntityRecognizer` của Amazon Comprehend.

   ![s6](/images/5/s6.png)

Bây giờ hãy đào tạo một bộ nhận diện thực thể tùy chỉnh với dữ liệu này và danh sách thực thể về số tài khoản tiết kiệm và kiểm tra.
   ![s7](/images/5/s7.png)
Kiểm tra trạng thái của công việc bộ nhận diện thực thể tùy chỉnh Comprehend
   ![s8](/images/5/s8.png)

### Bước 4: Tạo endpoint bộ nhận diện thực thể tùy chỉnh theo thời gian thực
Chúng ta sẽ tạo một điểm cuối bộ nhận diện thực thể theo thời gian thực với bộ nhận diện thực thể đã được đào tạo.
   ![s9](/images/5/s9.png)
Khi đã được tạo, điểm cuối này có thể được tìm thấy trong bảng điều khiển Amazon Comprehend.
   ![s10](/images/5/s10.png)
   ![s11](/images/5/s11.png)
### Document Enrichment 1
Bây giờ chúng ta đã có một điểm cuối bộ nhận diện thực thể theo thời gian thực, bằng cách sử dụng nó, chúng ta có thể trích xuất các thực thể tùy chỉnh từ một trong các tài liệu sao kê ngân hàng của mình.
   ![s11](/images/5/idp-custom-entity.png)
Bây giờ, thay vì trả về các thực thể chung, Amazon Comprehend đang trả về cho chúng ta các thực thể từ tài liệu quét mà chúng ta quan tâm, tức là số tài khoản kiểm tra và tiết kiệm.
   ![s12](/images/5/s12.png)

### Enrichment 2: Thực hiện việc che đi thông tin trong tài liệu
Chúng ta vẫn cần thực hiện một số làm phong phú trên tài liệu. Vì tài liệu chứa số tài khoản tiết kiệm và tài khoản kiểm tra của khách hàng, chúng ta muốn che đi những thông tin này. Vì chúng ta đã biết, thông qua thực thể tùy chỉnh của mình, số tài khoản tiết kiệm và tài khoản kiểm tra của khách hàng, chúng ta có thể dễ dàng sử dụng dữ liệu hình học của **Amazon Textract** để che đi thông tin đó ở bất cứ đâu trong tài liệu.
   ![s11](/images/5/idp-redaction.png)

Chúng ta sẽ chọn một sao kê ngân hàng từ danh sách tài liệu của mình, lấy vị trí S3 của tài liệu và thực hiện các hành động sau:
- Sử dụng **Amazon Textract** để lấy thông tin hình học, tức là các hộp bao quanh, của tất cả các dòng trong tài liệu.
- Sử dụng văn bản đã trích xuất ở trên để xác định các thực thể `CHECKING_AC` và `SAVINGS_AC`, bằng cách sử dụng bộ nhận diện thực thể tùy chỉnh của Comprehend.
- Tìm hộp bao quanh cho các từ `CHECKING_AC` và `SAVINGS_AC` từ phản hồi của Textract.
- Sử dụng dữ liệu hình học của hộp bao quanh để chú thích tài liệu và che đi tên và địa chỉ của khách hàng.
   ![s13](/images/5/s13.png)

Hàm trên tìm các thực thể tùy chỉnh trong tài liệu, tìm thông tin hình học tương ứng của văn bản thực thể tùy chỉnh và thực hiện việc che đi thông tin trong tài liệu. Hãy gọi hàm này cho một sao kê ngân hàng mẫu.
   ![s14](/images/5/s14.png)
Khi tệp đã được che đi được tạo ra, hãy cùng xem nó...
   ![s15](/images/5/s15.png)
   ![s14](/images/5/redacted-doc.png)
Như bạn có thể thấy, các số tài khoản kiểm tra và tiết kiệm đã được ẩn trong tài liệu.

### Kết luận
Trong notebook này, chúng ta đã đào tạo một bộ nhận diện thực thể tùy chỉnh của Amazon Comprehend bằng cách sử dụng danh sách thực thể của riêng mình để có thể trích xuất những thực thể đó từ các tài liệu. Chúng ta đã sử dụng 2 thực thể `CHECKING_AC` và `SAVINGS_AC`. Sau đó, chúng ta đã tạo một điểm cuối với bộ nhận diện thực thể tùy chỉnh và thực hiện `detect_entities` với điểm cuối đó trên một trong các sao kê ngân hàng. Cuối cùng, chúng ta đã lưu các thực thể đã trích xuất vào một tệp CSV và tải lên S3 để phân tích thêm.

Chúng ta vẫn cần thực hiện một số làm phong phú trên tài liệu. Vì tài liệu chứa số tài khoản kiểm tra và tiết kiệm của khách hàng, chúng ta muốn che đi những thông tin đó. Với việc đã biết số tài khoản kiểm tra và tiết kiệm của khách hàng thông qua thực thể tùy chỉnh, chúng ta đã sử dụng dữ liệu hình học của Amazon Textract để che đi thông tin đó trong tài liệu.




   






