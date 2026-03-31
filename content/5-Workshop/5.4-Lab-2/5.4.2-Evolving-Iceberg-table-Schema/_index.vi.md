---
title : "2.2 Thay đổi schema bảng Iceberg"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

Các thay đổi schema trong Iceberg chỉ tác động đến metadata, không có tệp dữ liệu nào bị sửa đổi khi áp dụng thay đổi schema.

Định dạng Iceberg hỗ trợ các loại thay đổi schema sau:

-   Add (Thêm) – Thêm cột mới vào bảng hoặc vào nested struct.
-   Drop (Xóa) – Xóa cột hiện có khỏi bảng hoặc nested struct.
-   Rename (Đổi tên) – Đổi tên cột hoặc trường dữ liệu trong nested struct.
-   Reorder (Sắp xếp lại) – Thay đổi thứ tự các cột.
-   Type promotion (Mở rộng kiểu dữ liệu) – Mở rộng kiểu dữ liệu của cột, trường struct, khóa map, giá trị map, hoặc phần tử list. Các trường hợp được hỗ trợ: \* integer to big integer \* float to double \* tăng độ chính xác của kiểu số thập phân

---

1.  Trong bước này, chúng ta sẽ thêm một cột mới vào bảng Iceberg vừa tạo — cụ thể là cột `comment`.

Dán truy vấn bên dưới vào trình soạn thảo và nhấn **Run**

```sql
ALTER TABLE iceberg_database.amazon_reviews_iceberg ADD COLUMNS (comment string)
```

![add-column](/images/5-Workshops/5.4/5.4.2/17.png)

---

2.  Chúng ta sẽ đặt giá trị cột `comment` thành `High rated` cho tất cả các hàng có đánh giá từ 4 trở lên. Dán truy vấn bên dưới vào trình soạn thảo và nhấn **Run**

```sql
UPDATE iceberg_database.amazon_reviews_iceberg
SET comment = 'High rated'
Where star_rating >=4;
```

Truy vấn này có thể mất vài phút để hoàn thành.

![update-column](/images/5-Workshops/5.4/5.4.2/18.png)

---

3.  Kiểm tra cột đã được thêm thành công bằng cách truy vấn bảng. Dán truy vấn bên dưới vào trình soạn thảo và nhấn **Run**

```sql
SELECT * FROM iceberg_database.amazon_reviews_iceberg
Where star_rating >=4 limit 10
```

Cuộn kết quả sang phải để thấy cột `comment` mới và các giá trị của nó.

![add-column](/images/5-Workshops/5.4/5.4.2/19.png)