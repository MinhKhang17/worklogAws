---
title: "Blog 6"
date: 2026-04-01
weight: 6
chapter: false
pre: " <b> 3.6. </b> "
---

# AWS: Tích hợp Agent, Khả năng chịu lỗi, Bảo mật, Lưu trữ và Bảo vệ Game

AWS đang không ngừng phát triển trên nhiều khía cạnh—từ tùy chỉnh mô hình AI cho doanh nghiệp, xây dựng hệ thống định danh và truy cập có khả năng chịu lỗi cao, đến các công cụ vận hành, cơ chế bảo mật mang tính xác định cho workflow có agent, và các giải pháp bảo vệ chuyên biệt cho workload nhạy cảm về độ trễ như game multiplayer.

Bài viết này tổng hợp các cập nhật và hướng dẫn mới nhất từ AWS nhằm giúp tổ chức áp dụng agent một cách an toàn, đồng thời vẫn đảm bảo tính ổn định và bảo mật hệ thống.

---

## Tùy chỉnh mô hình AI và chuyên biệt hóa có kiểm soát

AWS đã giới thiệu các phương pháp mới cho phép doanh nghiệp xây dựng mô hình phù hợp với dữ liệu nội bộ và kiến thức chuyên ngành.

Thay vì chỉ dựa vào prompt engineering hoặc fine-tuning giai đoạn cuối, các dịch vụ như Amazon Nova Forge cho phép:
- Bắt đầu từ các checkpoint sớm của mô hình
- Kết hợp dữ liệu riêng với dataset đã được chọn lọc

Cách tiếp cận này giúp:
- Giảm hiện tượng “catastrophic forgetting”
- Giữ được năng lực nền tảng của mô hình
- Tăng khả năng chuyên biệt hóa theo domain

### Các thực hành chính:
- Chọn checkpoint phù hợp (trước, giữa hoặc sau training)
- Kết hợp dữ liệu proprietary với dữ liệu public/vendor
- Sử dụng pipeline managed (ví dụ SageMaker AI) và deploy qua Bedrock

Các cơ chế Responsible AI là bắt buộc:
- kiểm soát an toàn
- kiểm duyệt nội dung
- governance xuyên suốt pipeline

---

## Định danh linh hoạt: Multi-Region và kiểm soát MCP

Khi hệ thống phân tán và agent hoạt động đa vùng, tính sẵn sàng của identity trở nên cực kỳ quan trọng.

### Multi-Region IAM Identity Center:
- Cho phép hệ thống vẫn hoạt động khi một Region bị sự cố
- Giảm độ trễ bằng cách đặt gần người dùng

### IAM context keys cho MCP:
- `aws:ViaAWSMCPService`
- `aws:CalledViaAWSMCP`

Cho phép:
- Chặn hoặc hạn chế hành động nhạy cảm từ agent
- Cho phép read-only nhưng chặn thao tác nguy hiểm
- Ánh xạ service với MCP server cụ thể

Sự kết hợp này giúp:
- tăng tính resilience
- tăng governance khi agent thao tác đa tài khoản và region

---

## Agent vận hành và sự phát triển nền tảng

Các công cụ agent cho vận hành cloud đang ngày càng trưởng thành.

AWS cung cấp:
- Agent DevOps
- MCP server có thể gọi hàng nghìn API

### Cách triển khai an toàn:
- Áp dụng least privilege IAM
- Dùng context keys để kiểm soát request từ agent
- Bắt đầu với chế độ `LOG_ONLY`
- Phân tích CloudTrail trước khi enforce

Điều này giúp:
- giảm rủi ro khi agent scale lớn
- dễ audit và xử lý sự cố

---

## Thực thi policy xác định (Deterministic) cho bảo mật agent

Nguyên tắc quan trọng:
👉 Không để AI quyết định quyền truy cập

AWS AgentCore sử dụng:
- Policy runtime kiểu Cedar
- Đánh giá rõ ràng: principal, action, resource

### Hướng dẫn thiết kế:
- Default deny
- Layered forbid
- Test policy với `LOG_ONLY`
- Kiểm tra chặt request parameters

Kết quả:
- Policy có thể audit
- Tái lập được
- Phù hợp môi trường regulated (finance, healthcare)

