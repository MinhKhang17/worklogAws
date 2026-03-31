---
title : "Lab 3: Làm việc với bảng Iceberg trên EMR"
date : 2026-03-16 
weight : 5 
chapter : false
pre : " <b> 5.5. </b> "
---


Với self-paced labs, chúng ta sẽ tạo một EMR cluster sử dụng Release 7.5 với Iceberg được cài đặt sẵn. Với AWS Events, EMR cluster đã được tạo sẵn cho bạn. Bài lab này đã được kiểm chứng với `EMR 7.5.0`, vì vậy chúng tôi khuyến nghị sử dụng cùng phiên bản để đảm bảo tính tương thích.

Chúng ta sẽ sử dụng PySpark Jupyter Notebook trong EMR Studio để làm việc tương tác với các bảng Iceberg.

Nếu bạn đang theo lộ trình self-paced, hãy đảm bảo đã hoàn thành bài lab **Tạo S3 bucket** trước khi bắt đầu. Với AWS Events, S3 bucket đã được tạo sẵn.