---
title : "Triển khai CloudFormation Template"
date : 2026-03-16 
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---

[AWS CloudFormation](https://aws.amazon.com/cloudformation/) cho phép bạn mô hình hóa, cấp phát và quản lý tài nguyên AWS cũng như tài nguyên bên thứ ba bằng cách xem hạ tầng như mã nguồn (infrastructure as code). Trong bước này, chúng ta sẽ triển khai một CloudFormation stack để cấp phát VPC, EC2 instance và S3 bucket.

---

1.  **Tải file template và tạo stack mới**
    
    Tải [CloudFormation template](https://ws-assets-prod-iad-r-cmh-8d6e9c21a4dec77d.s3.us-east-2.amazonaws.com/e26c223d-6107-4ca8-a3c1-d8da486d7ea2/rc-workstation.yaml) sau đây.
    
    Sau đó, đăng nhập vào tài khoản AWS của bạn và mở CloudFormation console.
    
    Trên CloudFormation console, nhấn **Create Stack** -> **With new resources (standard)**.

---

2.  **Tải template lên CloudFormation console**
    
    Trong phần **Specify Template**, chọn tùy chọn **Upload a template file**, rồi tải lên file ở bước 1. Sau đó nhấn **Next**.
    
    ![CFN Upload Template](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-cfn-create-stack.png)

---

3.  **Thiết lập thông tin stack**
    
    Nhập **Stack name** mà bạn muốn sử dụng, hoặc có thể dùng **rc-workshop**.
    
    * *Tên stack có thể bao gồm chữ cái (A-Z và a-z), số (0-9) và dấu gạch ngang (-).*
    
    Cung cấp các thông tin sau trong phần **Parameters**:
    
    * **Availability Zone**
        * Chọn **một** Availability Zone để sử dụng cho VPC.
        * *Lưu ý: Bạn có thể chọn bất kỳ Availability Zone nào trong danh sách xổ xuống.*
    * **VPC CIDR**
        * CIDR block dành cho VPC.
        * Vui lòng nhập hai octet đầu tiên của CIDR block. Template sẽ tự hoàn thiện phần còn lại của block cho các subnet.
        * *Lưu ý: Bạn có thể giữ tùy chọn mặc định (10.5) cho CIDR block, tuy nhiên hãy đảm bảo block này chưa được sử dụng.*
    * **Endpoint Device IP Address**
        * Nhập địa chỉ IP public của thiết bị đầu cuối sẽ dùng để kết nối tới Windows Server instance. Ví dụ: `128.128.128.128`.
        * Bạn cũng có thể nhập `0.0.0.0` để cho phép mọi IP, nhưng không được khuyến nghị.
    * **Desktop Instance Size**
        * Bạn có thể dùng bất kỳ loại instance nào trong danh sách xổ xuống để hoàn thành workshop này.
        * Loại instance G5 lớn nhất sẽ hoàn thành công việc nhanh nhất, nhưng cũng tốn chi phí nhất.
    * **Jump box Instance Size**
        * *Lưu ý: Jump server hoặc jump box là một hệ thống trong mạng được dùng để truy cập và quản lý các thiết bị ở một vùng bảo mật riêng biệt.*
    
    Nhấn **Next**.

---

4.  **Tạo stack**
    
    Trong trang **Configure stack options**, giữ nguyên toàn bộ thiết lập mặc định. Kéo xuống cuối trang và nhấn **Next**.
    
    Cuối cùng, xem lại thông tin stack bạn đã nhập ở bước 3.
    
    Tích chọn ô *"I acknowledge that AWS CloudFormation might create IAM resources"* rồi nhấn **Submit**.
    
    Quá trình triển khai thường mất khoảng **3-5 phút**.

---

5.  **Xác nhận triển khai thành công**
    
    Tab **Events** lúc này sẽ được hiển thị, cung cấp trạng thái tạo stack. Nhấn biểu tượng làm mới để cập nhật màn hình và xem tiến trình mới nhất.
    
    Nếu quá trình tạo instance/stack thành công, thông báo sau sẽ xuất hiện.
    
    ![Stack Create Complete](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-stack-complete.png)

⚠️ **Stack Failure**  
Các nguyên nhân phổ biến khiến việc tạo stack thất bại là loại instance được yêu cầu hiện không sẵn sàng để cấp phát, hoặc tài khoản đang sử dụng không có quyền khởi tạo các instance có hỗ trợ GPU. Vui lòng liên hệ đội ngũ IT và/hoặc bộ phận hỗ trợ kỹ thuật của Amazon để được hướng dẫn phù hợp.