---
title : "1.2 Tạo Athena tables"
date : 2026-03-25 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

1.  Truy cập [Athena Console](https://console.aws.amazon.com/athena/home)
    
    ---
    
2.  Mở **Query Editor** (không phải Notebook editor)
    
    ---
![open query editor](/images/5-Workshops/5.3/5.3.2/5.png)

3.  Sau khi vào trong Query Editor của Athena console, nhấn vào **Edit Settings** như hình bên dưới:
    

![Athena console](/images/5-Workshops/5.3/5.3.2/6.png)

---

1.  Vào **Settings** rồi nhấn **Manage**

![Athena Settings](/images/5-Workshops/5.3/5.3.2/7.png)

---

4.  Trong Manage Settings, nhấn **Browse S3**.

![Athena Settings](/images/5-Workshops/5.3/5.3.2/8.png)

---

5.  Chọn S3 bucket bằng cách tích vào nút radio tương ứng rồi nhấn **Choose**. Với self-paced labs, chọn bucket đã tạo trước đó. Với AWS Events, chọn bucket có tên iceberg-workshop-ACCOUNTID (ví dụ: iceberg-workshop-123456789).

![Choose-S3-data-set](/images/5-Workshops/5.3/5.3.2/9.png)

---

6.  Nhấn **Save** để lưu vị trí S3 output.

![Save-s3-location](/images/5-Workshops/5.3/5.3.2/10.png)

---

7.  Chuyển sang tab **Editor**, dán câu truy vấn bên dưới. Thay **YOURBUCKET** bằng tên S3 bucket của bạn, rồi nhấn **Run**.

```sql
CREATE EXTERNAL TABLE default.amazon_reviews_parquet(
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
ROW FORMAT SERDE 
'org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe' 
STORED AS INPUTFORMAT 
'org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat' 
OUTPUTFORMAT 
'org.apache.hadoop.hive.ql.io.parquet.MapredParquetOutputFormat'
LOCATION
's3://YOURBUCKET/productreviews/'; 
```

![Run-athena-create-table](/images/5-Workshops/5.3/5.3.2/11.png)

---

8.  Dán đoạn lệnh bên dưới vào trình soạn thảo truy vấn và nhấn **Run**.

Lệnh `MSCK REPAIR TABLE` quét hệ thống tệp (chẳng hạn Amazon S3) để phát hiện các phân vùng tương thích Hive đã được thêm vào sau khi bảng được tạo. Lệnh này so sánh phân vùng trong metadata của bảng với phân vùng trên S3. Nếu phân vùng mới tồn tại ở vị trí S3 được chỉ định, chúng sẽ được tự động cập nhật vào metadata và bảng Athena.

```sql
MSCK REPAIR TABLE default.amazon_reviews_parquet;
```
![Run-athena-repair-table](/images/5-Workshops/5.3/5.3.2/12.png)
---

**Bảng Athena đã được tạo thành công. Bảng này (`default.amazon_reviews_parquet`) sẽ được dùng làm nguồn dữ liệu để nạp vào các bảng Iceberg trong bài lab tiếp theo.**