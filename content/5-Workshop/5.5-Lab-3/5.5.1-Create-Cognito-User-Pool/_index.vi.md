---
title : "5.5.1 - Tạo Cognito User Pool"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.5.1. </b> "
---

## Hướng Dẫn Từng Bước: Tạo Cognito User Pool

### Mục Tiêu
Tạo một Amazon Cognito User Pool làm dịch vụ xác thực cho EV Data Marketplace, cho phép người dùng đăng ký, đăng nhập, và quản lý tài khoản của họ.

---

## Lịch Sử: Cognito User Pools

Cognito User Pools cung cấp:
- User sign-up và sign-in
- Quản lý tài khoản
- Đặt lại mật khẩu và phục hồi
- Xác thực đa yếu tố (tùy chọn)
- Tích hợp social identity provider (tùy chọn)

---

## Bước 1: Mở Amazon Cognito Console

1. Trong AWS Management Console, tìm kiếm **Cognito**
2. Nhấp vào **Cognito** từ kết quả
3. Bạn sẽ thấy dashboard Cognito
4. Nhấp vào nút **Create user pool**

![](/worklogAws/images/5-Workshops/lab3/task1/step1.png)

---

## Bước 2: Cấu Hình Trải Nghiệm Sign-In

1. Bạn ở trang **Configure sign-in experience**
2. Trong **Provider types**, giữ **Cognito user pool** được chọn
3. Trong **Cognito user pool sign-in options**, chọn:
   - ✓ **Email**
   - ✓ **User name**
   - (Cho phép người dùng đăng nhập bằng email hoặc username)
4. Nhấp vào nút **Next**

![](/worklogAws/images/5-Workshops/lab3/task1/step2.png)

---

## Bước 3: Cấu Hình Yêu Cầu Bảo Mật

1. Bạn ở trang **Configure security requirements**
2. Trong **Password policy**, chọn **Custom** để định nghĩa các quy tắc tùy chỉnh:
   - Độ dài tối thiểu: **12** ký tự
   - ✓ Yêu cầu chữ hoa
   - ✓ Yêu cầu chữ thường
   - ✓ Yêu cầu số
   - ✓ Yêu cầu ký tự đặc biệt (@, #, $, %, v.v.)
3. Trong **Multi-factor authentication (MFA)**, chọn **No MFA** (tùy chọn bây giờ, có thể thêm sau)
4. Trong **Account recovery**, giữ cài đặt mặc định
5. Nhấp vào nút **Next**


---

## Bước 4: Cấu Hình Trải Nghiệm Sign-Up

1. Bạn ở trang **Configure sign-up experience**
2. Trong **Self-service sign-up**, chọn **Enable self-registration**
   - Điều này cho phép người dùng mới tạo tài khoản
3. Trong **Attribute verification and user account confirmation**, chọn:
   - **Send email message** (xác minh email)
   - **Automatically confirm and sign users in** không được chọn
4. Trong **Required attributes**, giữ mặc định:
   - Email (bắt buộc)
5. Trong **Custom attributes**, chúng ta sẽ thêm các thuộc tính tùy chỉnh cho marketplace:
   - Nhấp vào nút **Add custom attribute**
   - Attribute name: `company_name`
   - Attribute type: **String**
   - Độ dài tối đa: **256**
6. Nhấp vào **Add custom attribute** lại cho:
   - Attribute name: `business_type`
   - Attribute type: **String**
   - Giá trị: `provider` hoặc `consumer`
7. Nhấp vào nút **Next**


---

## Bước 5: Cấu Hình Message Delivery

1. Bạn ở trang **Configure message delivery**
2. Trong **Email provider**, chọn **Send email with Cognito**
   - Sử dụng cái này cho kiểm tra/phát triển
   - Cho production, hãy cân nhắc sử dụng Amazon SES
3. Trong **Email address display name**, nhập: `EV Marketplace`
4. Để địa chỉ email dưới dạng mặc định
5. Nhấp vào nút **Next**


---

## Bước 6: Tích Hợp Ứng Dụng Của Bạn

1. Bạn ở trang **Integrate your app**
2. Trong **User pool name**, nhập: `ev-marketplace-user-pool`
3. Trong **App client name**, nhập: `ev-marketplace-app-client`
4. Trong **Client type**, giữ **Web client** được chọn (cho web/mobile apps)
5. Đảm bảo các tùy chọn sau được đánh dấu:
   - ✓ **Require client secret** (cho bảo mật)
   - ✓ **Allow user password auth** (cho truy cập theo chương trình)
6. Trong **Allowed sign-out URLs**, nhập:
   - `http://localhost:8080/logout` (cho kiểm tra)
   - `http://localhost:3000/logout` (cho frontend)
7. Nhấp vào nút **Next**


---

## Bước 7: Xem Lại và Tạo

1. Bạn ở trang **Review and create**
2. Xem lại tất cả cài đặt:
   - Tên User pool ✓
   - Tùy chọn sign-in ✓
   - Cài đặt bảo mật ✓
   - Custom attributes ✓
   - App client ✓
3. Nhấp vào nút **Create user pool**


---

## Bước 8: Xác Minh User Pool Được Tạo

1. Bạn sẽ thấy: "User pool created successfully"
2. Bạn sẽ thấy User Pool ID (như: `us-east-1_abcDefGhIj`)
3. Lưu ID này - bạn sẽ cần nó cho cấu hình backend
4. Đi tới phần **App clients and analytics**
5. Nhấp vào tên app client của bạn để xem:
   - Client ID
   - Client secret (nếu được kích hoạt)
   - Callback URLs
   - Các thông tin này sẽ cần thiết trong Lab 4


---

## Bước 9: Cấu Hình Email Settings (Tùy Chọn Nhưng Được Khuyến Nghị)

1. Trong menu bên trái, nhấp vào **App integration** → **App clients**
2. Nhấp vào app client của bạn
3. Dưới **App client settings**, cấu hình:
   - **Allowed OAuth scopes:**
     - ✓ email
     - ✓ openid
     - ✓ profile
   - **Callback URLs:**
     - `http://localhost:8080/auth/callback`
     - `https://yourdomain.com/auth/callback` (production)
4. Nhấp vào nút **Save**


---

## Tóm Tắt

Bạn đã tạo thành công một Cognito User Pool với:
- ✅ Tùy chọn sign-in bằng email và username
- ✅ Yêu cầu chính sách mật khẩu mạnh
- ✅ Custom attributes (company_name, business_type)
- ✓ Self-service registration được kích hoạt
- ✅ Xác minh email được cấu hình
- ✅ App client được cấu hình cho OAuth
- ✅ User Pool ID và Client ID được tạo

**Thông Tin Quan Trọng Để Lưu:**
- User Pool ID: `us-east-1_xxxxxxxxx`
- Client ID: `xxxxxxxxxxxxxxxxxxxx`
- Client secret: (nếu được kích hoạt)

**Nhiệm Vụ Tiếp Theo:** Cấu hình các nhóm người dùng cho kiểm soát truy cập dựa trên vai trò

