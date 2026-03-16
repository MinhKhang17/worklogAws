---
title : "Xem kết quả đầu ra"
date : 2026-03-16 
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---

Chúc mừng, bạn đã tạo thành công một mô hình 3D từ bộ ảnh chụp bằng drone! Trong bước này, chúng ta sẽ xem mô hình đã được tạo bên trong ứng dụng RealityCapture.

---

1. **Mở Project**
    
    Điều hướng đến thư mục *RealityCapture/rcproject*, sau đó nhấp đúp vào tệp có tên **Project** để mở và xem mô hình trong RealityCapture.
    
    ![Model Preview](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-full-screen.png)

---

2. **Thiết lập chế độ xem hai bảng (two panel view)**
    
    Để đảm bảo bạn có chế độ xem hai bảng như hình trên, hãy chọn tùy chọn được tô đỏ trên thanh menu phía trên của ứng dụng RC:
    
    ![Two Panel Option](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-two-panel-option.png)
    
    Sau khi có chế độ xem hai bảng, hãy đảm bảo bảng bên trái đang hiển thị tùy chọn **1Ds**. Nếu không, nhấn và giữ ô nhỏ ở góc trên bên phải của bảng và chọn **1Ds**.  
    Đối với bảng bên phải, hãy đảm bảo **3Ds** được chọn.
    
    ![Two Panel 1Ds 3Ds](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-1ds-3ds.png)

---

3. **Phiên bản High Poly vs. Low Poly**
    
    Khi bạn mở project trong RC, nhiều khả năng RC sẽ hiển thị phiên bản **low poly** của mesh.
    
    Trong bảng **1Ds**, mở rộng menu thả xuống **Component 0**. Bây giờ bạn sẽ thấy hai phiên bản của mesh: **HighPoly** với 30.7M tam giác (triangles) và **LowPoly** với 1.0M tam giác.  
    Nhấp vào tùy chọn **HighPoly** để xem phiên bản này của mesh trong bảng **3Ds**.
    
    ![High Low Poly Screen](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-high-low-poly.png)

---

4. **Xem bộ dữ liệu hình ảnh**
    
    Trong bảng bên trái, thay đổi tùy chọn từ **1Ds** sang **2Ds** để xem bộ dữ liệu hình ảnh cùng với mô hình cuối cùng.
    
    ![2Ds Option](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-high-poly-mesh.png)
    
    Mỗi điểm đang lơ lửng phía trên mesh đại diện cho một vị trí khác nhau nơi drone đã chụp ảnh.  
    Bạn có thể so sánh ảnh drone gốc với mô hình đã được tạo thông qua chế độ xem sau:
    
    ![Model to image compare 1](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-image-compare-1.png)
    
    ![Model to image compare 2](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-image-compare-2.png)