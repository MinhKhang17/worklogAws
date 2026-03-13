---
title: "Worklog Tuần 11"
date: 2026-03-23
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* **Backend**: Review API lần cuối, hoàn thiện Docker Compose sẵn sàng production, tài liệu biến môi trường.
* **Frontend**: Xây dựng `HomeScreen` dashboard trung tâm, sửa bug còn tồn, polish UX toàn ứng dụng.
* Đạt được ứng dụng hoàn chỉnh, tích hợp đầy đủ, sẵn sàng test cuối.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Xây dựng **HomeScreen** (Frontend) — 5 API song song khi mount <br>&emsp; + Bữa ăn hôm nay: tổng calo → progress bar vs. 2500 kcal <br>&emsp; + BMI từ `HealthCalculation` mới nhất <br>&emsp; + Chiều cao/cân nặng từ `BodyMetric` mới nhất <br>&emsp; + Tên kế hoạch tập active + link nhanh đến PlanDetail <br>&emsp; + Số buổi tập tuần này vs. mục tiêu 4 buổi | 24/03/2026 | 24/03/2026 | |
| 3   | - Hoàn thiện **Docker Compose** <br>&emsp; + Thêm `healthcheck` trên service `postgres` (`pg_isready`) <br>&emsp; + `depends_on.db.condition: service_healthy` cho service API <br>&emsp; + Xác nhận `GET /actuator/health` hoạt động <br>&emsp; + Hoàn chỉnh `.env.example` với mô tả tất cả biến | 25/03/2026 | 25/03/2026 | |
| 4   | - **Sửa bug** toàn diện Frontend <br>&emsp; + `WorkoutSessionScreen`: edge case hoàn thành bài tập cuối <br>&emsp; + `DietScreen`: `ensureDailyMeals` chỉ gọi 1 lần khi mount <br>&emsp; + `HealthDashboardScreen`: hiển loading khi gọi `calculateMetrics` <br>&emsp; + `BMITrendChart`: empty state khi dưới 2 điểm dữ liệu | 26/03/2026 | 26/03/2026 | |
| 5   | - Cải thiện **Response Interceptor** (Axios `client.ts`) <br>&emsp; + Hàng đợi refresh token: nhiều request `401` cùng lúc → chỉ refresh 1 lần duy nhất <br>&emsp; + Nếu refresh thất bại: `forceLogout` xóa token + logout Redux + về Login <br>&emsp; + Xử lý `code === 4040` "user not found" → tự động `forceLogout` | 27/03/2026 | 27/03/2026 | |
| 6   | - **Polish UX** toàn ứng dụng <br>&emsp; + Thêm `NotificationBox` thay thế native `Alert.alert` qua `installAlertProxy` <br>&emsp; + Thêm pull-to-refresh cho `HomeScreen` <br>&emsp; + Chuẩn hóa loading spinner và error state trên tất cả màn hình <br>&emsp; + Kiểm tra nhãn tiếng Việt nhất quán | 28/03/2026 | 28/03/2026 | |

### Kết quả đạt được tuần 11:

* **Backend — Docker Compose**:
  * Health check PostgreSQL đảm bảo API container chờ DB sẵn sàng hoàn toàn.
  * `.env.example` tài liệu đầy đủ 10+ biến môi trường cần thiết.
* **Frontend — HomeScreen**:
  * 5 API song song hoàn thành trong dưới 1.5s trên localhost.
  * Người dùng thấy rõ tiến độ calo và buổi tập ngày/tuần ngay khi mở app.
* **Frontend — Sửa Bug & Polish**:
  * Các bug quan trọng được xử lý; token refresh hoạt động ổn định.
  * `NotificationBox` tạo trải nghiệm thông báo đồng nhất toàn ứng dụng.
  * Nhãn tiếng Việt nhất quán trên tất cả màn hình.

### Kiến thức AWS đã học và giả sử áp dụng cho project:

* Nắm kiến trúc phân phối frontend bằng S3 static hosting kết hợp CloudFront để giảm độ trễ và tăng khả năng mở rộng.
* Hiểu quy trình thiết lập HTTPS đầy đủ với ACM certificate và Route 53 cho DNS routing.
* Học mô hình Origin Access Control để giữ bucket S3 ở trạng thái private nhưng vẫn phục vụ được qua CloudFront.
* Nắm chiến lược cache key và invalidation để cân bằng giữa tốc độ phân phối và độ mới của nội dung giao diện.
* Hiểu vai trò của AWS WAF trong việc giảm các tấn công phổ biến ở lớp web và lưu lượng bất thường.
* Nắm cơ chế xử lý lỗi ở edge và fallback page để SPA routing hoạt động ổn định khi truy cập deep link.
* Chuẩn hóa tư duy release frontend với cache busting, propagation control và khả năng rollback nhanh.

Tóm lại, tuần 11 tập trung vào lớp phân phối frontend trên AWS để chuẩn bị cho môi trường production thực tế.

### Kế hoạch tuần tiếp theo:

* Chạy kiểm thử tích hợp end-to-end toàn bộ ứng dụng.
* Viết tài liệu dự án (README, API reference, sơ đồ kiến trúc).
* Chuẩn bị demo và dọn dẹp code cho bàn giao.
