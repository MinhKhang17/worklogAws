---
title : "2.4 Xóa các hàng khỏi bảng"
date : 2026-03-25
weight : 4
chapter : false
pre : " <b> 5.4.4 </b> "
---

Chúng ta sẽ xóa một số bản ghi khỏi bảng, sau đó khôi phục lại dữ liệu đã xóa thông qua Snapshot của bảng Iceberg.

1.  Xóa tất cả các hàng có product\_category = 'Software'. Dán truy vấn bên dưới vào trình soạn thảo và nhấn **Run**.

```sql
delete from iceberg_database.amazon_reviews_iceberg
where product_category = 'Software'
```

![delete-rows](/images/5-Workshops/5.4/5.4.4/21.png)

---

2.  Chạy truy vấn bên dưới để xác nhận các hàng đã bị xóa — kết quả sẽ trả về không có bản ghi nào. Dán truy vấn vào trình soạn thảo và nhấn **Run**.

```sql
Select * from iceberg_database.amazon_reviews_iceberg
where product_category = 'Software'
```
![delete-rows](/images/5-Workshops/5.4/5.4.4/22.png)