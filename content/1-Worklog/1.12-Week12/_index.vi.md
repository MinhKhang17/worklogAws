---
title: "Worklog Tuần 12"
date: 2026-03-30
weight: 12
chapter: false
pre: " <b> 1.12 </b> "
---

### Mục tiêu tuần 12:

* Thực hiện kiểm thử tích hợp end-to-end toàn bộ ứng dụng myFit (tất cả tính năng, tất cả màn hình).
* Viết tài liệu dự án đầy đủ — README, API reference, tổng quan kiến trúc.
* Dọn dẹp code, xóa debug artifacts, chuẩn bị bàn giao dự án.
* Nhìn lại 12 tuần thực tập: bài học kinh nghiệm, điểm mạnh và hướng cải thiện tương lai.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - **Kiểm thử tích hợp** — Backend <br>&emsp; + Kiểm tra tất cả API endpoint với input hợp lệ + không hợp lệ <br>&emsp; + Xác nhận Flyway V1/V2/V3 migration chạy trên DB mới <br>&emsp; + Docker Compose cold start: `db` + `api` healthy dưới 30 giây <br>&emsp; + Rà soát `application.properties` — không có giá trị dev nào lọt sang production | 31/03/2026 | 31/03/2026 | |
| 3   | - **Kiểm thử tích hợp** — Frontend (6 hành trình người dùng) <br>&emsp; + Hành trình 1: Đăng ký → Onboarding → Trang chủ <br>&emsp; + Hành trình 2: Tạo kế hoạch → Clone kế hoạch system → Kích hoạt <br>&emsp; + Hành trình 3: Bắt đầu buổi tập → Log set → Timer nghỉ → Kết thúc → Màn hình Thành công <br>&emsp; + Hành trình 4: Thêm thực phẩm vào 4 bữa → Kiểm tra tổng calo <br>&emsp; + Hành trình 5: Nhập chỉ số cơ thể → BMI/BMR/TDEE tính đúng → Chart hiển thị <br>&emsp; + Hành trình 6: Chat AI → Bedrock phản hồi tiếng Việt | 01/04/2026 | 01/04/2026 | |
| 4   | - Viết **Backend README** (`myFit-api/README.md`) <br>&emsp; + Tổng quan dự án & sơ đồ kiến trúc (API ↔ PostgreSQL ↔ Cognito ↔ S3) <br>&emsp; + Tài liệu từng module: Auth, Food, SystemWorkout, UserWorkoutPlan, Session, UserMetric, Media, GoalType <br>&emsp; + Hướng dẫn cài đặt: prerequisites, biến `.env`, lệnh Docker Compose <br>&emsp; + Bảng API endpoint reference | 02/04/2026 | 02/04/2026 | |
| 4   | - Cập nhật **Frontend** `guide.md` <br>&emsp; + Bảng tech stack <br>&emsp; + Sơ đồ cấu trúc navigation <br>&emsp; + Hướng dẫn cài đặt: `npm install`, biến `.env`, `npx expo start` <br>&emsp; + Danh sách màn hình với mô tả tính năng <br>&emsp; + Ghi chú cấu hình AWS Cognito + Bedrock | 02/04/2026 | 02/04/2026 | |
| 5   | - **Dọn dẹp code** — Backend <br>&emsp; + Xóa `TODO`, `FIXME`, `System.out.println` debug <br>&emsp; + Thêm Javadoc cho method public không hiển nhiên <br>&emsp; + Rà soát security config không để lộ route không mong muốn <br>&emsp; + Build cuối: `mvn clean package -DskipTests` → JAR build thành công | 03/04/2026 | 03/04/2026 | |
| 6   | - **Dọn dẹp code** — Frontend <br>&emsp; + Xóa tất cả `console.log` <br>&emsp; + Chạy `eslint` và sửa cảnh báo lint còn lại <br>&emsp; + Xóa import không dùng <br>&emsp; + Build cuối: `npx expo export` → zero TypeScript error <br> - **Tổng kết dự án**: tài liệu bài học kinh nghiệm, quyết định kỹ thuật và hướng cải thiện tương lai | 04/04/2026 | 04/04/2026 | |

