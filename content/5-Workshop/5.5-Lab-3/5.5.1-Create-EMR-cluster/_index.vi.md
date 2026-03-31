---
title : "3.1 Tạo EMR cluster"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

Nếu bạn đang thực hiện workshop này trên tài khoản AWS của riêng mình, hãy làm theo các bước dưới đây để tạo EMR Cluster.

1.  Truy cập [Amazon EMR Console](https://console.aws.amazon.com/emr/home). Trong thanh điều hướng bên trái, dưới mục **EMR on EC2**, chọn **Clusters**.

---

2.  Nhấn nút **Create cluster** ở góc trên cùng bên phải.

![click-create-cluster](/images/5-Workshops/5.5/5.5.1/1.png)

---

3.  Trên trang **Create cluster**, trong mục **Name and applications**, nhập tên mô tả cho cluster ở phần **Cluster name**.

![go-to-advance-option](/images/5-Workshops/5.5/5.5.1/3.png)

4.  Trong mục **Amazon EMR release**, chọn `emr-7.5.0`. Tại phần **Application bundle**, chọn **Custom** để tự chọn các ứng dụng sau:
    
    1.  Hadoop
    2.  Hive
    3.  JupyterEnterpriseGateway
    4.  Spark
    5.  Livy

5.  Mở rộng phần **Software settings**. Từ menu thả xuống **Edit software settings**, chọn **Enter configuration** và dán đoạn JSON sau để bật Iceberg:

```json
[{
  "Classification": "iceberg-defaults",
  "Properties": {
    "iceberg.enabled": "true"
  }
}]
```

> **Lưu ý:** Bài lab này đã được kiểm tra với `EMR 7.5.0`. Các bản phát hành EMR 7.x (7.5.0 trở lên) cũng tương thích. Sử dụng phiên bản EMR cũ hơn có thể gây ra hành vi không mong đợi.

![Create-Cluster-Advanced-Options](/images/5-Workshops/5.5/5.5.1/2.png)

6.  Cuộn xuống phần **Cluster termination**. Mặc định, tùy chọn **Automatically terminate cluster after idle time** được bật. Hãy **tắt** tùy chọn này để cluster tiếp tục hoạt động trong suốt thời gian thực hành workshop.

![Create-Cluster-Advanced-Options](/images/5-Workshops/5.5/5.5.1/4.png)

7.  Giữ nguyên các cài đặt còn lại ở mặc định. Nhấn **Create cluster** để khởi chạy EMR cluster. Cluster sẽ chuyển qua các trạng thái `Starting` → `Bootstrapping` → `Waiting`. **Chờ cho đến khi cluster hiển thị trạng thái `Waiting`** (khoảng 10–15 phút) trước khi chuyển sang bước tiếp theo.

---