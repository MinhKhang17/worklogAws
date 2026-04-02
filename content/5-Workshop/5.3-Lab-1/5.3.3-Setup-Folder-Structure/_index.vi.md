---
title : "5.3.3 - Thiết Lập Cấu Trúc Thư Mục"
date : 2026-03-25
weight : 3
chapter : false
pre : " <b> 5.3.3. </b> "
---

## Hướng Dẫn Từng Bước: Thiết Lập Cấu Trúc Thư Mục S3

### Mục Tiêu
Tạo cấu trúc thư mục có tổ chức trong bucket S3 để lưu trữ các bộ dữ liệu, metadata, và nhật ký giao dịch.

---

## Tổng Quan: Cấu Trúc Thư Mục

Chúng tôi sẽ tạo cấu trúc sau:
```
ev-data-marketplace-datasets-xxxxx/
├── /datasets/          (Tệp bộ dữ liệu EV)
├── /metadata/          (Metadata và mô tả bộ dữ liệu)
├── /logs/              (Ghi nhật ký giao dịch và truy cập)
└── /backups/           (Các bản sao lưu)
```

---

## Bước 1: Mở S3 Bucket Của Bạn

1. Điều hướng đến dashboard S3
2. Tìm và nhấp vào bucket của bạn: `ev-data-marketplace-datasets-xxxxx`
3. Bạn sẽ thấy một bucket trống (không có objects)


---

## Bước 2: Tạo Thư Mục `/datasets/`

1. Nhấp vào nút **Create folder**
2. Trong trường tên thư mục, gõ: `datasets`
3. Nhấp vào nút **Create folder**
4. Thư mục `/datasets/` sẽ xuất hiện trong bucket


---

## Bước 3: Tạo Thư Mục `/metadata/`

1. Nhấp vào nút **Create folder** lại
2. Trong trường tên thư mục, gõ: `metadata`
3. Nhấp vào nút **Create folder**
4. Thư mục `/metadata/` sẽ xuất hiện trong bucket


---

## Bước 4: Tạo Thư Mục `/logs/`

1. Nhấp vào nút **Create folder**
2. Trong trường tên thư mục, gõ: `logs`
3. Nhấp vào nút **Create folder**
4. Thư mục `/logs/` sẽ xuất hiện trong bucket


---

## Bước 5: Tạo Thư Mục `/backups/`

1. Nhấp vào nút **Create folder**
2. Trong trường tên thư mục, gõ: `backups`
3. Nhấp vào nút **Create folder**
4. Thư mục `/backups/` sẽ xuất hiện trong bucket


---

## Bước 6: Xác Minh Tất Cả Thư Mục

1. Bucket của bạn sẽ hiển thị tất cả bốn thư mục chính:
   - datasets/
   - metadata/
   - logs/
   - backups/


---

## Bước 7: Tạo Thư Mục Con Trong `/datasets/`

Bây giờ chúng ta sẽ tạo các thư mục con trong datasets để tổ chức dữ liệu theo loại:

### 7.1: Mở thư mục datasets

1. Nhấp vào thư mục `datasets/` để mở nó
2. Bên trong, tạo các thư mục con sau bằng cách nhấp **Create folder** cho mỗi:
   - `ev-battery-data`
   - `ev-charging-data`
   - `ev-economic-data`
   - `ev-location-data`


---

## Bước 8: Tạo Thư Mục Con Trong `/metadata/`

1. Điều hướng lại gốc bucket
2. Nhấp vào thư mục `metadata/`
3. Tạo các thư mục con sau:
   - `dataset-descriptions`
   - `pricing-info`
   - `user-profiles`
   - `purchase-history`


---

## Bước 9: Tạo Thư Mục Con Trong `/logs/`

1. Điều hướng lại gốc bucket
2. Nhấp vào thư mục `logs/`
3. Tạo các thư mục con sau:
   - `access-logs`
   - `transaction-logs`
   - `error-logs`


---

## Cấu Trúc Thư Mục Cuối Cùng

Sau khi hoàn thành tất cả các bước, cấu trúc bucket của bạn sẽ trông như sau:

```
ev-data-marketplace-datasets-xxxxx/
├── datasets/
│   ├── ev-battery-data/
│   ├── ev-charging-data/
│   ├── ev-economic-data/
│   └── ev-location-data/
├── metadata/
│   ├── dataset-descriptions/
│   ├── pricing-info/
│   ├── user-profiles/
│   └── purchase-history/
├── logs/
│   ├── access-logs/
│   ├── transaction-logs/
│   └── error-logs/
└── backups/
```


---

## Tóm Tắt

Bạn đã thiết lập thành công cấu trúc S3 bucket có tổ chức với:
- **Thư mục chính** để tổ chức logic (datasets, metadata, logs, backups)
- **Thư mục con** theo loại dữ liệu và mục đích
- **Tách biệt rõ ràng** các mối quan tâm cho khả năng mở rộng
- **Nền tảng sẵn sàng** cho tải lên và quản lý dữ liệu

**Lab 1 Hoàn Tất!** Bucket S3 của bạn hiện được cấu hình đầy đủ và sẵn sàng sử dụng trong marketplace.

---

## Tiếp Theo: Tiến Hành Lab 2 - Tạo IAM Users và Policies
