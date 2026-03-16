---
title : "Thiết lập RealityCapture"
date : 2026-03-16 
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---

Bây giờ chúng ta đã kết nối tới EC2 instance và có quyền truy cập vào virtual desktop, bước tiếp theo là hoàn tất thiết lập workstation và kích hoạt [RealityCapture](https://www.capturingreality.com/realitycapture/). RealityCapture là một phần mềm quang trắc ảnh (photogrammetry) dành cho Windows, cho phép bạn tạo các mô hình 3D siêu chân thực từ một tập hợp ảnh và/hoặc dữ liệu quét laser.

---

1.  **(Tùy chọn) Điều chỉnh cài đặt hiển thị**
    
    Trên máy trạm ảo, nhấp chuột phải vào màn hình desktop và chọn **Display settings** trong menu.
    
    Chọn màn hình hiển thị của bạn, sau đó kéo xuống phần **Scale and layout**.
    
    Trong menu xổ xuống, điều chỉnh tỉ lệ hiển thị thành **150%** hoặc **175%**, hoặc bất kỳ kích thước nào phù hợp nhất với màn hình của bạn.

---

2.  **Tắt Internet Explorer Enhanced Security Settings**
    
    Gõ *PowerShell* vào thanh tìm kiếm và mở ứng dụng **Windows PowerShell**.
    
    Sao chép/dán đoạn mã sau vào PowerShell, rồi nhấn **Enter**:
    
    ```powershell
    function Disable-IEESC {
    $AdminKey = "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}"
    $UserKey = "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}"
    Set-ItemProperty -Path $AdminKey -Name "IsInstalled" -Value 0
    Set-ItemProperty -Path $UserKey -Name "IsInstalled" -Value 0
    Stop-Process -Name Explorer
    Write-Host "IE Enhanced Security Configuration (ESC) has been disabled." -ForegroundColor Green }
    Disable-IEESC
    ```
    
    Thao tác này sẽ tắt các thiết lập bảo mật nâng cao của Internet Explorer.

---

3.  **Cài đặt Epic Games Launcher**
    
    Trước khi có thể cài đặt và khởi chạy RealityCapture, bạn cần tải Epic Games Launcher.
    
    Vào thư mục *Downloads* và tìm file **EpicInstaller**. Mở file này và thực hiện lần lượt các bước trong trình hướng dẫn cài đặt. Bạn có thể giữ nguyên toàn bộ tùy chọn mặc định. **Quá trình cài đặt sẽ mất khoảng 1-2 phút.**
    
    Nếu bạn không thấy file **EpicInstaller** trong thư mục Downloads, hãy mở trình duyệt Microsoft Edge và truy cập trang web [RealityCapture](https://www.capturingreality.com/realitycapture/).
    
    Nhấn nút **Download now** ở góc trên bên phải màn hình, sau đó ở trang tiếp theo, nhấn **Download Launcher**.
    
    Mở file vừa tải về và thực hiện lần lượt các bước trong trình hướng dẫn cài đặt. Bạn có thể giữ nguyên toàn bộ tùy chọn mặc định. **Quá trình cài đặt sẽ mất khoảng 1-2 phút.**

---

4.  **Cài đặt RealityCapture**
    
    Mở Epic Games Launcher. Đăng nhập nếu bạn đã có tài khoản Epic Games, hoặc tạo tài khoản mới nếu chưa có.
    
    Trình hướng dẫn cài đặt RealityCapture có thể tự động xuất hiện trên màn hình. Nếu có, hãy hoàn tất quá trình cài đặt (giữ nguyên mọi tùy chọn mặc định) rồi chuyển sang bước tiếp theo.
    
    Nếu trình hướng dẫn cài đặt RealityCapture không tự xuất hiện, hãy vào mục Unreal Engine trong launcher và chọn tab **RealityCapture**. Sau đó nhấn **Install**.
    
    ![Epic Games Launcher](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-epic-launcher.png)
    
    Chấp nhận thỏa thuận cấp phép người dùng cuối (End User License Agreement) của RealityCapture, sau đó hoàn tất các bước trong trình hướng dẫn cài đặt (giữ nguyên toàn bộ tùy chọn mặc định). Lúc này bạn sẽ thấy shortcut của RealityCapture trên Desktop.

---

5.  **Khởi chạy ứng dụng**
    
    Nếu chưa được mở tự động, bây giờ bạn có thể mở ứng dụng RealityCapture.
    
    ![RC Launch](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-welcome-screen.png)