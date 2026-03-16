---
title : "Lưu vào S3"
date : 2026-03-16 
weight : 4
chapter : false
pre : " <b> 5.3.4 </b> "
---

Trong bước này, chúng ta sẽ sử dụng PowerShell để lưu project RC và mô hình FBX lên S3.

---

1. **Chạy script rcSave**
    
    Trong ứng dụng PowerShell, lưu model và project lên S3 bằng cách chạy script **rcSave** (bỏ dấu ngoặc khi nhập):
    
    ```powershell
    C:\\RealityCapture\\rcSave.ps1 s3://[ENTER S3 BUCKET NAME]/output
    ```
    
    Truy cập **AWS Console** và mở S3 bucket của workshop.
    
    Bây giờ bạn sẽ thấy một thư mục mới có tên **output**, với hai thư mục con: **model** và **project**.

---

2. **(Tùy chọn) Xem nội dung script rcSave**
    
    Trong script PowerShell này có hai lệnh:  
    - Lệnh thứ nhất dùng để tải các tệp **model** lên S3  
    - Lệnh thứ hai dùng để tải các tệp **project** lên S3
    
    ```powershell
    Write-Output "Uploading Models to S3" 
    & "C:\\Program Files\\Amazon\\AWSCLIV2\\aws.exe" s3 cp "c:\\RealityCapture\model" ($Args[0]+"/model") --recursive     
    ```
    
    ```powershell
    Write-Output "Uploading Project to S3" 
    & "C:\\Program Files\\Amazon\\AWSCLIV2\\aws.exe" s3 cp "c:\\RealityCapture\rcproject" ($Args[0] + "/project") --recursive   
    ```

---

✅ **Chúc mừng!**  
Bạn đã hoàn thành tất cả các bước của workshop này. Vui lòng tiếp tục đến phần **Cleanup**.