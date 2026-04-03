---
title : "5.5.2 - Cấu Hình User Groups"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

## Hướng Dẫn Từng Bước: Cấu Hình Cognito User Groups

### Mục Tiêu
Tạo các nhóm người dùng trong Cognito để quản lý các quyền dựa trên vai trò: nhóm DataProviders và nhóm DataConsumers cho người dùng marketplace.

---

## Lịch Sử: User Groups

User groups cho phép bạn:
- Tổ chức người dùng theo vai trò hoặc chức năng
- Gắn các IAM roles vào nhóm
- Quản lý quyền ở cấp độ nhóm
- Hỗ trợ kiểm soát truy cập dựa trên vai trò (RBAC)

---

## Bước 1: Mở Cấu Hình User Groups

1. Trong console AWS Cognito, nhấp vào user pool của bạn: `ev-marketplace-user-pool`
2. Trên menu bên trái, nhấp vào **User groups**
3. Bạn sẽ thấy danh sách groups trống
4. Nhấp vào nút **Create group**

![](/worklogAws/images/5-Workshops/lab3/task2/step1.png)

---

## Bước 2: Tạo DataProviders Group

### Bước 2.1: Cấu Hình Chi Tiết Nhóm

1. Trong **Group name**, nhập: `DataProviders`
2. Trong **Description**, nhập: `Group for data providers who can upload and manage datasets`
3. Trong **IAM role**, chọn role mà chúng ta tạo trong Lab 2: `EvDataProviderRole`
4. Trong **Priority**, nhập: `1` (số thấp hơn = ưu tiên cao hơn)
5. Nhấp vào nút **Create group**

![](/worklogAws/images/5-Workshops/lab3/task2/step2.1.png)

---

### Bước 2.2: Xác Minh DataProviders Group Được Tạo

1. Bạn sẽ thấy DataProviders group trong danh sách
2. Trạng thái hiển thị IAM role được gắn


---

## Bước 3: Tạo DataConsumers Group

### Bước 3.1: Cấu Hình Consumer Group

1. Nhấp vào nút **Create group** lại
2. Trong **Group name**, nhập: `DataConsumers`
3. Trong **Description**, nhập: `Group for data consumers who can download and view datasets`
4. Trong **IAM role**, chọn: `EvDataConsumerRole`
5. Trong **Priority**, nhập: `2`
6. Nhấp vào nút **Create group**

![](/worklogAws/images/5-Workshops/lab3/task2/step3.1.png)

---

### Bước 3.2: Xác Minh DataConsumers Group Được Tạo

1. Cả hai nhóm hiện xuất hiện trong danh sách:
   - ✓ DataProviders (Priority 1)
   - ✓ DataConsumers (Priority 2)


---

## Bước 4: Tạo Admin Group (Tùy Chọn Nhưng Được Khuyến Nghị)

### Bước 4.1: Tạo Admin Group

1. Nhấp vào nút **Create group**
2. Trong **Group name**, nhập: `Admins`
3. Trong **Description**, nhập: `Administrators who can manage users and moderate datasets`
4. Trong **IAM role**, chọn: `EvDataMarketplaceServiceRole` (hoặc tạo một role dành riêng cho admin)
5. Trong **Priority**, nhập: `0` (ưu tiên cao nhất)
6. Nhấp vào nút **Create group**

![](/worklogAws/images/5-Workshops/lab3/task2/step4.1.png)

---

## Bước 5: Xác Minh Tất Cả Nhóm

1. User pool của bạn bây giờ sẽ có ba nhóm:
   - ✓ **Admins** (Priority 0 - Cao nhất)
   - ✓ **DataProviders** (Priority 1)
   - ✓ **DataConsumers** (Priority 2 - Thấp nhất)

2. Mỗi nhóm có một IAM role được liên kết cho tích hợp dịch vụ


---

## Bước 6: Thêm Custom Attributes Cho Nhóm (Trong APP)

Mặc dù Cognito không trực tiếp lưu trữ các custom group attributes, ứng dụng backend của bạn có thể:
1. Truy vấn các nhóm từ Cognito
2. Lưu trữ metadata bổ sung trong cơ sở dữ liệu
3. Sử dụng nó cho các cài đặt marketplace cụ thể

---

## Tóm Tắt

Bạn đã cấu hình thành công các nhóm người dùng với:
- **DataProviders group** → Truy cập vào các tính năng provider
- **DataConsumers group** → Truy cập vào các tính năng consumer
- **Admins group** → Truy cập quản trị toàn quyền
- **IAM roles được gắn** → Hệ thống quyền rõ ràng
- **Mức độ ưu tiên được đặt** → Xác định thứ tự quyền

Các nhóm này hiện đã sẵn sàng để có người dùng được gán cho chúng.

**Nhiệm Vụ Tiếp Theo:** Tạo và cấu hình app client cho OAuth flow