### Kết quả đạt được tuần 12:

* **Kiểm thử tích hợp**:
  * Tất cả API endpoint backend vượt qua test thủ công với input hợp lệ và không hợp lệ.
  * Docker Compose cold start đáng tin cậy — API healthy trong 25 giây sau `docker-compose up`.
  * Flyway V1, V2, V3 migration chạy sạch trên PostgreSQL mới.
  * Tất cả 6 hành trình người dùng test end-to-end không có lỗi nghiêm trọng.
* **Tài liệu**:
  * `myFit-api/README.md` bao gồm hướng dẫn cài đặt đầy đủ, bảng biến môi trường, và mô tả endpoint.
  * Frontend `guide.md` cập nhật sơ đồ navigation, danh sách màn hình, và cấu hình AWS.
  * Tổng quan kiến trúc: Spring Boot API ↔ PostgreSQL ↔ AWS Cognito ↔ AWS S3 ↔ React Native ↔ AWS Bedrock.
* **Chất lượng Code**:
  * Zero `console.log` hay `System.out.println` còn lại trong production code.
  * TypeScript build (`npx expo export`) không có lỗi.
  * Maven `mvn clean package` build JAR thành công.
* **Tổng kết dự án — Bài học kinh nghiệm**:
  * **Ngăn chặn IDOR** qua trích xuất `sub` từ JWT là pattern bảo mật quan trọng phải áp dụng nhất quán trong REST API phân quyền theo user.
  * **Soft delete** với `@SQLRestriction` linh hoạt hơn hard delete cho dữ liệu thuộc sở hữu người dùng — cho phép khôi phục tiềm năng.
  * **JWT Stateless** loại bỏ phức tạp quản lý session phía server, đánh đổi bằng độ phức tạp của token revocation (giải quyết bằng forced logout + refresh queue).
  * **React Native + NativeWind** là bộ đôi mạnh mẽ — cú pháp TailwindCSS quen thuộc tăng tốc đáng kể phát triển UI mobile.
  * **Redux + React Query** phân tách rõ ràng: Redux quản lý auth/session state; React Query quản lý server cache và background refetch.
  * **Hướng cải thiện tương lai**: Deploy Backend lên AWS ECS (Fargate) + ALB HTTPS; Frontend bundle lên CloudFront + S3; CI/CD qua GitHub Actions (đã scaffolded trong `.github/workflows/`).

### Kiến thức AWS đã học và giả sử áp dụng cho project:

* Thực hiện đánh giá kiến trúc theo 5 trụ cột Well-Architected gồm Security, Reliability, Performance Efficiency, Cost Optimization và Operational Excellence.
* Ghi nhận mức độ sẵn sàng tin cậy của hệ thống qua health check dependency, backup/restore plan và mục tiêu RPO/RTO thực tế.
* Áp dụng tư duy FinOps bằng cách rà soát right-sizing, budget alert, lifecycle policy và dọn tài nguyên không dùng ở non-production.
* Tổng hợp checklist hardening bảo mật gồm IAM review, token policy, secret handling, mã hóa dữ liệu và audit logging.
* Chuẩn bị runbook vận hành cloud cho deploy, rollback, xử lý sự cố và kiểm tra định kỳ.
* Hoàn thiện tiêu chí bàn giao như tái tạo môi trường được, tài liệu biến môi trường rõ ràng và ownership minh bạch.
* Đề xuất roadmap AWS tiếp theo gồm tăng độ chặt ECS cộng ALB, tối ưu CloudFront, nâng mức observability và rollout theo giai đoạn.

Tóm lại, tuần 12 biến toàn bộ kiến thức AWS đã học thành một khung đánh giá, vận hành và bàn giao hoàn chỉnh cho dự án.
