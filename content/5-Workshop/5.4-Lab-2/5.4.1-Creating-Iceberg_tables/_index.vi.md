---
title : "2.1 Tạo các bảng Iceberg"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---


1.  Để tạo Database mới, dán đoạn truy vấn bên dưới vào trình soạn thảo truy vấn và nhấn **Run**. Bạn cần đang ở trong Athena Query Editor để thực thi các lệnh này.

```sql
create database iceberg_database;
```

![create-iceberg-db](/images/5-Workshops/5.4/5.4.1/13.png)

---

2.  Để tạo bảng Iceberg, dán đoạn truy vấn bên dưới vào trình soạn thảo. Thay `<<update-s3-bucket>>` bằng S3 bucket từ bước điều kiện tiên quyết **Tạo S3 bucket**, rồi nhấn **Run**.

Trong thuộc tính bảng, cài đặt `'write_target_data_file_size_bytes'='536870912'` xác định kích thước mục tiêu tính bằng byte cho các file do Athena tạo ra. Trong trường hợp này, kích thước file mục tiêu là 512MB.

```sql
CREATE TABLE iceberg_database.amazon_reviews_iceberg(
marketplace string,
customer_id string,
review_id string,
product_category string,
product_id string,
product_parent string,
product_title string,
star_rating int,
helpful_votes int,
total_votes int,
vine string,
verified_purchase string,
review_headline string,
review_body string,
review_date bigint)
LOCATION 's3://<<update-s3-bucket>>/amazon_reviews_iceberg/'
TBLPROPERTIES (
'table_type'='ICEBERG',
'format'='parquet',
'write_target_data_file_size_bytes'='536870912'
)
```

![Create-iceberg-table](/images/5-Workshops/5.4/5.4.1/14.png)

---

3.  Chèn dữ liệu từ `amazon_reviews_parquet` vào bảng `iceberg_database.amazon_reviews_iceberg`

Dán truy vấn bên dưới vào trình soạn thảo và nhấn **Run**. (Chúng ta chỉ tải một vài Product Categories để giảm thời gian chờ.)

Bước này có thể mất tối đa 1 phút để hoàn thành.

```sql
insert into iceberg_database.amazon_reviews_iceberg
select *
from default.amazon_reviews_parquet
where product_category in ('Gift_Card', 'Apparel','Software')
```

![insert-into-iceberg-table](/images/5-Workshops/5.4/5.4.1/15.png)

---

4.  Xác nhận dữ liệu đã được nạp thành công bằng cách chạy câu truy vấn kiểm tra. Dán lệnh bên dưới vào trình soạn thảo và nhấn **Run**.

```sql
SELECT * FROM "iceberg_database"."amazon_reviews_iceberg" limit 10;
```

![iceberg-test-query](/images/5-Workshops/5.4/5.4.1/16.png)

---

**Chúc mừng! Bạn đã tạo thành công bảng Athena Iceberg. Hãy cùng khám phá một số tính năng chính của Iceberg trên Athena nhé.**