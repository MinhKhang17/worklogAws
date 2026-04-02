---
title: "Blog 4"
date: 2025-12-02
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

# AWS: Các kiểm soát bảo mật quan trọng để ngăn chặn việc xóa tài khoản trái phép trong AWS Organizations

Trong môi trường multi-account trên AWS, AWS Organizations đóng vai trò là nền tảng trung tâm để quản lý và áp dụng các chính sách bảo mật. Tuy nhiên, một rủi ro nghiêm trọng có thể xảy ra khi một tài khoản thành viên bị xâm nhập.

Nếu attacker chiếm quyền kiểm soát tài khoản, họ có thể thực hiện hành động **rời khỏi tổ chức (leave organization)**, từ đó vô hiệu hóa toàn bộ các cơ chế governance như SCP, logging và monitoring. :contentReference[oaicite:1]{index=1}  

Để giải quyết vấn đề này, AWS đề xuất một **mô hình bảo mật nhiều lớp (layered security controls)** nhằm đảm bảo rằng các tài khoản luôn nằm trong phạm vi kiểm soát của tổ chức.

---

## Vấn đề bảo mật trong AWS Organizations

Trong kiến trúc multi-account:

- AWS Organizations cung cấp governance tập trung  
- SCP áp dụng giới hạn quyền ở cấp tổ chức  
- Logging và monitoring được triển khai xuyên suốt  

Tuy nhiên, nếu một account bị compromise:

- Có thể tự rời khỏi organization  
- Mất toàn bộ SCP protection  
- Không còn bị giám sát  

Điều này tạo ra một **security gap nghiêm trọng**, đặc biệt trong môi trường production.

---

## Mô hình bảo mật nhiều lớp (Layered Security Approach)

AWS khuyến nghị sử dụng nhiều lớp kiểm soát thay vì một cơ chế đơn lẻ.

Các lớp chính bao gồm:

1. Service Control Policies (SCP)  
2. Organizational Unit (OU) design  
3. Secure account migration  
4. Centralized root access management  

Cách tiếp cận này đảm bảo:
- Ngăn chặn hành vi trái phép  
- Cho phép hoạt động hợp lệ  
- Duy trì governance liên tục  

---

## Ngăn chặn account rời tổ chức bằng SCP

Biện pháp quan trọng nhất là sử dụng **Service Control Policy (SCP)** để deny hành động:

```text
organizations:LeaveOrganization