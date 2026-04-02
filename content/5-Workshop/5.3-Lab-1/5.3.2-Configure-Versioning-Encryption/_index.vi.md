---
title : "5.3.2 - Cấu Hình Versioning & Encryption"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

## Hướng Dẫn Từng Bước: Cấu Hình Bucket Versioning và Encryption

### Mục Tiêu
Kích hoạt versioning để theo dõi các thay đổi bộ dữ liệu và cấu hình mã hóa phía máy chủ để bảo vệ dữ liệu nhạy cảm.

---

## Phần A: Kích Hoạt Bucket Versioning

### Bước 1: Truy Cập Thuộc Tính Bucket

1. Trong dashboard S3, xác định vị trí bucket `ev-data-marketplace-datasets-xxxxx` của bạn
2. Nhấp vào tên bucket để mở nó
3. Nhấp vào tab **Properties** ở phía trên

![S3 bucket properties tab](/images/5-Workshops/lab1/step1.png)

---

### Bước 2: Điều Hướng Đến Versioning

1. Cuộn xuống trong tab Properties
2. Tìm phần **Bucket Versioning**
3. Nhấp vào nút **Edit**

![Bucket Versioning section](/images/5-Workshops/lab1/step2.png)

---

### Bước 3: Kích Hoạt Versioning

1. Chọn tùy chọn **Enable**
2. Nhấp vào nút **Save changes**
3. Bạn sẽ thấy: "Bucket versioning status has been updated"

![Enable versioning confirmation](/images/5-Workshops/lab1/step3.png)

---

### Bước 4: Xác Minh Versioning

1. Quay lại properties bucket
2. Xác nhận trạng thái **Versioning** hiển thị: **Enabled**
3. Điều này cho phép bạn khôi phục các phiên bản trước của các tệp bộ dữ liệu

![Versioning status enabled](/images/5-Workshops/lab1/step4.png)

---

## Phần B: Cấu Hình Mã Hóa Phía Máy Chủ

### Bước 5: Truy Cập Cài Đặt Encryption

1. Trong tab **Properties**, cuộn để tìm phần **Encryption**
2. Nhấp vào nút **Edit** trong phần Encryption

![Encryption section](/images/5-Workshops/lab1/step5.png)

---

### Bước 6: Cấu Hình Loại Encryption

1. Chọn **Server-side encryption with Amazon S3-managed keys (SSE-S3)**
   - Đây là phương pháp mã hóa mặc định được khuyến nghị
   - Không có chi phí bổ sung
   - Khóa được quản lý bởi AWS

2. KHÔNG chọn **SSE-KMS** (yêu cầu thiết lập KMS bổ sung)

![Encryption type selection](/images/5-Workshops/lab1/step6.png)

---

### Bước 7: Kích Hoạt Default Encryption

1. Đánh dấu hộp: **Enable default encryption**
2. Loại encryption: Đảm bảo **SSE-S3** được chọn
3. Nhấp vào nút **Save changes**

![Default encryption enabled](/images/5-Workshops/lab1/step7.png)

---

### Bước 8: Xác Minh Encryption

1. Quay lại Properties bucket
2. Xác nhận **Encryption** hiển thị: **Enabled (SSE-S3)**
3. Tất cả các objects được tải lên sẽ được mã hóa theo mặc định

![Encryption status confirmed](/images/5-Workshops/lab1/step8.png)

---

## Phần C: Kích Hoạt Block Public Access (Thực Tiễn Tốt Nhất Về Bảo Mật)

### Bước 9: Truy Cập Block Public Access

1. Ở trong tab **Properties**
2. Cuộn để tìm phần **Block Public Access**
3. Nhấp vào nút **Edit**

![Block Public Access section](/images/5-Workshops/lab1/step9.png)

---

### Bước 10: Cấu Hình Giới Hạn Truy Cập

1. Đảm bảo tất cả bốn tùy chọn được **Kích Hoạt**:
   - Block public access to buckets and objects granted through new access control lists (ACLs)
   - Block public access to buckets and objects granted through any access control lists (ACLs)
   - Block public access to buckets and objects granted through new public bucket or access point policies
   - Block public access to buckets and objects granted through any public bucket or access point policies

2. Nhấp vào nút **Save changes**


---

### Bước 11: Xác Minh Cài Đặt Bảo Mật

1. Xác nhận tất cả các tùy chọn blocking hiển thị là **On**
2. Bucket của bạn hiện được bảo vệ khỏi truy cập công khai không được phép


---

## Tóm Tắt

Bạn đã cấu hình thành công bucket S3 của mình với:
-  **Versioning Kích Hoạt:** Theo dõi và khôi phục các phiên bản bộ dữ liệu trước
-  **Mã Hóa Phía Máy Chủ (SSE-S3):** Bảo vệ dữ liệu khi đang lưu
-  **Truy Cập Công Khai Bị Chặn:** Ngăn chặn truy cập trái phép
-  **Các Thực Tiễn Tốt Nhất Về Bảo Mật Được Áp Dụng**

**Nhiệm Vụ Tiếp Theo:** Thiết lập cấu trúc thư mục để tổ chức các bộ dữ liệu
