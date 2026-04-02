---
title: "AWS Workshop: Secure Data Storage với Cognito, IAM và S3"
date: 2026-01-05
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## Giải pháp Xây dựng Hệ thống Lưu trữ Dữ liệu Bảo mật trên AWS

### 1. Tóm tắt điều hành

Workshop tập trung vào việc xây dựng một hệ thống lưu trữ dữ liệu an toàn trên AWS sử dụng ba dịch vụ chính: Amazon S3, AWS IAM và Amazon Cognito.  

Hệ thống cho phép người dùng:
- Đăng ký và đăng nhập thông qua Cognito
- Được cấp quyền truy cập tài nguyên thông qua IAM roles
- Upload, download và quản lý dữ liệu trên S3

Mục tiêu của workshop là giúp người học hiểu cách triển khai cơ chế xác thực (authentication) và phân quyền (authorization) trong một hệ thống cloud thực tế, đồng thời xây dựng nền tảng cho các ứng dụng lưu trữ dữ liệu an toàn.

---

### 2. Vấn đề cần giải quyết

#### Vấn đề hiện tại

- Việc quản lý người dùng và quyền truy cập dữ liệu thường phức tạp
- Dữ liệu lưu trữ trên cloud dễ bị truy cập trái phép nếu không cấu hình đúng
- Người học AWS thường chưa hiểu rõ cách tích hợp giữa authentication và storage
- Thiếu mô hình đơn giản nhưng đầy đủ để triển khai hệ thống bảo mật

---

#### Giải pháp đề xuất

Workshop xây dựng một hệ thống lưu trữ dữ liệu với các thành phần:

- **Amazon Cognito**: Quản lý user (signup, login, token)
- **AWS IAM**: Phân quyền truy cập tài nguyên dựa trên role
- **Amazon S3**: Lưu trữ dữ liệu người dùng

Flow hoạt động:

1. User đăng nhập qua Cognito  
2. Cognito cấp token xác thực  
3. Token được dùng để assume IAM role  
4. IAM role cho phép truy cập S3 theo policy  
5. User upload/download dữ liệu từ S3  

---

#### Lợi ích & Giá trị

- Hiểu rõ cơ chế authentication và authorization trên AWS
- Triển khai được hệ thống lưu trữ dữ liệu an toàn
- Áp dụng được cho các ứng dụng thực tế (file storage, user data)
- Là nền tảng cho các hệ thống lớn hơn (backend, SaaS, data platform)

---

### 3. Kiến trúc giải pháp

Hệ thống sử dụng kiến trúc đơn giản nhưng bảo mật cao:

---

**Authentication Layer:**
- **Amazon Cognito**
  - Quản lý user pool
  - Xác thực người dùng
  - Cấp JWT token

---

**Authorization Layer:**
- **AWS IAM**
  - Định nghĩa role và policy
  - Kiểm soát quyền truy cập S3
  - Mapping giữa Cognito user và IAM role

---

**Storage Layer:**
- **Amazon S3**
  - Lưu trữ dữ liệu người dùng
  - Phân quyền truy cập theo IAM policy
  - Có thể phân tách theo folder/user prefix

---

**Security Flow:**

- User → Cognito (login)
- Cognito → IAM (assume role)
- IAM → S3 (authorize access)

---

### 4. Triển khai kỹ thuật

#### Các bước thực hiện

1. **Thiết lập S3**
   - Tạo bucket
   - Cấu hình policy (private by default)

2. **Cấu hình IAM**
   - Tạo role cho user
   - Viết policy cho phép truy cập S3 (GetObject, PutObject)

3. **Thiết lập Cognito**
   - Tạo User Pool
   - Cấu hình authentication flow
   - Tạo Identity Pool để map IAM role

4. **Kết nối hệ thống**
   - Mapping Cognito → IAM role
   - Test login và access S3

5. **Kiểm tra bảo mật**
   - Đảm bảo user chỉ truy cập được dữ liệu của mình
   - Verify access bằng credentials tạm thời

---

#### Công nghệ sử dụng

- Amazon S3
- AWS IAM
- Amazon Cognito
- AWS Console / CLI

---

### 5. Lịch trình & Cột mốc

- **Giai đoạn 1:** Thiết lập S3 và IAM
- **Giai đoạn 2:** Cấu hình Cognito
- **Giai đoạn 3:** Tích hợp hệ thống
- **Giai đoạn 4:** Kiểm thử và xác thực bảo mật

---

### 6. Ước tính ngân sách

Workshop sử dụng dịch vụ cơ bản:

- Amazon S3: ~$1–2
- Amazon Cognito: miễn phí (trong free tier)
- AWS IAM: miễn phí  

👉 Tổng chi phí: ~$1–3

---

### 7. Đánh giá rủi ro

**Rủi ro:**
- Cấu hình sai IAM policy → lộ dữ liệu
- Bucket S3 bị public ngoài ý muốn
- Mapping Cognito không đúng → user không access được

**Giảm thiểu:**
- Sử dụng nguyên tắc least privilege
- Block public access trên S3
- Test kỹ authentication flow
- Sử dụng IAM policy condition (user-based access)

---

### 8. Kết quả kỳ vọng

**Cải tiến kỹ thuật:**
- Hiểu rõ cách tích hợp Cognito + IAM + S3
- Triển khai thành công hệ thống lưu trữ bảo mật
- Nắm được cơ chế cấp quyền tạm thời (temporary credentials)

**Giá trị dài hạn:**
- Áp dụng cho:
  - File storage system
  - User content platform
  - Backend authentication system
- Là nền tảng cho các hệ thống serverless phức tạp hơn