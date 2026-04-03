---
title : "5.4.1 - Tạo IAM Policies"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---

## Hướng Dẫn Từng Bước: Tạo IAM Policies

### Mục Tiêu
Tạo các IAM policies tùy chỉnh xác định các quyền cụ thể cho các data providers và data consumers để tương tác với S3 bucket và các tài nguyên marketplace.

---

## Lịch Sử: Kiểm Soát Truy Cập Dựa Trên Policies

IAM policies là các tài liệu JSON xác định những hành động nào mà users/roles có thể thực hiện trên các tài nguyên AWS cụ thể. Chúng ta sẽ tạo hai policies chính:
- **EvDataProviderPolicy** → Tải lên và quản lý các bộ dữ liệu
- **EvDataConsumerPolicy** → Tải xuống và xem các bộ dữ liệu

---

## Bước 1: Mở AWS IAM Console

1. Trong AWS Management Console, tìm kiếm **IAM**
2. Nhấp vào **IAM** từ kết quả
3. Trên menu bên trái, nhấp vào **Policies** dưới "Access management"

*Placeholder hình ảnh: Trang IAM Policies*

---

## Bước 2: Tạo Data Provider Policy

### Bước 2.1: Bắt Đầu Tạo Policy

1. Nhấp vào nút **Create policy**
2. Chọn tab **JSON** (để nhập tài liệu policy thô)
3. Bạn sẽ thấy trình chỉnh sửa văn bản cho policy JSON

*Placeholder hình ảnh: Tạo policy - JSON editor*

---

### Bước 2.2: Nhập Provider Policy JSON

Xóa nội dung mặc định và dán policy này:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ListBuckets",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*"
        },
        {
            "Sid": "UploadDatasets",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/datasets/*"
        },
        {
            "Sid": "ManageMetadata",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/metadata/*"
        },
        {
            "Sid": "WriteTransactionLogs",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/logs/transaction-logs/*"
        }
    ]
}
```

> **Lưu ý:** Thay thế `ev-data-marketplace-datasets-*` bằng tên bucket thực tế của bạn

*Placeholder hình ảnh: Policy JSON được dán*

---

### Bước 2.3: Xem Lại và Đặt Tên Policy

1. Nhấp vào nút **Next: Tags** (hoặc bỏ qua tags)
2. Nhấp vào nút **Next: Review**
3. Trong trường **Policy name**, nhập: `EvDataProviderPolicy`
4. Trong **Description**, nhập: `Policy for data providers to upload and manage datasets`
5. Nhấp vào nút **Create policy**

*Placeholder hình ảnh: Xem lại policy và đặt tên*

---

### Bước 2.4: Xác Minh Provider Policy Được Tạo

1. Bạn sẽ thấy thông báo thành công: "The policy EvDataProviderPolicy has been created"
2. Policy hiện có sẵn để gán cho users/roles

*Placeholder hình ảnh: Policy được tạo thành công*

---

## Bước 3: Tạo Data Consumer Policy

### Bước 3.1: Bắt Đầu Tạo Consumer Policy

1. Nhấp vào nút **Create policy** lại
2. Chọn tab **JSON**
3. Xóa nội dung mặc định

*Placeholder hình ảnh: JSON editor policy mới*

---

### Bước 3.2: Nhập Consumer Policy JSON

Dán policy này:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ListBuckets",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*"
        },
        {
            "Sid": "DownloadDatasets",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/datasets/*"
        },
        {
            "Sid": "ViewMetadata",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/metadata/dataset-descriptions/*"
        },
        {
            "Sid": "WriteAccessLogs",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/logs/access-logs/*"
        }
    ]
}
```

*Placeholder hình ảnh: Consumer policy JSON*

---

### Bước 3.3: Xem Lại và Đặt Tên Consumer Policy

1. Nhấp vào **Next: Tags** (bỏ qua nếu không cần)
2. Nhấp vào **Next: Review**
3. Trong trường **Policy name**, nhập: `EvDataConsumerPolicy`
4. Trong **Description**, nhập: `Policy for data consumers to download and view datasets`
5. Nhấp vào nút **Create policy**

*Placeholder hình ảnh: Xem lại consumer policy*

---

### Bước 3.4: Xác Minh Consumer Policy Được Tạo

1. Thông báo thành công: "The policy EvDataConsumerPolicy has been created"
2. Cả hai policies hiện đã sẵn sàng để sử dụng

*Placeholder hình ảnh: Cả hai policies được tạo*

---

## Tóm Tắt

Bạn đã tạo thành công hai IAM policies:

| Tên Policy | Mục Đích | Quyền |
|------------|---------|-------|
| **EvDataProviderPolicy** | Các data providers tải lên và quản lý bộ dữ liệu | Tải lên, Chỉnh sửa, Xóa (datasets/metadata) |
| **EvDataConsumerPolicy** | Các data consumers tải xuống bộ dữ liệu | Truy cập chỉ đọc (datasets/metadata) |

Cả hai policies tuân theo **nguyên tắc đặc quyền tối thiểu** - người dùng chỉ nhận được quyền tối thiểu mà họ cần.

**Nhiệm Vụ Tiếp Theo:** Tạo IAM Roles và gán các policies này cho roles

*Placeholder hình ảnh: Xem danh sách Policies*
