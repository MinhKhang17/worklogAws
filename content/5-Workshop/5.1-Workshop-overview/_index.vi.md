---
title : "Tổng quan"
date : 2026-03-16
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

## Bạn sẽ xây dựng gì

Trước tiên, chúng ta sẽ thiết lập một **máy trạm ảo RealityCapture** trên một **Amazon EC2 G5 instance**. Máy trạm ảo RealityCapture cho phép người dùng tạo hoặc khởi tạo một **máy ảo có khả năng xử lý đồ họa** trên **Amazon Web Services (AWS)**, giúp loại bỏ nhu cầu phải chạy các workload của RealityCapture trên máy tính desktop hoặc laptop có GPU tại chỗ.

Sau đó, chúng ta sẽ đi qua từng bước để **chạy quy trình photogrammetry trên cloud**. Bao gồm:

- Tải bộ dữ liệu hình ảnh lên **Amazon S3**
- Khởi chạy một job mới trên **RealityCapture** bằng **PowerShell**
- Xuất **model và texture** trở lại **S3**

![RC Diagram](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-workshop-arch.png)

---

## Những gì bạn cần chuẩn bị

* **Tài khoản AWS** – Tài khoản này cần có:

  * Quyền triển khai **EC2 instances** bằng **CloudFormation templates**
  * **Service quota** (tối thiểu 8) để khởi chạy **EC2 G Type instances**
  * Loại instance EC2 tối thiểu: **g4dn.2xlarge** hoặc **g5.2xlarge**

ℹ️ **Yêu cầu tăng Quota cho Amazon EC2 G Type**

RealityCapture yêu cầu một **Amazon EC2 graphics instance (G type)**. **Bạn rất có thể cần yêu cầu tăng service quota để thực hiện workshop này.**

Trong tài khoản AWS của bạn:

1. Truy cập **Service Quotas**
2. Chọn **AWS Services**
3. Tìm và chọn **Amazon Elastic Cloud Compute (EC2)**
4. Tìm và chọn **“Running On-Demand G and VT instances”**

Nếu tài khoản của bạn có **ít hơn 8 vCPU** cho loại instance này, hãy yêu cầu **tăng quota lên 8 vCPU hoặc cao hơn**.

**Lưu ý:** Việc tăng quota sẽ được đội ngũ AWS xem xét và **có thể mất vài ngày để xử lý**.

⚠️ **Chi phí**

Các tài khoản **AWS Free Tier** không có quota cho **EC2 G type instances**.

Để biết chi tiết về giá EC2, vui lòng xem:
https://aws.amazon.com/ec2/pricing/

**Chạy toàn bộ workshop và dọn dẹp sau đó sẽ tốn khoảng ~$10–15 USD.**

*Lưu ý:* Chi phí có thể thay đổi tùy theo:

- Region AWS bạn triển khai
- Loại và kích thước instance
- Thời gian bạn khám phá thêm các tính năng của RealityCapture ngoài các bước trong workshop

Khi bạn **không sử dụng EC2 instance**, hãy **tắt instance** để tránh phát sinh chi phí khi instance vẫn đang chạy.

Sau khi **stop instance**, bạn sẽ **không còn bị tính phí sử dụng hoặc truyền dữ liệu** cho instance đó. Tuy nhiên, bạn vẫn sẽ bị tính phí cho các tài nguyên liên quan, ví dụ:

- **EBS volumes** được gắn kèm
- **Elastic IP addresses**

---

## Regions được hỗ trợ

Workshop này **chỉ hoạt động trong các AWS Region sau**:

**us-east-1, us-east-2, us-west-1, us-west-2, ca-central-1, eu-central-1, ap-northeast-1**

---

## Bạn sẽ học được gì

Trong workshop này, bạn sẽ học cách:

* Sử dụng **NICE DCV remote display protocol (RDP)** để chạy các ứng dụng đồ họa nặng từ xa trên **EC2 instances** thông qua **virtual workstation**
* Sử dụng **PowerShell** để tạo **textured mesh** bằng **RealityCapture** và lưu mesh vào **S3**
* Triển khai **AWS CloudFormation template**