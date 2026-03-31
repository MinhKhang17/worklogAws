---
title : "3.2 Thiết lập EMR Studio và kết nối với EMR cluster"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

**A. Lấy VPC và Subnet ID của EMR cluster**

1.  Truy cập [Amazon EMR Console](https://console.aws.amazon.com/emr/home). Trong thanh điều hướng bên trái, dưới mục **EMR on EC2**, chọn **Clusters**.

2.  Nhấn **Cluster ID** của cluster để mở trang chi tiết. Chuyển sang tab **Summary** và cuộn xuống phần **Network and security**. Sao chép cả **VPC ID** và **Subnet ID** — bạn sẽ cần chúng khi tạo Studio.

---

**B. Tạo EMR Studio và Workspace**

1.  Vẫn trong thanh điều hướng bên trái, dưới mục **EMR on EC2**, chọn **Studios**. Sau đó nhấn **Create Studio**.

    ![EMRStudioPage](/images/5-Workshops/5.5/5.5.2/1.png)
    ![EMRStudioPage2](/images/5-Workshops/5.5/5.5.2/2.png)

2.  Trên trang **Create a Studio**:
    - Chọn **Custom setup**.
    - Nhấn **Browse S3** để chọn S3 bucket làm nơi lưu trữ notebook.
    - Trong mục **Service role**, chọn **EMR\_Iceberg\_Notebook\_Role**.

    ![Create Studio Bucket/Role](/images/5-Workshops/5.5/5.5.2/3.png)

3.  Cuộn xuống phần **Networking and security**. Chọn **VPC ID** và **Subnet ID** đã sao chép ở Bước A.2. Sau đó nhấn **Create Studio**.

    ![Create Studio Bucket/Role](/images/5-Workshops/5.5/5.5.2/4.png)
    ![Create Studio Bucket/Role2](/images/5-Workshops/5.5/5.5.2/5.png)   

4.  Sau khi Studio được tạo, nhấn **Launch Studio** để mở trong tab trình duyệt mới. Bạn sẽ thấy giao diện JupyterLab.

    > **Lưu ý:** Nếu tab mới không tự động mở, hãy kiểm tra tính năng chặn popup của trình duyệt và cho phép popup từ domain của AWS Console.

5.  Trong giao diện JupyterLab, nhấn biểu tượng **Cluster** (hoặc **Compute**) ở thanh bên trái. Trong phần **Compute type**, chọn **EMR on EC2 cluster**, sau đó chọn cluster của bạn từ danh sách thả xuống. Nhấn **Attach** ở cuối bảng để kết nối cluster với workspace.

    ![Create Studio Bucket/Role](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/AttachCluster.png)


**Chúc mừng! Thiết lập EMR Studio/Workspace đã hoàn tất. Bây giờ hãy cùng khám phá các tính năng Iceberg trên EMR.**