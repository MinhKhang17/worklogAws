---
title : "1.1 Xem và tải xuống tập dữ liệu mẫu"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

Chúng ta sẽ làm việc với phiên bản mô phỏng của bộ dữ liệu Amazon Product Reviews trong cả hai phần lab Athena và EMR. Hãy dành vài phút để tìm hiểu cấu trúc và nội dung của bộ dữ liệu này.

**Bộ dữ liệu Đánh giá Khách hàng Amazon**

Amazon Customer Reviews (hay còn gọi là Product Reviews) là một trong những tính năng biểu tượng của Amazon. Trong hơn hai thập kỷ kể từ bài đánh giá đầu tiên vào năm 1995, hàng triệu khách hàng Amazon đã đóng góp hơn một trăm triệu bài đánh giá, chia sẻ ý kiến và trải nghiệm sử dụng sản phẩm trên Amazon.com. Bộ dữ liệu phong phú này đã trở thành nguồn tài nguyên quý giá cho nghiên cứu trong các lĩnh vực như Xử lý Ngôn ngữ Tự nhiên (NLP), Truy xuất Thông tin (IR) và Học Máy (ML). Bộ dữ liệu được thiết kế để phản ánh đa dạng đánh giá của khách hàng, sự khác biệt nhận thức về sản phẩm theo khu vực địa lý, cũng như xu hướng quảng cáo hoặc thiên kiến của người đánh giá.

LƯU Ý: Bộ dữ liệu dùng trong workshop này là dạng mô phỏng, chứa các con số, tên và văn bản được tạo ngẫu nhiên.

**Tải xuống bộ dữ liệu mẫu và tải lên S3**

1.  Tải xuống bộ dữ liệu từ một trong các đường dẫn bên dưới
    
    -   [Dữ liệu mẫu - us-east-1](https://ws-assets-prod-iad-r-iad-ed304a55c2ca1aee.s3.us-east-1.amazonaws.com/e57af944-04b9-41f5-8285-90295ed32bdc/simulatedproductreviews.parquet)
        
    -   [Dữ liệu mẫu - us-west-2](https://ws-assets-prod-iad-r-pdx-f3b3f9f1a7d6a3d0.s3.us-west-2.amazonaws.com/e57af944-04b9-41f5-8285-90295ed32bdc/simulatedproductreviews.parquet)
        
2.  Mở [AWS S3 console](https://s3.console.aws.amazon.com/s3/buckets) của bạn
    
3.  Nhấn vào tên S3 bucket đã được tạo cho bạn
    
4.  Nhấn **Create folder**
    
![create folder](/images/5-Workshops/5.3/5.3.1/3.png)

5.  Nhập **productreviews** làm tên thư mục, rồi nhấn nút **Create folder**
    
6.  Điều hướng vào thư mục vừa tạo bằng cách nhấn vào **productreviews**, sau đó nhấn nút **Upload**
    
7.  Nhấn **Add files**, chọn tệp dữ liệu đã tải về ở bước 1, rồi nhấn **Upload**

![upload file](/images/5-Workshops/5.3/5.3.1/4.png)