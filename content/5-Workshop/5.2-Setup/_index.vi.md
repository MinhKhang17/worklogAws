---
title : "Thiết lập Workstation"
date : 2026-03-16 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

✅ **Thời gian triển khai ước tính:** 20 phút

ℹ️ **Các thực hành bảo mật tốt nhất**
Các tài nguyên AWS và đoạn mã được triển khai trong workshop này nên được xóa ngay sau khi bạn hoàn thành workshop. Chúng tôi đã cung cấp hướng dẫn trong tài liệu này để hỗ trợ bạn thực hiện việc đó (xem phần *Cleanup*). Nếu bạn chọn sử dụng nội dung của workshop này làm nền tảng cho các ứng dụng production của riêng mình, hãy đảm bảo áp dụng các thực hành bảo mật tốt nhất cho từng dịch vụ liên quan. Bạn có thể tìm thấy các hướng dẫn bảo mật trong mục “Security” của Developer Guide cho từng dịch vụ, thường nằm trong tiểu mục có tên “Security Best Practices”. Xem [https://docs.aws.amazon.com/security/](https://docs.aws.amazon.com/security/) để truy cập nhanh tới tài liệu phù hợp.

---

## Ghi chú quan trọng

1. Khi sử dụng NICE DCV client, bạn có thể nhận được thông báo `'No license available'`. Bạn không cần giấy phép riêng cho Reality Capture Virtual Desktop. NICE DCV server sẽ tự động phát hiện rằng nó đang chạy trên Amazon EC2 instance và định kỳ kết nối để xác minh giấy phép. Bạn có thể bỏ qua thông báo này một cách an toàn.

2. Có thể sẽ xuất hiện thông báo cho biết không tìm thấy NVIDIA Control Panel. Bạn có thể yên tâm bỏ qua thông báo này vì nó sẽ không ảnh hưởng đến hiệu năng hoặc chức năng của hệ thống.