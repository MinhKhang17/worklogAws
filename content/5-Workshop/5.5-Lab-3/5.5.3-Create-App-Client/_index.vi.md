---
title : "5.5.3 - Tạo App Client & Kiểm Tra Xác Thực"
date : 2026-03-25
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

## Hướng Dẫn Từng Bước: Tạo App Client & Kiểm Tra Xác Thực

### Mục Tiêu
Cấu hình app client cho các OAuth authentication flows và kiểm tra chức năng sign-up/sign-in của người dùng.

---

## Bước 1: Cấu Hình Cài Đặt App Client

1. Trong user pool `ev-marketplace-user-pool` của bạn
2. Nhấp vào **App integration** trên menu bên trái
3. Nhấp vào **App clients**
4. Bạn sẽ thấy app client được tạo trước đó: `ev-marketplace-app-client`
5. Nhấp vào nó để chỉnh sửa cài đặt


---

## Bước 2: Cấu Hình Authentication Flows

1. Trong **Authentication flows and security**, cấu hình:
   - ✓ **ALLOW_ADMIN_USER_PASSWORD_AUTH** (cho kiểm tra)
   - ✓ **ALLOW_CUSTOM_AUTH**
   - ✓ **ALLOW_USER_PASSWORD_AUTH** (cho app login)
   - ✓ **ALLOW_USER_SRP_AUTH** (secure password auth)
   - ✓ **ALLOW_REFRESH_TOKEN_AUTH** (token refresh)

2. Nhấp vào nút **Save**


---

## Bước 3: Cấu Hình Advanced App Client Settings

1. Trong **Advanced app client settings**, đặt:
   - **Token expiration (in hours):**
     - Access token: `1` giờ
     - ID token: `1` giờ
     - Refresh token: `30` ngày

2. Nhấp vào nút **Save**


---

## Bước 4: Lấy App Client Credentials

1. Trong **App client overview** hoặc **App client settings**:
   - Ghi chú **Client ID**
   - Ghi chú **Client Secret** (nếu được hiển thị)
   - Ghi chú **App domain** hoặc **Cognito domain**

2. Các thông tin này sẽ cần cho cấu hình backend


---

## Bước 5: Cấu Hình OAuth Domain (Custom Domain)

### Bước 5.1: Điều Hướng Đến Cấu Hình Domain

1. Trong menu **App integration**, nhấp vào **Domain name**
2. Bạn sẽ thấy domain đã được cấu hình hay chưa
3. Nếu chưa, nhấp vào nút **Create custom domain**


---

### Bước 5.2: Tạo Domain

1. Nhập tên domain tùy chỉnh: `ev-marketplace`
   - Lưu ý: Phải là duy nhất trên toàn cầu
2. Domain đầy đủ sẽ là: `ev-marketplace.auth.us-east-1.amazoncognito.com`
3. Nhấp vào nút **Create domain**


---

## Bước 6: Kiểm Tra User Sign-Up

### Bước 6.1: Điều Hướng Đến User Testing

1. Trong user pool của bạn, nhấp vào **Users** trên menu bên trái
2. Nhấp vào nút **Create user** để thêm một user kiểm tra theo cách thủ công, HOẶC
3. Sử dụng Cognito Hosted UI để kiểm tra self-service sign-up


---

### Bước 6.2: Truy Cập Hosted UI

1. Trong **App integration** → **App clients**
2. Nhấp vào liên kết **Hosted UI**
3. Điều này mở giao diện đăng nhập được cung cấp bởi Cognito
4. Nhấp vào **Sign up** để tạo một user kiểm tra mới


---

### Bước 6.3: Tạo Test Users

Tạo hai user kiểm tra:

**User 1 - Provider:**
- Username: `provider-test`
- Email: `provider@marketplace.local`
- Password: `TempPass123!@#`
- Custom attribute - business_type: `provider`
- Custom attribute - company_name: `EV Data Inc`

**User 2 - Consumer:**
- Username: `consumer-test`
- Email: `consumer@marketplace.local`
- Password: `TempPass123!@#`
- Custom attribute - business_type: `consumer`
- Custom attribute - company_name: `EV Analysis Ltd`


---

## Bước 7: Gán Users Cho Nhóm

### Bước 7.1: Gán Provider User Cho Group

1. Đi tới **Users** trong user pool của bạn
2. Nhấp vào user **provider-test**
3. Nhấp vào tab **User groups**
4. Nhấp vào **Add to group**
5. Chọn nhóm **DataProviders**
6. Nhấp vào nút **Add**


---

### Bước 7.2: Gán Consumer User Cho Group

1. Quay lại **Users**
2. Nhấp vào user **consumer-test**
3. Nhấp vào tab **User groups**
4. Nhấp vào **Add to group**
5. Chọn nhóm **DataConsumers**
6. Nhấp vào nút **Add**


---

## Bước 8: Xác Minh Gán Nhóm

1. Quay lại profile người dùng
2. Xác nhận `provider-test` ở trong nhóm **DataProviders**
3. Xác nhận `consumer-test` ở trong nhóm **DataConsumers**


---

## Bước 9: Kiểm Tra Authentication Flow

### Bước 9.1: Kiểm Tra Provider Login

1. Đi tới Hosted UI (từ App clients)
2. Đăng nhập với thông tin provider:
   - Username: `provider-test`
   - Password: `TempPass123!@#`
3. Nên xác thực thành công
4. Sao chép mã ủy quyền hoặc ID token


---

### Bước 9.2: Kiểm Tra Consumer Login

1. Đăng xuất
2. Đăng nhập với thông tin consumer:
   - Username: `consumer-test`
   - Password: `TempPass123!@#`
3. Nên xác thực thành công
4. Ghi chú các yêu cầu token (nên hiển thị nhóm)


---

## Bước 10: Xác Minh JWT Tokens

### Bước 10.1: Giải Mã ID Token

1. Đi tới [jwt.io](https://jwt.io)
2. Dán ID token từ xác thực
3. Xác minh token chứa:
   - `iss` (issuer) - Cognito URL
   - `sub` (subject) - User ID
   - `cognito:groups` - Nên hiển thị thành viên nhóm
   - Custom attributes (`company_name`, `business_type`)


---

## Tóm Tắt

Bạn đã cấu hình thành công Cognito authentication với:
- ✅ App client được cấu hình cho OAuth flows
- ✅ Authentication flows được kích hoạt
- ✅ Token expiration được đặt phù hợp
- ✅ Custom domain được cấu hình
- ✅ Test users được tạo trong cả hai nhóm
- ✅ Thành viên nhóm được xác minh
- ✅ JWT tokens được xác minh với claims nhóm

**Lab 3 Hoàn Tất!** Cơ sở hạ tầng Cognito của bạn đã sẵn sàng để tích hợp backend.

---

## Thông Tin Để Lưu Cho Lab 4:

- **User Pool ID:** `us-east-1_xxxxxxxxx`
- **Client ID:** `xxxxxxxxxxxxxxxxxxxx`
- **Client Secret:** (nếu có)
- **Cognito Domain:** `ev-marketplace.auth.us-east-1.amazoncognito.com`
- **Test Provider User:** `provider-test` / Group: `DataProviders`
- **Test Consumer User:** `consumer-test` / Group: `DataConsumers`

**Tiếp Theo:** Tiến Hành Lab 4 - Tích Hợp Với Backend Java Spring Boot

