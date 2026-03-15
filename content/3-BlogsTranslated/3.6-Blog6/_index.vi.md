---
title: "Blog 6"
date: 2026-03-02
weight: 6
chapter: false
pre: " <b> 3.6. </b> "
---

# Hiểu về IAM cho Managed AWS MCP Servers

Khi các AI agent ngày càng được tích hợp sâu vào quy trình phát triển phần mềm, các tổ chức cần một cách để cho phép các agent này tương tác với tài nguyên AWS **một cách an toàn và nhất quán**. Trong thực tế, điều này có nghĩa là AI agent nên sử dụng cùng mô hình **AWS Identity and Access Management (IAM)** mà developer đã quen dùng, thay vì buộc các team phải xây dựng một hệ thống authorization riêng cho hoạt động do AI điều khiển.

Đồng thời, các tổ chức cũng cần đủ khả năng kiểm soát để **phân biệt giữa hành động do người dùng thực hiện trực tiếp** và **hành động do AI agent thực hiện thay mặt người dùng**.

Trong bài viết trên AWS Security Blog, các tác giả giải thích cách AWS giải quyết nhu cầu này cho **AWS-managed remote Model Context Protocol (MCP) servers**. Bài viết giới thiệu các **IAM context key tiêu chuẩn mới**, giúp các tổ chức áp dụng chính sách quản trị khác nhau cho hoạt động AI dựa trên MCP, mô tả mô hình authorization đơn giản hơn tương tự cách **AWS CLI** và **AWS SDKs** hoạt động, đồng thời giới thiệu kế hoạch hỗ trợ **VPC endpoints** trong tương lai để tăng cường kiểm soát mạng riêng.

---

## Tổng quan

AWS cho biết tại **AWS re:Invent 2025**, công ty đã ra mắt bản preview của bốn AWS-managed remote MCP servers:

- **AWS**
- **EKS**
- **ECS**
- **SageMaker**

Các MCP server này được **AWS vận hành và quản lý**, vì vậy khách hàng không cần cài đặt hoặc duy trì hạ tầng MCP server riêng. Thay vào đó, họ được hưởng lợi từ:

- cập nhật tự động
- khả năng mở rộng và độ bền tốt hơn
- khả năng audit thông qua **AWS CloudTrail**

Một ví dụ quan trọng được đề cập là **AWS MCP Server**, có thể cung cấp truy cập đến tài liệu AWS và thực thi hơn **15.000 AWS APIs**. Điều này cho phép AI agent hỗ trợ các tác vụ infrastructure nhiều bước như:

- tạo tài nguyên VPC
- cấu hình alarm cho **Amazon CloudWatch**

Tuy nhiên, AWS nhận thấy khách hàng có hai mối quan tâm lớn khi AI agent bắt đầu tham gia nhiều hơn vào workflow phát triển:

1. AI agent cần sử dụng **IAM permission hiện có**, thay vì framework permission mới.
2. Tổ chức muốn áp dụng **governance control khác nhau** cho hành động do AI và hành động do con người.

Để giải quyết vấn đề này, AWS giới thiệu hai **IAM context keys** mới cho AWS-managed MCP servers:

- `aws:ViaAWSMCPService`
- `aws:CalledViaAWSMCP`

Các context key này cho phép xác định:

- request có đi qua MCP server hay không
- MCP server nào đã khởi tạo request

Theo AWS, điều này giúp triển khai **defense-in-depth**, duy trì audit trail chi tiết và đáp ứng yêu cầu compliance bằng cách phân biệt truy cập do AI và truy cập trực tiếp của người dùng.

Ngoài ra, AWS cũng công bố một thay đổi nhằm **đơn giản hóa authorization model**. Trong tương lai gần, khách hàng sẽ **không cần sử dụng IAM action riêng cho MCP** như:
