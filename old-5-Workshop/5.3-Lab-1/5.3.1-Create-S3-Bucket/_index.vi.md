---
title : "5.3.1 - Tạo S3 Bucket"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

## Hướng Dẫn Từng Bước: Tạo S3 Bucket

### Mục Tiêu
Tạo một S3 bucket sẽ đóng vai trò là nơi lưu trữ trung tâm cho tất cả các bộ dữ liệu, metadata, và nhật ký giao dịch của EV Data Marketplace.

---

## Bước 1: Mở AWS Management Console

1. Truy cập [AWS Management Console](https://aws.amazon.com/console/)
2. Đăng nhập bằng thông tin tài khoản AWS của bạn
3. Đảm bảo bạn đang ở region **us-east-1** (hiển thị ở góc trên cùng bên phải)

![Trang chủ AWS Management Console](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113457.png)

---

## Bước 2: Điều Hướng Đến Dịch Vụ S3

1. Trong thanh tìm kiếm ở đầu trang, gõ **S3**
2. Nhấp vào **S3** từ kết quả dropdown
3. Dashboard S3 sẽ tải (hiển thị danh sách buckets)

![Dashboard S3 hiển thị danh sách buckets](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113517.png)

---

## Bước 3: Tạo Bucket Mới

1. Nhấp vào nút **Create bucket** (nút màu cam)
2. Bạn sẽ được chuyển hướng đến biểu mẫu tạo bucket

![Nút Create bucket được tô sáng](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113537.png)

---

## Bước 4: Cấu Hình Tên Bucket

1. Trong trường **Bucket name**, nhập:
   ```
   ev-data-marketplace-datasets-<your-account-id>
   ```
   Ví dụ: `ev-data-marketplace-datasets-123456789012`
   
   > **Lưu ý:** Tên S3 bucket phải là duy nhất trên toàn cầu và tuân theo các quy tắc:
   > - Dài 3-63 ký tự
   > - Chỉ các chữ cái thường, số, và dấu gạch ngang
   > - Không bắt đầu hoặc kết thúc bằng dấu gạch ngang
   > - Không có dấu gạch dưới hoặc chữ cái in hoa

2. **Region:** Xác minh nó được đặt thành **us-east-1**

![Biểu mẫu cấu hình tên bucket](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113557.png)

---

## Bước 5: Xem Lại Cài Đặt Bucket

1. Giữ nguyên các mặc định sau:
   - **Copy settings from existing bucket:** Để không được chọn
   - **ACLs disabled (Recommended)** được chọn

2. Để các tùy chọn khác ở mặc định hiện tại

![Cài đặt bucket với giá trị mặc định](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113617.png)

---

## Bước 6: Tạo Bucket

1. Cuộn xuống dưới cùng của biểu mẫu
2. Nhấp vào nút **Create bucket**
3. Bạn sẽ thấy thông báo thành công: "Successfully created bucket 'ev-data-marketplace-datasets-xxxxx'"

![Thông báo thành công sau khi tạo bucket](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113637.png)

---

## Bước 7: Xác Minh Tạo Bucket

1. Quay lại dashboard S3
2. Bạn sẽ thấy bucket mới của mình trong danh sách buckets
3. Nhấp vào tên bucket để mở nó
4. Bucket hiện đã sẵn sàng cho cấu hình

![Bucket mới được tạo có thể nhìn thấy trong danh sách S3](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113907.png)

---


**Nhiệm Vụ Tiếp Theo:** Cấu hình versioning và encryption
