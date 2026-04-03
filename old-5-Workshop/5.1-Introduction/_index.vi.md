---
title : "Giới thiệu về Marketplace Dữ Liệu Xe Điện"
date : 2026-03-25 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

## Tổng Quan Dự Án

**EV Data Marketplace** là nền tảng thương mại điện tử dữ liệu chuyên biệt cho ngành xe điện (Electric Vehicle). Dự án cho phép các nhà cung cấp dữ liệu (Data Providers) như nhà sản xuất, công ty vận hành sạc, hãng bảo hiểm, và các tổ chức nghiên cứu có thể đăng ký, xác thực, quản lý quyền truy cập và bán các bộ dữ liệu về xe điện cho các khách hàng (Data Consumers).

---

## Các Thành Phần Chính

Dự án sử dụng các dịch vụ AWS chính để xây dựng một hệ thống an toàn, mạnh mẽ và có khả năng mở rộng:

- **Amazon S3 (Simple Storage Service)** – Lưu trữ tất cả các bộ dữ liệu, tệp metadata, và các tài liệu liên quan
- **AWS IAM (Identity and Access Management)** – Quản lý quyền truy cập từng người dùng, định nghĩa bucket policies, và điều khiển ai có thể truy cập dữ liệu nào
- **Amazon Cognito** – Xác thực người dùng, quản lý hồ sơ (user profiles) và kiểm soát truy cập dựa trên vai trò (role-based access control)

---

## Khái Niệm Chính

### Vai Trò Người Dùng

- **Data Provider** – Tạo, tải lên, và quản lý bộ dữ liệu về xe điện (ví dụ: dữ liệu sạc, thông số hiệu năng pin, thông tin vị trí)
- **Data Consumer** – Tìm kiếm, mua, và tải xuống các bộ dữ liệu khác phục vụ cho phân tích, nghiên cứu, hoặc phát triển sản phẩm
- **Admin** – Quản lý người dùng, xóa duyệt bộ dữ liệu, xử lý tranh chấp, và duy trì sức khỏe hệ thống

### Quy Trình Cơ Bản

1. **Đăng ký & Xác thực** – Người dùng đăng ký tài khoản qua Cognito, tạo hồ sơ và định rõ vai trò (provider hoặc consumer)
2. **Tải lên Dữ liệu** – Data provider tải dữ liệu lên S3 với metadata mô tả (tiêu đề, mô tả, giá cả, phiên bản)
3. **Quản lý Quyền Truy Cập** – IAM quản lý quyền truy cập dữ liệu dựa trên vai trò, người dùng, và bộ dữ liệu
4. **Mua & Tải xuống** – Data consumer duyệt catalog, mua bộ dữ liệu, và tải xuống từ S3 với quyền tạm thời

### Loại Dữ Liệu

Marketplace hỗ trợ các loại dữ liệu về xe điện như:

- **Dữ liệu Hiệu Năng Pin** – Dung lượng, tuổi thọ, tốc độ phóng điện, nhiệt độ
- **Dữ liệu Sạc** – Thời gian sạc, địa điểm sạc, mức năng lượng
- **Dữ liệu Kinh Tế** – Tiêu thụ điện năng, chi phí vận hành, so sánh giá xăng
- **Dữ liệu Bản Đồ** – Vị trí, lộ trình, khoảng cách từ sạc

---

## Mục Tiêu Workshop

Trong workshop này, bạn sẽ:

1. Thiết lập môi trường AWS với S3, IAM, và Cognito
2. Tạo ứng dụng backend để quản lý người dùng, bộ dữ liệu, và giao dịch
3. Cấu hình xác thực qua Cognito với role-based access control
4. Triển khai API để quản lý tập tin S3 và quyền truy cập
5. Thử nghiệm luồng provider/consumer từ upload đến download

**Thời gian dự kiến:** 3-4 giờ | **Region:** `us-east-1`