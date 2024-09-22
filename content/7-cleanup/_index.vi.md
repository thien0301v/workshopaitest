+++
title = "Dọn dẹp tài nguyên"
date = 2022
weight = 6
chapter = false
+++

WChúng ta sẽ thực hiện các bước sau để xóa các tài nguyên đã tạo trong bài tập này.

- Đi tới notebook `05-idp-cleanup.ipynb` và làm theo các ô mã để xóa các tài nguyên đã tạo trong tài khoản.
   ![s1](/images/7/s1.png)
   ![s2](/images/7/s2.png)
- Truy cập **Amazon Comprehend** console để xác minh xem tất cả các endpoint và mô hình đã bị xóa.
   ![s3](/images/7/s3.png)
- Truy cập Amazon S3 console, điều hướng đến bucket có tên ``sagemaker-studio<xxxxxxx>`` và ``idp-a2i-xxxxxx``, và xác minh xem mọi thứ trong các bucket đã bị xóa.
- Truy cập **CloudFormation** và xóa
   ![s4](/images/7/s4.png)
  

