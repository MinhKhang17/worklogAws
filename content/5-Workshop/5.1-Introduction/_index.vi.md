---
title : "Giới thiệu về Apache Iceberg trên AWS"
date : 2026-03-25 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

[Apache Iceberg](https://iceberg.apache.org/) là một định dạng bảng mở được thiết kế đặc biệt cho các tập dữ liệu phân tích cực kỳ lớn. Định dạng này hỗ trợ nhiều tác vụ data lake hiện đại như chèn (insert), cập nhật (update), xóa (delete) ở cấp độ bản ghi và truy vấn du hành thời gian (time travel). Iceberg tổ chức các tập hợp tệp lớn dưới dạng các bảng có cấu trúc, cho phép tiến hóa schema và phân vùng một cách trơn tru mà không cần viết lại dữ liệu. Kiến trúc của nó được tối ưu hóa riêng cho Amazon S3 và đảm bảo tính nhất quán dữ liệu ngay cả trong các tình huống ghi đồng thời.

---

Một số thuật ngữ quan trọng trong Apache Iceberg bao gồm:

-   Schema – Tên và kiểu dữ liệu của tất cả các trường trong một bảng.
-   Partition spec – Định nghĩa cách tính các giá trị phân vùng từ các trường dữ liệu.
-   Snapshot – Ảnh chụp trạng thái bảng tại một thời điểm, bao gồm toàn bộ tập hợp các tệp dữ liệu tại thời điểm đó.
-   Manifest list – Tệp liệt kê tất cả các manifest file liên kết với một snapshot nhất định.
-   Manifest – Tệp chứa danh sách các data file hoặc delete file tạo nên một phần của snapshot.
-   Data file – Tệp chứa dữ liệu hàng thực tế của bảng.
-   Delete file – Tệp ghi lại những hàng đã bị xóa, theo vị trí hoặc theo giá trị dữ liệu.

---

Iceberg theo dõi từng tệp dữ liệu riêng lẻ thay vì theo thư mục. Các writer có thể tạo tệp độc lập và thêm vào bảng bằng một commit duy nhất và rõ ràng. Trạng thái bảng được lưu trữ trong các metadata file, và mỗi thay đổi đối với bảng sẽ tạo ra một metadata file mới thay thế file cũ theo cơ chế nguyên tử (atomically). Metadata file lưu trữ schema bảng, cấu hình phân vùng và toàn bộ lịch sử snapshot. Mỗi snapshot đại diện cho trạng thái đầy đủ của bảng tại một thời điểm cụ thể và là điểm truy cập để truy vấn toàn bộ tập dữ liệu.

Mỗi snapshot là một ảnh hoàn chỉnh của dữ liệu tại một thời điểm nhất định. Các snapshot được liệt kê trong metadata file, nhưng tham chiếu tệp thực tế nằm rải rác ở các manifest file riêng biệt. Việc chuyển đổi nguyên tử giữa các metadata file cung cấp khả năng cách ly snapshot, cho phép người đọc làm việc với phiên bản nhất quán mà không bị ảnh hưởng bởi các thay đổi đang diễn ra. Đường dẫn tệp dữ liệu được lưu trong manifest, mỗi manifest chứa siêu dữ liệu về từng tệp bao gồm thông tin phân vùng và thống kê. Manifest có thể được chia sẻ giữa các snapshot để giảm thiểu việc ghi lại siêu dữ liệu không thay đổi.

---

**Apache Iceberg trên Amazon Athena**

Các bảng Iceberg đã đăng ký trong AWS Glue catalog được Athena hỗ trợ đầy đủ, tuân theo thông số kỹ thuật của [Glue Catalog implementation](https://iceberg.apache.org/docs/latest/aws/#glue-catalog) mã nguồn mở. Athena hỗ trợ bảng Iceberg v2 ở định dạng Parquet. Để tạo bảng Iceberg qua Athena, đặt thuộc tính `table_type` thành `ICEBERG` trong mệnh đề `TBLPROPERTIES`, như cú pháp bên dưới:

```sql
CREATE TABLE
  [db_name.]table_name (col_name data_type [COMMENT col_comment] [, ...] )
  [PARTITIONED BY (col_name | transform, ... )]
  LOCATION 's3://DOC-EXAMPLE-BUCKET/your-folder/'
  TBLPROPERTIES ( 'table_type' ='ICEBERG' [, property_name=property_value] )
```

---

**Apache Iceberg trên Amazon EMR**

Từ Amazon EMR phiên bản 7.5.0, bạn có thể chạy Apache Spark 3 trên EMR cluster với hỗ trợ định dạng bảng Iceberg. EMR 7.5.0 đi kèm với Iceberg phiên bản 1.6.0. Để kích hoạt hỗ trợ Iceberg, hãy thêm phân loại (classification) sau vào cấu hình cluster:

```java
[{ "Classification":"iceberg-defaults",
    "Properties":{"iceberg.enabled":"true"}
}]
```

Ngoài ra, bạn có thể tạo EMR cluster kèm ứng dụng Spark và đưa tệp `/usr/share/aws/iceberg/lib/iceberg-spark3-runtime.jar` vào làm dependency JAR trong các Spark job của mình.

Bài thực hành này dự kiến kéo dài tối đa 2 giờ. Vui lòng sử dụng region **us-east-1** trong suốt quá trình thực hành, vì bộ dữ liệu sử dụng trong bài nằm ở region này.