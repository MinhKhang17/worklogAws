---
title : "Kết nối tới EC2 instance"
date : 2026-03-16
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

Bây giờ stack đã được triển khai thành công, hãy kết nối tới EC2 instance bằng giao thức remote display [NICE DCV](https://aws.amazon.com/hpc/dcv/) (RDP). NICE DCV là một giao thức hiển thị từ xa hiệu năng cao, cung cấp cho khách hàng một cách an toàn để truyền desktop từ xa và stream ứng dụng từ bất kỳ môi trường cloud hoặc data center nào tới bất kỳ thiết bị nào, ngay cả trong các điều kiện mạng khác nhau. Với NICE DCV và Amazon EC2, khách hàng có thể chạy từ xa các ứng dụng yêu cầu đồ họa cao trên EC2 instance, rồi truyền giao diện người dùng tới các máy khách đơn giản hơn, từ đó không còn cần đến các máy trạm chuyên dụng đắt tiền.

⚠️ **Warning**  
Các lệnh dòng lệnh trên trang này được viết cho máy Mac/Linux. Nếu bạn dùng Windows, bạn vẫn có thể thực hiện các bước này bằng Command Prompt hoặc PowerShell, tuy nhiên bạn cần tham khảo tài liệu dành cho Windows để tìm các lệnh tương đương.

---

1.  **Tạo file key pair**
    
    Trên AWS console, dùng thanh tìm kiếm và gõ **Parameter Store**.
    
    ℹ️ **Note**  
    Bạn cũng có thể truy cập Parameter Store bằng cách vào Systems Manager console. Bạn sẽ tìm thấy **Parameter Store** trong menu điều hướng bên trái, dưới mục **Application Management**.
    
    Tìm parameter có tên `"/ec2/keypair/key-***********"`, nhấn vào tên để mở trang chi tiết parameter.
    
    Trong trường **Value**, chọn **Show** để hiển thị RSA private key.
    
    Sao chép toàn bộ giá trị từ `"-----BEGIN RSA PRIVATE KEY-----"` đến `"-----END RSA PRIVATE KEY-----"`.
    
    ![EC2 Parameter Details](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-keypair.png)
    
    Mở terminal và tạo file key-pair bằng lệnh sau:
    
    ℹ️ **Note**  
    Bạn có thể đặt tên file tùy ý, nhưng file phải kết thúc bằng đuôi **.pem**
    
    ```bash
    touch reality-capture.pem
    ```
    
    Chỉnh sửa file này bằng lệnh sau:
    
    ```bash
    nano reality-capture.pem
    ```
    
    Sao chép và dán RSA private key từ AWS console vào file này. Sau đó lưu file bằng **Ctrl+O** --> **Enter**.
    
    Thoát nano editor bằng **Ctrl+X**.

---

2.  **Xác minh instance đã khởi chạy và sao chép địa chỉ IP**
    
    Trên AWS console, dùng thanh tìm kiếm và gõ **EC2**.
    
    Trong EC2 console, dưới mục *Resources*, nhấn vào liên kết **Instances (running)**. Bạn sẽ thấy hai instance được CloudFormation tạo ra: **rc-workshop-workstation-base-ec2** và **rc-workshop-jumpbox-ec2**.
    
    Tùy vào tốc độ cấp phát, VM của bạn có thể tạm thời hiển thị trạng thái *initializing*.
    
    Khi VM hoàn tất quá trình cấp phát, nó sẽ hiển thị trạng thái *running* với toàn bộ kiểm tra ở trạng thái **passed**.
    
    ![Instance Status Passed](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-instance-running.png)
    
    Với instance có tên **rc-workshop-workstation-base-ec2**, hãy sao chép địa chỉ IP private bằng cách nhấn vào liên kết màu xanh dưới **Instance ID**, sau đó tại trang *Instance summary*, tìm trường **Private IPv4 Address**. Dán địa chỉ này vào nơi an toàn vì bạn sẽ dùng nó ở bước tiếp theo.
    
    ![Instance Public IP](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-private-ip.png)
    
    Với jump box instance có tên **rc-workshop-jumpbox-ec2**, hãy sao chép địa chỉ IP public bằng cách nhấn vào liên kết màu xanh dưới **Instance ID**, sau đó tại trang *Instance summary*, tìm trường **Public IPv4 Address**. Dán địa chỉ này vào nơi an toàn vì bạn sẽ dùng nó ở bước tiếp theo.
    
    ✅ **Jump Box**  
    Jump server hoặc jump box là một hệ thống trong mạng dùng để truy cập và quản lý các thiết bị nằm trong một vùng bảo mật riêng biệt.
    
    ![Instance Public IP](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/public-ip.jpeg)
    
    ℹ️ **Note**  
    Tùy thuộc vào thiết lập bảo mật AWS của bạn, có thể bạn sẽ cần thêm hoặc chỉnh sửa security group trước khi kết nối tới VM. Hãy tham khảo đội ngũ IT/Bảo mật thông tin của bạn để được hướng dẫn phù hợp.

---

3.  **Thiết lập kết nối SSH**
    
    Mở terminal. Di chuyển tới thư mục chứa file key pair (.pem) mà bạn đã lưu.
    
    Đảm bảo quyền của file là 400 bằng cách chạy lệnh sau:
    
    ```bash
    chmod 400 reality-capture.pem
    ```
    
    Dùng lệnh SSH sau để kết nối vào jump box public, đồng thời mở cổng 8888 trên máy local và ánh xạ nó tới cổng 8443 trên instance private:
    
    ```bash
    ssh -i reality-capture.pem -L 8888:[INSERT PRIVATE IP SAVED IN STEP 2]:8443 ec2-user@[INSERT PUBLIC JUMPBOX IP]
    ```
    
    *Lưu ý: Khi chèn địa chỉ IP public và private vào lệnh SSH, hãy bỏ các dấu ngoặc vuông bao quanh.*
    
    Trả lời **yes** khi được hỏi. Lúc này bạn sẽ kết nối thành công tới instance và thấy hình sau trong cửa sổ terminal.
    
    ![Terminal Instance Connected](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-ssh-connected.png)

---

4.  **Kết nối tới EC2 instance**
    
    Để kết nối tới EC2 instance, chúng ta sẽ sử dụng ứng dụng NICE DCV client. Hãy làm theo [hướng dẫn cài đặt NICE DCV](https://docs.aws.amazon.com/dcv/latest/userguide/client.html) phù hợp với máy tính của bạn.
    
    Sau khi cài đặt NICE DCV client, hãy mở ứng dụng và nhập **localhost:8888**. Sau đó chọn **Connect**.
    
    Nếu bạn nhận được thông báo sau, hãy chọn **Trust and Connect**.
    
    Để tìm username và password, vào EC2 console, rồi nhấn vào instance có tên **rc-workshop-workstation-base-ec2**.
    
    Trong trang Instance summary, tìm và chọn nút **Connect** ở góc trên bên phải màn hình.
    
    Chọn tab **RDP Client**.
    
    ![RDP Connect](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-rdp-connect.png)
    
    Sao chép username (Administrator) và nhập vào màn hình đăng nhập của NICE DCV client.
    
    Giải mã và sao chép mật khẩu:
    
    * Trong mục Password, nhấn **Get password**, một màn hình mới sẽ mở ra.
    * Nhấn **Upload private key file**, tìm và chọn file key pair bạn đã tạo ở bước 1.
        * *Bạn có thể bỏ qua tên file trong mục "Key pair associated with this instance".*
    * Nhấn **Decrypt password**, sau đó mật khẩu đã giải mã sẽ xuất hiện. Sao chép và dán mật khẩu này vào NICE DCV client để hoàn tất đăng nhập.
    
    ℹ️ **Note**  
    Nếu bạn nhận được thông báo lỗi từ NICE DCV rằng không thể kết nối tới instance, hãy đảm bảo máy tính của bạn có outbound access tới địa chỉ Public hoặc Private IP trên cổng TCP 8443.
    
    Nếu thành công, màn hình desktop Microsoft Windows sẽ xuất hiện.
    
    ![RC Virtual Desktop](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-desktop.png)