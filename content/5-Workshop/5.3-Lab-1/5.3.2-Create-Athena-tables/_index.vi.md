---
title : "Khởi chạy Job"
date : 2026-03-16 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

Trong bước này, chúng ta sẽ sử dụng PowerShell để khởi chạy một job RealityCapture. Job này sẽ thực hiện các bước sau: 1/ căn chỉnh bộ dữ liệu hình ảnh, 2/ xây dựng mô hình base high poly, 3/ tạo texture cho mô hình, 4/ đơn giản hóa mesh thành phiên bản low poly.

---

1.  **Kiểm tra AWS CLI**
    
    Trên desktop của virtual workstation, gõ *PowerShell* vào thanh tìm kiếm và mở ứng dụng **Windows PowerShell**.
    
    Kiểm tra xem AWS CLI đã được cài đặt hay chưa bằng cách chạy lệnh:
    
    ```powershell
    aws --version
    ```
    
    Nếu đầu ra hiển thị đường dẫn cài đặt, bạn có thể bỏ qua và chuyển sang bước tiếp theo. Nếu không, hãy làm theo hướng dẫn bên dưới để tải AWS CLI.
    
    Cài đặt AWS CLI bằng cách chạy lệnh sau:
    
    ```powershell
    msiexec.exe /i [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi)
    ```
    
    Hoàn tất trình hướng dẫn cài đặt và giữ nguyên mọi tùy chọn mặc định.

---

2.  **Thiết lập thông tin xác thực PowerShell**
    
    **INTERNAL**
    
    Nếu đang sử dụng tài khoản Isengard, hãy truy cập [AWS Console Access Dashboard](https://isengard.amazon.com/console-access). Mở menu temporary credentials của tài khoản Isengard mà bạn đang dùng cho workshop này.
    
    Mở rộng menu xổ xuống *PowerShell*, rồi nhấn **Copy Powershell**.
    
    ![Set Temporary Credentials](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-temp-creds.png)
    
    Để thiết lập temporary credentials, sao chép và dán các thông tin xác thực đó vào ứng dụng PowerShell trên virtual workstation, rồi nhấn **Enter**.
    
    **EXTERNAL**
    
    Làm theo [hướng dẫn này](https://docs.aws.amazon.com/powershell/latest/userguide/creds-idc-cli.html) để cấu hình credentials cho PowerShell sử dụng IAM Identity Center và AWS CLI.

---

3.  **Tạo các thư mục job**
    
    Di chuyển tới thư mục `"C:/"` bằng lệnh sau:
    
    ```powershell
    cd ../..
    ```
    
    Tạo một thư mục mới tên là RealityCapture:
    
    ```powershell
    New-Item -Path "C:\" -Name "RealityCapture" -ItemType Directory
    ```
    
    Tạo ba thư mục con có tên `"model"`, `"s3-input-images"`, `"rcproject"`:
    
    ```powershell
    New-Item -Path C:\RealityCapture\model,C:\RealityCapture\s3-input-images,C:\RealityCapture\rcproject -ItemType Directory
    ```

---

4.  **Tải các file assets**
    
    Trên S3 console, vào S3 bucket của workshop và sao chép S3 URI của thư mục **assets** như minh họa trong hình bên dưới:
    
    ![S3 Assets URI](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-assets-s3-uri.png)
    
    Tải các PowerShell script và file Texture Settings từ S3 về workstation bằng lệnh sau (xóa dấu ngoặc khi thay nội dung):
    
    ```powershell
    aws s3 sync "[ENTER S3 URI OF ASSETS FOLDER]" C:\RealityCapture
    ```

---

5.  **Chạy script rcStart**
    
    Tương tự bước 4, hãy sao chép S3 URI của thư mục **images**.
    
    ℹ️ **Chạy RealityCapture từ PowerShell**  
    Trong lệnh bên dưới, chúng ta chạy file script **rcStart.ps1** với bốn tham số: 1/ tên job, 2/ S3 input bucket/folder, 3/ số lượng polygon mục tiêu cho bước simplify, 4/ khóa kích hoạt RealityCapture.
    
    Khởi chạy một RC job mới bằng cách thực thi file script **rcStart** (xóa dấu ngoặc khi thay nội dung):
    
    ```powershell
    C:\\RealityCapture\\rcStart.ps1 DroneImagery [ENTER S3 URI OF IMAGES FOLDER] 1000000
    ```
    
    ⚠️ **Ước tính thời gian chạy (dựa trên kích thước instance)**
    * g5.2xlarge = ~18 phút
    * g5.4xlarge = ~15 phút
    * g5.8xlarge = ~12 phút

---

6.  **(Tùy chọn) Xem output của PowerShell**
    
    Nếu bạn kiểm tra output của PowerShell, bạn sẽ thấy log của từng bước trong quá trình chạy job.
    
    ![PowerShell job start](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-powershell-start.png)
    
    ![PowerShell job complete](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-powershell-complete.png)

---

7.  **(Tùy chọn) Xem nội dung script rcStart**
    
    Trong file script **rcStart.ps1**, hãy xem lệnh *Running RC* ở dòng 48. Lệnh này kết hợp các bước căn chỉnh ảnh (`-align`), dựng mesh (`-calculateNormalModel`), đơn giản hóa mesh (`-simplify`) và tạo texture (`-calculateTexture`) vào trong một câu lệnh duy nhất:
    
    ```powershell
    Write-Output "Running RC..." 
    & "C:\Program Files\Capturing Reality\RealityCapture\RealityCapture.exe" -newScene -headless -set "appQuitOnError=true"  -set "appProcessAction=ExecuteProgram" -set "appProcessActionTime=0" -stdConsole -writeProgress "C:\RealityCapture\ProcessingProgress.txt" -addFolder "C:\RealityCapture\s3-input-images" -align -selectMaximalComponent -setReconstructionRegionAuto -calculateNormalModel -renameSelectedModel HighPoly -calculateTexture -simplify ${simp} -renameSelectedModel LowPoly -unwrap -reprojectTexture HighPoly LowPoly C:\RealityCapture\TextureReprojectionSettings.xml -selectModel LowPoly -selectMarginalTriangles -removeSelectedTriangles -selectModel LowPoly -exportModel LowPoly C:\RealityCapture\model\LowPolyModel.fbx -save C:\RealityCapture\rcproject\Project.rcproj -quit
    ```
    
    Điều này cho thấy khả năng xâu chuỗi nhiều lệnh thành một quy trình thực thi kết hợp. Để xem đầy đủ danh sách các lệnh CLI của RealityCapture, hãy tham khảo [tài liệu Capturing Reality](https://rchelp.capturingreality.com/en-US/tutorials/commandline.htm).