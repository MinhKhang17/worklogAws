---
title : "Dọn dẹp tài nguyên"
date : 2026-03-25
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

Thực hiện các bước sau để dọn dẹp toàn bộ tài nguyên đã tạo trong bài lab nhằm tránh phát sinh chi phí không cần thiết.

1.  Truy cập [AWS S3 Console](https://s3.console.aws.amazon.com/s3/home) và xóa S3 bucket đã tạo trong lab (`ev-data-marketplace-datasets-xxxxx`).  
    Bạn cần xóa toàn bộ dữ liệu bên trong bucket (datasets, metadata, logs, backups) trước khi xóa bucket.

2.  Truy cập [IAM Console](https://console.aws.amazon.com/iam/) và xóa các IAM Users đã tạo:
    - `provider-test-user`
    - `consumer-test-user`  
    Lưu ý: cần xóa access keys trước khi xóa user.

3.  Trong IAM Console, vào **Roles** và xóa các role:
    - `EvDataProviderRole`
    - `EvDataConsumerRole`
    - `EvDataMarketplaceServiceRole`

4.  Trong IAM Console, vào **Policies** và xóa các policy:
    - `EvDataProviderPolicy`
    - `EvDataConsumerPolicy`  
    (Nếu cần, hãy detach policy khỏi role trước khi xóa)

5.  Truy cập [Amazon Cognito Console](https://console.aws.amazon.com/cognito/) và xóa User Pool:
    - `ev-marketplace-user-pool`

6.  Trong Cognito (nếu vẫn còn), xóa:
    - User groups: `Admins`, `DataProviders`, `DataConsumers`
    - App client: `ev-marketplace-app-client`
    - Domain (nếu đã cấu hình)

7.  Kiểm tra lại toàn bộ tài nguyên:
    - Không còn S3 bucket
    - Không còn IAM users / roles / policies
    - Không còn Cognito User Pool

# Cảm ơn bạn!

Hy vọng bạn đã học được điều gì đó mới và có thêm cảm hứng từ workshop này 🚀