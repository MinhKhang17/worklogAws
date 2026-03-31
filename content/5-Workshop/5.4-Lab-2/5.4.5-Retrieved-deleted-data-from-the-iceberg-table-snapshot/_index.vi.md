---
title : "2.5 Khôi phục dữ liệu đã xóa từ snapshot bảng Iceberg"
date : 2026-03-25
weight : 5
chapter : false
pre : " <b> 5.4.5 </b> "
---

1.  Lấy lịch sử snapshot của bảng Iceberg bằng truy vấn bên dưới. Dán vào trình soạn thảo và nhấn **Run**.

```sql
SELECT * FROM "iceberg_database"."amazon_reviews_iceberg$history"
```

![retrive-rows](/images/5-Workshops/5.4/5.4.5/23.png)

---

2.  Dùng truy vấn bên dưới để lấy lại các hàng đã xóa từ một snapshot cụ thể và chèn trở lại vào bảng chính. Thay `<<Enter Snapshot ID>>` bằng Snapshot ID phù hợp trước khi chạy. Dán truy vấn vào trình soạn thảo và nhấn **Run**.

```sql
insert into iceberg_database.amazon_reviews_iceberg
select * from iceberg_database.amazon_reviews_iceberg FOR VERSION AS OF  <<Enter Snapshot ID>>
where product_category = 'Software' limit 10
```

![retrive-rows](/images/5-Workshops/5.4/5.4.5/24.png)

---

3.  Truy vấn bảng chính để xác nhận các hàng đã xóa đã được khôi phục thành công. Dán truy vấn bên dưới vào trình soạn thảo và nhấn **Run**.

```sql
Select * from iceberg_database.amazon_reviews_iceberg
where product_category = 'Software' limit 10
```

![rows-retrived](/images/5-Workshops/5.4/5.4.5/25.png)