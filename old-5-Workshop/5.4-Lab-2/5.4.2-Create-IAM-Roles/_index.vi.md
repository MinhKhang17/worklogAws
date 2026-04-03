---
title : "5.4.2 - Tạo IAM Roles"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---

## Hướng Dẫn Từng Bước: Tạo IAM Roles

### Mục Tiêu
Tạo các IAM roles sẽ được gắn vào users và sử dụng cho xác thực service-to-service. Các roles sẽ có các policies mà chúng ta đã tạo trong 5.4.1.

---

## Lịch Sử: Roles vs Policies

- **Policies** định nghĩa NHỮNG hành động nào được phép (quyền)
- **Roles** là các vùng chứa cho các policies có thể được giả định bởi users, applications, hoặc services

---

## Bước 1: Mở IAM Roles Console

1. Trong AWS IAM Console, trên menu bên trái, nhấp vào **Roles**
2. Bạn sẽ thấy dashboard roles với các roles hiện có (nếu có)
3. Nhấp vào nút **Create role**

*Placeholder hình ảnh: Trang IAM Roles*

---

## Bước 2: Tạo Provider Role

### Bước 2.1: Chọn Trusted Entity

1. Bạn ở bước **Select trusted entity**
2. Giữ nguyên mặc định: **AWS service** được chọn
3. Trong phần "Use case", nhấp vào **EC2**
   > Đây chỉ là tạm thời; chúng ta sẽ xác minh nó có thể được sử dụng bởi users

4. Nhấp vào nút **Next**

*Placeholder hình ảnh: Chọn trusted entity - EC2*

---

### Bước 2.2: Thêm Xin Phép Cho Role

1. Bây giờ bạn ở bước **Add permissions**
2. Trong hộp tìm kiếm, gõ: `EvDataProviderPolicy`
3. Đánh dấu hộp ✓ bên cạnh **EvDataProviderPolicy**
4. Nhấp vào nút **Next**

*Placeholder hình ảnh: Thêm EvDataProviderPolicy*

---

### Bước 2.3: Đặt Tên Cho Role

1. Bạn ở bước **Name, review, and create**
2. Trong **Role name**, nhập: `EvDataProviderRole`
3. Trong **Description**, nhập: `Role for data providers to upload and manage EV datasets`
4. Để **Maximum session duration** ở mặc định (1 giờ)
5. Nhấp vào nút **Create role**

*Placeholder hình ảnh: Tên role và xem lại*

---

### Bước 2.4: Cập Nhật Mối Quan Hệ Tin Cậy

Sau khi tạo role, chúng ta cần cho phép users giả định role này:

1. Nhấp vào **EvDataProviderRole** mới từ danh sách roles
2. Nhấp vào tab **Trust relationships**
3. Nhấp vào nút **Edit trust policy**

*Placeholder hình ảnh: Tab Trust relationships*

---

### Bước 2.5: Sửa Đổi Trust Policy

1. Thay thế JSON bằng trust policy này:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "cognito-idp.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::ACCOUNT-ID:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

> **Lưu ý:** Thay thế `ACCOUNT-ID` bằng ID tài khoản AWS của bạn

2. Nhấp vào nút **Update policy**

*Placeholder hình ảnh: Trust policy được cập nhật*

---

## Bước 3: Tạo Consumer Role (Quy Trình Tương Tự)

### Bước 3.1: Tạo Consumer Role

1. Nhấp vào nút **Create role**
2. Chọn **AWS service** → **EC2** (lại lần nữa)
3. Nhấp vào **Next**

*Placeholder hình ảnh: Tạo consumer role*

---

### Bước 3.2: Thêm Consumer Policy

1. Tìm kiếm: `EvDataConsumerPolicy`
2. Đánh dấu ✓ hộp bên cạnh nó
3. Nhấp vào **Next**

*Placeholder hình ảnh: Thêm EvDataConsumerPolicy*

---

### Bước 3.3: Đặt Tên Consumer Role

1. Trong **Role name**, nhập: `EvDataConsumerRole`
2. Trong **Description**, nhập: `Role for data consumers to download and view EV datasets`
3. Nhấp vào nút **Create role**

*Placeholder hình ảnh: Tạo consumer role*

---

### Bước 3.4: Cập Nhật Consumer Trust Policy

1. Nhấp vào **EvDataConsumerRole** từ danh sách
2. Nhấp vào tab **Trust relationships**
3. Nhấp vào nút **Edit trust policy**
4. Thay thế bằng trust policy tương tự như Provider (thay đổi ACCOUNT-ID):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "cognito-idp.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::ACCOUNT-ID:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

5. Nhấp vào nút **Update policy**

*Placeholder hình ảnh: Consumer trust policy được cập nhật*

---

## Bước 4: Tạo Service Role Cho Backend Application

### Bước 4.1: Tạo Service Role

1. Nhấp vào nút **Create role**
2. Chọn **AWS service** → **Lambda** (hoặc **EC2** nếu triển khai trên EC2)
3. Nhấp vào **Next**

*Placeholder hình ảnh: Service role cho backend*

---

### Bước 4.2: Thêm Cả Hai Policies Cho Service Role

1. Tìm kiếm và thêm cả hai policies:
   - ✓ **EvDataProviderPolicy**
   - ✓ **EvDataConsumerPolicy**
2. Nhấp vào **Next**

*Placeholder hình ảnh: Thêm cả hai policies cho service role*

---

### Bước 4.3: Đặt Tên Service Role

1. Trong **Role name**, nhập: `EvDataMarketplaceServiceRole`
2. Trong **Description**, nhập: `Service role for EV marketplace backend application for S3 and Cognito access`
3. Nhấp vào nút **Create role**

*Placeholder hình ảnh: Tạo service role*

---

## Tóm Tắt

Bạn đã tạo thành công ba IAM roles:

| Tên Role | Policy Được Gắn | Mục Đích |
|----------|-----------------|---------|
| **EvDataProviderRole** | EvDataProviderPolicy | Cho các data providers tải lên datasets |
| **EvDataConsumerRole** | EvDataConsumerPolicy | Cho các data consumers tải xuống datasets |
| **EvDataMarketplaceServiceRole** | Cả hai policies | Cho dịch vụ ứng dụng backend |

Tất cả các roles đã được cấu hình với các trust relationships thích hợp cho phép:
- ✅ Cognito service giả định chúng
- ✅ EC2/Lambda services giả định chúng
- ✅ Root account giả định chúng

**Nhiệm Vụ Tiếp Theo:** Tạo IAM Users và gán chúng cho roles

*Placeholder hình ảnh: Tất cả ba roles trong danh sách*
