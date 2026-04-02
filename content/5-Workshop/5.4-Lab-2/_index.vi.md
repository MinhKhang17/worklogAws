---
title : "Lab 2: Tạo IAM User"
date : 2026-03-25
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Tổng Quan

Trong bài lab này, bạn sẽ tạo và cấu hình các IAM user và role cho EV Data Marketplace với các quyền phù hợp để truy cập S3. IAM (Identity and Access Management) điều khiển ai có thể truy cập các tài nguyên AWS nào và các hành động nào họ có thể thực hiện.

## Mục Tiêu

1. Tạo các IAM policy cho vai trò data provider và data consumer
2. Tạo service role cho ứng dụng backend
3. Cấu hình các bucket access policies cho S3
4. Thiết lập quyền cho các hoạt động upload/download
5. Tạo IAM users cho kiểm tra và phát triển
6. Thiết lập access keys cho truy cập theo chương trình

## Yêu Cầu Tiên Quyết

- Hoàn thành Lab 1 (S3 bucket đã được tạo)
- Hiểu biết về các khái niệm IAM (users, roles, policies)
- Truy cập vào AWS IAM console

## Các Nhiệm Vụ Chính

- Tạo IAM policy: `EvDataProviderPolicy` (upload, list, describe objects)
- Tạo IAM policy: `EvDataConsumerPolicy` (download, list objects)
- Tạo IAM role: `EvDataMarketplaceServiceRole` (cho backend)
- Tạo IAM users: `provider-user` và `consumer-user` cho kiểm tra
- Tạo access keys cho truy cập theo chương trình
- Gán policies cho users và roles

## Kết Quả Mong Đợi

Các IAM users và roles được cấu hình với các policies nguyên tắc tối thiểu cho phép nhà cung cấp tải dữ liệu lên và người tiêu dùng tải xuống từ S3 bucket.