---
title: "Worklog Tuần 10"
date: 2026-03-16
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* **Backend**: Hoàn thiện endpoint — cải thiện validation, pagination, viết unit test cho service chính.
* **Frontend**: Xây dựng `ChatScreen` với AWS Bedrock AI và `ProfileScreen` quản lý tài khoản.
* Cung cấp trợ lý AI tư vấn fitness — tính năng khác biệt của ứng dụng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Hoàn thiện endpoint backend <br>&emsp; + Thêm `@Valid` và custom constraint validator cho tất cả request DTO <br>&emsp; + Chuẩn hóa `PageResponse<T>` cho tất cả paginated endpoint <br>&emsp; + Thêm filter ngày chạy `?startDate=&endDate=` cho session history | 17/03/2026 | 17/03/2026 | |
| 3   | - Viết **unit test** (JUnit 5 + Mockito) <br>&emsp; + `UserWorkoutPlanServiceTest`: clone, activate, IDOR prevention <br>&emsp; + `HealthCalculationServiceTest`: BMI/BMR/TDEE cho nhiều trường hợp <br>&emsp; + `UserWorkoutSessionServiceTest`: active session query, deactivate | 18/03/2026 | 18/03/2026 | |
| 4   | - Xây dựng **chatService** (Frontend) <br>&emsp; + Gọi trực tiếp AWS Bedrock Runtime API <br>&emsp; + Model: `anthropic.claude-3-5-haiku-20241022-v1:0` <br>&emsp; + System prompt tiếng Việt: persona huấn luyện viên thể dục <br>&emsp; + Gửi 12 lượt hội thoại gần nhất (sliding window) | 19/03/2026 | 19/03/2026 | <https://docs.aws.amazon.com/bedrock/> |
| 5   | - Xây dựng **ChatScreen** (Frontend) <br>&emsp; + Giao diện chat toàn màn hình với bừa chat user/bot <br>&emsp; + Hiệu ứng "đang gõ" (3 chấm nẩy) khi chờ phản hồi <br>&emsp; + 4 chip gợi ý nhanh: "Gợi ý bài tập", "Thực đơn hôm nay", "Mục tiêu calo", "Tư vấn giảm cân" <br>&emsp; + Lời chào của bot bằng tiếng Việt <br>&emsp; + Keyboard avoidance animation | 20/03/2026 | 20/03/2026 | |
| 6   | - Xây dựng **ProfileScreen** (Frontend) <br>&emsp; + Hiển thị avatar, tên, email, username, ngày sinh, giới tính <br>&emsp; + Modal chỉnh sửa ngày sinh và giới tính <br>&emsp; + Đăng xuất: `signOut` + `dispatch(logout)` + xóa secure storage <br>&emsp; + Xóa tài khoản: `deleteUserProfile` + `signOut` — đều có `ConfirmModal` xác nhận | 21/03/2026 | 21/03/2026 | |

### Kết quả đạt được tuần 10:

* **Backend — Hoàn thiện & Testing**:
  * Tất cả DTO có `@Valid` — lỗi validation trả về cấu trúc `ApiResponse` theo field.
  * `PageResponse<T>` được chuẩn hóa cho tất cả paginated endpoint.
  * Unit test pass cho `UserWorkoutPlanService`, `HealthCalculationService`, `UserWorkoutSessionService`.
* **Frontend — AI Chat**:
  * `chatService` gọi Bedrock thành công, chat có context vai trò tiếng Việt.
  * Quick-option chip cho phép tương tác ngay không cần tự gõ.
* **Frontend — Profile**:
  * Load profile từ Redux — không tốn thêm API call.
  * Đăng xuất và xóa tài khoản đều có xác nhận an toàn.

### Kiến thức AWS đã học và giả sử áp dụng cho project:

* Nắm trọn quy trình artifact container: tối ưu Docker build, chuẩn hóa image tag immutable và push image lên Amazon ECR.
* Hiểu mô hình triển khai ECS Fargate qua task definition, service, health check và desired count.
* Học cách tổ chức mạng cho container trên AWS: private subnet, outbound qua NAT và tích hợp ALB target group.
* Biết chiến lược rollout an toàn như rolling update và minimum healthy percent để giảm rủi ro downtime.
* Áp dụng nguyên tắc tách config runtime khỏi image bằng env hoặc secrets injection ở task level.
* Hiểu vai trò của quality gate trong GitHub Actions trước khi cho phép bước deploy lên AWS.
* Liên kết metric vận hành sau deploy với tiêu chí rollback để quyết định release dựa trên dữ liệu thực tế.

Tóm lại, tuần 10 đưa kiến thức AWS sang mức triển khai backend thực tế bằng container platform managed service.

### Kế hoạch tuần tiếp theo:

* **Backend**: Review lần cuối API, hoàn thiện Docker Compose với health check và tài liệu biến môi trường.
* **Frontend**: Xây dựng `HomeScreen` dashboard với 5 API song song, sửa bug còn tồn, polish UX toàn ứng dụng.
