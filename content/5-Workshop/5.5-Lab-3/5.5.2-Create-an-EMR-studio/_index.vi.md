---
title : "Tải bộ dữ liệu hình ảnh lên S3"
date : 2026-03-16
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

Trong bước này, chúng ta sẽ tải bộ dữ liệu hình ảnh lên Amazon S3. Bộ dữ liệu Drone Imagery này chứa 482 hình ảnh được chụp bằng drone cùng với các ground control point có thông tin vị trí chính xác. Bộ dữ liệu này có thể được dùng để kiểm tra cách georeferencing hoạt động thông qua hình ảnh hoặc ground control point.

Truy cập trang Capturing Reality để xem thêm các [bộ dữ liệu mẫu](https://www.capturingreality.com/sample-datasets).

---

1.  **Tải xuống và giải nén bộ dữ liệu hình ảnh**
    
    Tải bộ dữ liệu từ [đây](https://www.capturingreality.com/download/files/GCP-Drone-Sample-Dataset) và giải nén thư mục.

---

2.  **Tạo thư mục input trên S3**
    
    Trên CloudFormation console, mở stack bạn đã tạo ở phần *Setup Workstation* trước đó và vào tab **Resources**.
    
    Kéo xuống cho đến khi bạn thấy tài nguyên có tên **S3 Bucket**, sau đó nhấn vào **Physical ID**. Thao tác này sẽ mở S3 console trong một tab mới.
    
    Nhấn **Create Folder**, đặt tên thư mục là **Images** và giữ nguyên tất cả các thiết lập mặc định khác.
    
    ![S3 Create Folder](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-s3-create-folder.png)

---

3.  **Tải bộ dữ liệu hình ảnh lên S3**
    
    Mở thư mục bộ dữ liệu hình ảnh mà bạn đã tải ở bước 1, rồi tìm các ảnh trong đường dẫn *DroneImagery_GCP/orthoPhoto/Images*.
    
    Trên S3 console, mở thư mục **images**, sau đó nhấn **Upload**.
    
    ![S3 Upload Images](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-s3-upload.png)
    
    Tải ảnh lên S3 bằng cách kéo thả trực tiếp, hoặc nhấn nút **Add Files** để chọn file.
    
    ![S3 Final Upload](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-s3-upload-confirm.png)
    
    Ở cuối màn hình, giữ nguyên tất cả các thiết lập mặc định rồi nhấn **Upload** (bước này sẽ mất khoảng 5 phút).

---

4.  **Tạo thư mục assets**
    
    Quay về thư mục gốc của S3 bucket và tạo một thư mục mới có tên **assets**.

---

5.  **Tải các file Texture Projection Settings và PowerShell Script lên S3**
    
    Tải xuống và giải nén các file sau: [Assets](https://ws-assets-prod-iad-r-iad-ed304a55c2ca1aee.s3.us-east-1.amazonaws.com/e26c223d-6107-4ca8-a3c1-d8da486d7ea2/rc-assets.zip)
    
    Trong S3 console, mở thư mục **assets** đã tạo ở bước 4, rồi nhấn **Upload**.
    
    Tải các file **rcStart**, **rcSave** và **TextureReprojectionSettings** lên thư mục **assets** trên S3.
    
    ✅ **Tìm hiểu thêm về các file assets:**
    * **Texture Reprojection Settings:** File này cho phép bạn chiếu texture từ một model đã được gán texture sang một model khác trong cùng một component được tạo trong RealityCapture. Bạn có thể chiếu texture được tạo trên model có độ chi tiết cao sang một model đã được đơn giản hóa mạnh hơn để rút ngắn đáng kể thời gian xử lý, đồng thời vẫn đạt được texture sắc nét nhất có thể.
    * **rcStart:** Script này chịu trách nhiệm tải bộ dữ liệu hình ảnh từ S3 xuống EC2 instance, kích hoạt giấy phép RealityCapture, và khởi chạy một tác vụ RealityCapture mới với các tham số được cung cấp.
    * **rcSave:** Script này lưu model đầu ra và các file project lên S3.