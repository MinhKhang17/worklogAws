---
title : "Dọn dẹp tài nguyên"
date : 2026-03-16
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

⚠️ **Dừng instance khi không sử dụng**

Bạn có thể **dừng (stop) các EC2 instance** để tránh phát sinh chi phí mà không cần xóa toàn bộ stack. Chỉ cần vào **EC2 Console**, sau đó chọn **Stop instance** trong menu thả xuống **Instance state**.

Sau khi dừng instance, bạn sẽ **không còn bị tính phí sử dụng hoặc phí truyền dữ liệu** cho instance đó. Tuy nhiên, bạn vẫn sẽ bị tính phí cho các tài nguyên liên quan, chẳng hạn như **EBS volumes được gắn kèm** và **Elastic IP addresses** liên kết với instance.

---

**Thực hiện theo các bước sau để xóa toàn bộ tài nguyên AWS đã tạo trong workshop này.**

1. **Xóa stack: Phần 1**
    
    Trên **AWS Console**, vào **CloudFormation** và mở trang **Stacks**.
    
    Chọn nút radio (dial) hoặc nhấp vào tên stack, sau đó nhấn nút **Delete**. Thao tác này sẽ xóa tất cả tài nguyên ngoại trừ **S3 bucket**.
    
    Sau khi hoàn tất, bạn sẽ thấy thông báo sau:  
    *Delete Failed: The following resource(s) failed to delete: [S3Bucket]*
    
    ![RC Stack Delete Failed](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-delete-failed.png)

---

2. **Xóa stack: Phần 2**
    
    (Tùy chọn) Trước khi thực hiện bước này, bạn có thể tải xuống nội dung của **S3 bucket** trong workshop để lưu lại kết quả làm việc.
    
    Trên **AWS Console**, vào **S3** và mở **workshop bucket**.
    
    Xóa từng thư mục con: chọn checkbox bên cạnh **cả ba thư mục**, sau đó nhấn **Delete**. Làm theo hướng dẫn trên màn hình để xác nhận việc xóa.
    
    Quay lại **CloudFormation Console**, mở **workshop stack**. Sau đó nhấn **Delete** một lần nữa để hoàn tất việc xóa stack.
    
    Bạn sẽ thấy thông báo thành công cuối cùng:
    
    ![RC Stack Delete Success](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-delete-complete.png)

---

✅ **Workshop hoàn thành**