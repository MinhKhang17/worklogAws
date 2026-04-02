---
title : "Lab 1: Tạo S3 Bucket"
date : 2026-03-25
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## Tổng Quan

Trong bài lab này, bạn sẽ tạo và cấu hình một Amazon S3 bucket để lưu trữ các bộ dữ liệu cho EV Data Marketplace. Bucket này sẽ là kho lưu trữ trung tâm cho tất cả các tệp dữ liệu, metadata, và nhật ký giao dịch.

## Mục Tiêu

1. Tạo S3 bucket với quy ước đặt tên phù hợp
2. Cấu hình bucket versioning để theo dõi các thay đổi dữ liệu
3. Thiết lập cấu trúc thư mục cho datasets, metadata, và logs
4. Kích hoạt mã hóa phía máy chủ để bảo mật
5. Cấu hình cài đặt public access block
6. Thiết lập bucket policies cho điều khiển truy cập IAM

## Yêu Cầu Tiên Quyết

- Tài khoản AWS có quyền quản trị
- Truy cập AWS Management Console
- Hiểu biết cơ bản về các khái niệm S3

## Các Nhiệm Vụ Chính

- Tạo bucket: `ev-data-marketplace-datasets-{account-id}`
- Kích hoạt versioning
- Tạo các thư mục: `/datasets`, `/metadata`, `/logs`
- Cấu hình mã hóa (SSE-S3)
- Thiết lập public access blocks
- Xác định bucket policies cho truy cập IAM role

## Kết Quả Mong Đợi

Một S3 bucket an toàn, có phiên bản, sẵn sàng để lưu trữ các bộ dữ liệu marketplace với các điều khiển truy cập thích hợp.