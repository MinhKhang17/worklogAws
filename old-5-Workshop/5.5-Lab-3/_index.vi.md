---
title : "Lab 3: Tạo Cognito User Pool"
date : 2026-03-16 
weight : 5 
chapter : false
pre : " <b> 5.5. </b> "
---

## Tổng Quan

Trong bài lab này, bạn sẽ thiết lập Amazon Cognito User Pool cho xác thực và phân quyền của các người dùng EV Data Marketplace. Cognito cung cấp một cách an toàn, có khả năng mở rộng để quản lý nhận dạng người dùng và triển khai đăng nhập duy nhất (SSO).

## Mục Tiêu

1. Tạo User Pool Cognito cho xác thực
2. Cấu hình các luồng đăng ký và đăng nhập
3. Thiết lập chính sách mật khẩu và MFA (tùy chọn)
4. Tạo các nhóm người dùng cho điều khiển truy cập dựa trên vai trò
5. Cấu hình Cognito app client cho tích hợp backend
6. Thiết lập các thuộc tính người dùng cho hồ sơ provider/consumer

## Yêu Cầu Tiên Quyết

- Hoàn thành Lab 1 (S3 bucket đã được tạo)
- Hoàn thành Lab 2 (IAM users và roles đã được tạo)
- Hiểu biết về các khái niệm xác thực

## Các Nhiệm Vụ Chính

- Tạo User Pool: `ev-marketplace-user-pool`
- Cấu hình chính sách mật khẩu (độ dài, độ phức tạp)
- Kích hoạt xác minh email
- Tạo các nhóm người dùng: `DataProviders` và `DataConsumers`
- Tạo app client cho ứng dụng backend
- Cấu hình các thuộc tính tùy chỉnh (tên công ty, giấy phép kinh doanh, v.v.)
- Kiểm tra các luồng đăng ký và đăng nhập

## Kết Quả Mong Đợi

Một User Pool Cognito đầy đủ chức năng với các nhóm người dùng được cấu hình, các thuộc tính tùy chỉnh, và app client sẵn sàng để tích hợp backend.