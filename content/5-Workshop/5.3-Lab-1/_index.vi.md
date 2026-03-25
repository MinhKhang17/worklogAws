---
title : "Chạy RealityCapture"
date : 2026-03-16
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

Photogrammetry có thể được tóm tắt thành ba bước cơ bản: **alignment (căn chỉnh), construction (xây dựng), và texture (tạo texture)**.  
Bước đầu tiên là căn chỉnh các hình ảnh trong bộ dữ liệu, sau đó RealityCapture sẽ xây dựng **mesh**, và cuối cùng tạo **texture** và áp dụng chúng lên mesh.

Nhiều tính năng của RealityCapture có thể được sử dụng trực tiếp thông qua **command line** hoặc bằng cách chạy **script**. Các lệnh này được truyền vào ứng dụng dưới dạng tham số của `RealityCapture.exe` và được thực thi theo một chuỗi. Quá trình này hoạt động tương tự như khi bạn gọi các chức năng thông qua GUI. Ứng dụng vẫn sẽ khởi chạy và bạn có thể tương tác với nó như bình thường trong khi quá trình tính toán đang diễn ra.

Chúng ta sẽ sử dụng **Windows PowerShell** để thực thi các lệnh của RealityCapture. Bằng cách **chaining (nối) nhiều lệnh lại với nhau**, chúng ta có thể thực hiện cả ba bước nêu trên chỉ với **một lệnh duy nhất**, mà không cần thao tác với GUI. Chúng ta chỉ sử dụng GUI ở bước cuối cùng để xem mô hình đã hoàn thành.

ℹ️ **Lưu ý**

Việc học cách sử dụng RealityCapture **không cần GUI** là rất quan trọng nếu bạn muốn biến workflow này thành một **pipeline tự động**. Việc xây dựng một **pipeline photogrammetry tự động** sẽ là nội dung của một module trong tương lai của workshop này.

Để xem danh sách đầy đủ các lệnh CLI của RealityCapture, hãy tham khảo tài liệu của Capturing Reality:  
[Capturing Reality documentation](https://rchelp.capturingreality.com/en-US/tutorials/commandline.htm).