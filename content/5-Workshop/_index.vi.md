---
title: "Workshop"
date : 2026-03-25 
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

## Xây dựng Data Lake Hiện Đại với Apache Iceberg trên AWS

Bài thực hành này được xây dựng nhằm mang lại trải nghiệm thực chiến trong việc triển khai một Transactional Data Lake sử dụng [Apache Iceberg](https://iceberg.apache.org/) trên Amazon EMR và Amazon Athena. Apache Iceberg là một định dạng bảng mở, phù hợp với các tập dữ liệu phân tích cực kỳ lớn mà ít có sự biến đổi. Định dạng này ra đời nhằm khắc phục những hạn chế của bố cục bảng truyền thống vốn có trong Hive, Trino và Spark. Các dịch vụ AWS hiện hỗ trợ định dạng bảng Apache Iceberg bao gồm:

1. Amazon Athena.  
2. Amazon EMR.

Trong bài thực hành này, chúng ta sẽ thực hành phân tích S3 Data Lake thông qua cả Amazon Athena lẫn Amazon EMR với sự hỗ trợ của định dạng bảng Iceberg. Để thực hiện bài thực hành, bạn cần có kiến thức cơ bản về các lệnh SQL cho các phần lab Athena và có hiểu biết về PySpark cho các phần lab EMR.

---

**Đối tượng hướng đến:** Kỹ sư dữ liệu (Data Engineers), Nhà phân tích dữ liệu (Data Analysts), Kỹ sư đám mây (Cloud Engineers), Nhà phát triển Big Data (Big Data Developers)

**Các tình huống ứng dụng:** Xây dựng transactional data lakes, truy vấn dữ liệu S3 qua Athena, xử lý dữ liệu bằng EMR & PySpark, quản lý dữ liệu dạng bảng quy mô lớn bằng Apache Iceberg, và nâng cấp kiến trúc data lake hiện đại

---

✅ **Thời lượng ước tính:** 2-3 giờ

⚠️ **Dọn dẹp tài nguyên:** Sau khi hoàn thành bài thực hành, tham khảo phần **Dọn dẹp** (Cleanup) để xóa các tài nguyên đã tạo và tránh phát sinh chi phí ngoài mong muốn.