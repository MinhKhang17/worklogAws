---
title : "2.3 Truy vấn du hành thời gian và du hành phiên bản"
date : 2026-03-25
weight : 3
chapter : false
pre : " <b> 5.4.3 </b> "
---

1.  Hãy lấy lịch sử snapshot của bảng Iceberg bằng truy vấn bên dưới. Dán vào trình soạn thảo và nhấn **Run**. Sao chép giá trị **snapshot_id** cũ hơn — bạn sẽ cần nó ở bước tiếp theo.

```sql
SELECT * FROM "iceberg_database"."amazon_reviews_iceberg$history"
```

![snapshot-timetravel](/images/5-Workshops/5.4/5.4.3/20.png)

---

2.  Bây giờ hãy truy vấn snapshot từ trước khi chúng ta thêm cột `comment`. Dán truy vấn bên dưới vào trình soạn thảo, thay thế phần giữ chỗ `snapshot_id` bằng giá trị cũ hơn bạn đã sao chép, rồi nhấn **Run**.

Sau khi chạy, xác nhận rằng kết quả không có cột `comment`.

```sql
select * from iceberg_database.amazon_reviews_iceberg FOR VERSION AS OF  <<replace snapshot_id>>
where marketplace ='UK'
```

![retrive-snapshot](/images/5-Workshops/5.4/5.4.3/21.png)

---

3.  Chúng ta cũng có thể sử dụng timestamp `made_current_at` để truy vấn một snapshot cụ thể. Dán truy vấn bên dưới vào trình soạn thảo, thay thế phần giữ chỗ bằng giá trị timestamp thực tế, rồi nhấn **Run**.

**Ngoài ra**, bạn có thể dùng trực tiếp giá trị của cột `made_current_at` để truy cập snapshot theo thời gian.

```sql
select * from iceberg_database.amazon_reviews_iceberg for TIMESTAMP AS OF TIMESTAMP '<<replace with made_current_at time>>' 
where marketplace ='UK'
```