---

## Bảo vệ chuyên biệt: Game Multiplayer và DDoS

Đối với workload UDP, độ trễ thấp như game:

AWS cung cấp:
- Relay-based protection
- Ẩn endpoint server
- Giới hạn traffic theo player

### Best practices:
- Không expose server trực tiếp
- Dùng token xác thực
- Test latency thực tế
- Kết hợp CloudWatch monitoring

---

## Các bước triển khai thực tế

1. Phân loại use case của agent (read-only, admin, destructive)
2. Áp dụng least privilege IAM + MCP context keys
3. Deploy theo giai đoạn với `LOG_ONLY`
4. Dùng multi-region nếu cần high availability
5. Với môi trường regulated, kết hợp VPC endpoint + IAM

---

## Kết luận

AWS đang theo hướng:
- Tăng sức mạnh cho agent
- Nhưng kiểm soát chặt chẽ hơn

Bằng cách kết hợp:
- Tùy chỉnh mô hình
- Identity đa vùng
- Policy xác định
- Bảo vệ workload

→ Doanh nghiệp có thể tận dụng AI mà vẫn kiểm soát rủi ro.

---

## About the Authors

Bài viết tổng hợp từ nhiều blog và cập nhật sản phẩm của AWS về AI, bảo mật, identity, agent và bảo vệ hệ thống.
---
title: "Blog 6"
date: 2026-03-02
weight: 6
chapter: false
pre: " <b> 3.6. </b> "
---

# Tìm hiểu IAM cho AWS MCP Server được quản lý

Khi AI agent ngày càng tích hợp sâu vào workflow phát triển phần mềm, tổ chức cần một cách để agent tương tác với tài nguyên AWS một cách an toàn và nhất quán.

Mục tiêu:
- Agent sử dụng cùng mô hình IAM như developer
- Không cần hệ thống phân quyền riêng
- Phân biệt rõ hành động của người và AI

---

## Tổng quan

Tại AWS re:Invent 2025, AWS giới thiệu:
- AWS MCP Server
- EKS MCP
- ECS MCP
- SageMaker MCP

Các server này:
- Được AWS quản lý hoàn toàn
- Tự động cập nhật
- Scale tốt
- Audit qua CloudTrail

Một MCP server có thể:
- Truy cập tài liệu AWS
- Gọi hơn 15,000 API

---

## Context keys mới

AWS giới thiệu:

- `aws:ViaAWSMCPService` (boolean)
- `aws:CalledViaAWSMCP` (string)

Cho phép:
- Xác định request đến từ AI
- Phân biệt theo từng MCP server
- Áp dụng policy chi tiết

---

## Ví dụ policy

### Chặn toàn bộ MCP
Nếu `aws:ViaAWSMCPService = true` → deny

### Cho phép read S3 nhưng chặn delete
- Allow: `GetObject`, `ListBucket`
- Deny: `DeleteObject`, `DeleteBucket`

### Giới hạn theo MCP server
- Chỉ cho phép EKS nếu gọi từ EKS MCP

---

## Đơn giản hóa authorization

AWS sẽ:
- Loại bỏ permission riêng cho MCP
- Dùng IAM hiện tại
- MCP chỉ forward request + context keys

→ Giống cách AWS CLI / SDK hoạt động

---

## VPC Endpoint (sắp ra mắt)

Cho phép:
- Agent chạy hoàn toàn trong private network
- Kết hợp:
  1. kiểm soát network (VPC)
  2. kiểm soát IAM

→ tăng bảo mật cho môi trường regulated

---

## Lưu ý khi triển khai

- Thiết kế IAM theo least privilege
- Theo dõi CloudTrail
- Bắt đầu nhỏ → mở rộng dần
- Tối ưu policy theo usage thực tế

---

## Kết luận

AWS đang giúp:
- AI agent dễ triển khai hơn
- Nhưng vẫn giữ:
  - governance
  - auditability
  - security

---

## About the Authors

**Riggs Goodman III** – Principal Architect, chuyên về AI security  
**Praneeta Prakash** – Product Manager AWS Developer Tools  
**Khaled Sinno** – Principal Engineer IAM  
**Shreya Jain** – Product Manager AWS Identity