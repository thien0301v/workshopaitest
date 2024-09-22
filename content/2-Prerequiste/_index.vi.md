---
title : "Chuẩn bị "
date : "`r Sys.Date()`"
weight : 2
chapter : false

---

{{% notice info %}}
Bạn cần tạo 1 tài khoản AWS để thực hiện lab này.
{{% /notice %}}

Nếu bạn chưa có tài khoản AWS với quyền truy cập Administrator, hãy tạo ngay bây giờ.
  - [Tạo tài khoản AWS](https://aws.amazon.com/vi/getting-started/)

### **Triển khai CloudFormation Stack**
1. Tải xuống AWS CloudFormation bằng nút "Download Template" bên dưới và sử dụng nó trong bảng điều khiển AWS CloudFormation. [Download Template](https://idp-assets-wwso.s3.us-east-2.amazonaws.com/cfn/idp-workshop-templates.zip).
 ![stack](/images/2.prerequisite/yaml-stack.png)

2. Tìm kiếm "Cloud Formation" 
   ![search](/images/2.prerequisite/search.png)
3. Tạo "stack" và chọn "With new resources (standard)"
   ![create](/images/2.prerequisite/create.png)
4. Trong phần chuẩn bị template, chọn "Choose an existing template", tại phần Specify template, chọn "Upload a template file"
   ![create](/images/2.prerequisite/create1.png)
Và nhấn "Next"
5. Đặt tên cho stack là "IDPSageMakerCfnStack", các tham số để mặc định
   ![name](/images/2.prerequisite/name.png)
Và nhấn "Next"
6. Step 4: Review and Create
  ![step4](/images/2.prerequisite/step4.png)
7. Chờ quá trình thực thi hoàn tất, bạn sẽ thấy kết quả như sau:
 ![complete](/images/2.prerequisite/complete.png)

##### Sau khi CloudFormation stacks được triển khai, hãy làm theo các hướng dẫn dưới đây để truy cập vào Amazon SageMaker Studio IDE.

### Truy cập Amazon SageMaker Studio
1. Tìm kiếm "SageMaker"
   ![sage](/images/2.prerequisite/sage.png)
2. Bạn sẽ thấy trang Domains, nếu không, nhấp vào tùy chọn Domains trong menu bên trái. Tiếp theo, nhấp vào tên Domain.
     >Note: nếu bạn đã thay đổi tên miền của mình trong mẫu CloudFormation, thì tên đó sẽ được hiển thị trong danh sách.
     ![domain](/images/2.prerequisite/sagedomain.png)
3. Trong trang **Domain details** nhấp vào menu thả xuống Launch và chọn **Studio**
   ![studio](/images/2.prerequisite/studio.png)
4. **SageMaker Studio IDE** sẽ mở ra trong một tab mới của trình duyệt. Trang có thể mất vài phút để tải khi bạn truy cập vào **SageMaker Studio** lần đầu tiên. Khi giao diện **SageMaker Studio IDE** tải xong, bạn sẽ thấy màn hình như bên dưới. Nhấp vào **"Studio Classic"** (trên menu bên trái gần đầu).
   ![studioclassic](/images/2.prerequisite/studioclassic.png)
5. Bạn sẽ thấy một ứng dụng **SageMaker Studio classic** đang chạy. Nhấp vào **"Open"**.
   ![open](/images/2.prerequisite/openclassic.png)
6. Bạn sẽ được chuyển hướng đến một tab trình duyệt mới với **Amazon SageMaker Studio Classic IDE**:
    ![jupy](/images/2.prerequisite/jupyterlab.png)
7. Khi bạn đã ở trong **Amazon SageMaker Studio IDE**, bạn sẽ thấy thư mục kho lưu trữ workshop.
   ![repo](/images/2.prerequisite/repo.png)