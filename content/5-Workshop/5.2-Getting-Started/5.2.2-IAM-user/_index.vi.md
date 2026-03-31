---
title : "Tạo một IAM User"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

Các dịch vụ AWS như Athena yêu cầu thông tin xác thực hợp lệ khi bạn truy cập, để dịch vụ có thể xác minh rằng bạn có đủ quyền hạn cần thiết. AWS Management Console yêu cầu mật khẩu; ngoài ra, bạn có thể tạo access key để tương tác qua CLI hoặc API. Tuy nhiên, không nên sử dụng thông tin xác thực của root account cho các tác vụ thông thường. Thay vào đó, hãy sử dụng AWS Identity and Access Management (IAM) để tạo một IAM user chuyên dụng, thêm vào nhóm có quyền Administrator, hoặc cấp quyền trực tiếp cho user đó. Sau đó bạn có thể truy cập AWS thông qua URL đăng nhập riêng dành cho IAM user.

Nếu bạn đã đăng ký AWS nhưng chưa tạo IAM user cho mình, bạn có thể thực hiện qua IAM console. Nếu chưa quen với console, hãy tham khảo tài liệu về AWS Management Console để có cái nhìn tổng quan.

**Các bước tạo IAM user và thêm vào nhóm Administrators**

1.  Đăng nhập vào IAM console tại [https://console.aws.amazon.com/iam/](https://console.aws.amazon.com/iam/) bằng email và mật khẩu của root account. Lưu ý: Hạn chế tối đa việc sử dụng root user. Hãy cất giữ thông tin xác thực root ở nơi an toàn và chỉ dùng cho những tác vụ thực sự cần quyền root.

---

1.  Trong thanh điều hướng của console, chọn **Users**, sau đó nhấn **Create user**.
    
2.  Tại ô **User name**, nhập `Administrator`.
    
3.  Tích vào ô **AWS Management Console access**, chọn **Custom password** và nhập mật khẩu. Có thể bật **Require password reset** để buộc người dùng đổi mật khẩu lần đăng nhập đầu tiên.
    
4.  Nhấn **Next: Permissions**.
    
5.  Trên trang **Set permissions**, chọn **Add user to group**.
    
6.  Nhấn **Create group**.
    
7.  Trong hộp thoại **Create group**, tại ô **Group name**, nhập `Administrators`.
    
8.  Tại **Filter policies**, tích chọn **AWS managed - job function**.
    
9.  Trong danh sách policy, chọn **AdministratorAccess**, rồi nhấn **Create group**.
    
10. Trong danh sách nhóm, chọn nhóm vừa tạo. Nhấn **Refresh** nếu cần.
     
11. Nhấn **Next: Tags** để gắn thẻ metadata cho user theo cặp key-value nếu muốn.
     
12. Nhấn **Next: Review** để xem lại cài đặt, sau đó nhấn **Create user**.
     

---

Bạn có thể lặp lại quy trình này để tạo thêm nhóm và người dùng, cấp quyền truy cập tài nguyên AWS phù hợp.

Để đăng nhập bằng IAM user mới, hãy đăng xuất khỏi AWS console và truy cập URL sau — thay your\_aws\_account\_id bằng mã số tài khoản AWS của bạn, không có dấu gạch ngang (ví dụ: nếu tài khoản là 1234-5678-9012, dùng 123456789012):

[https://your\_aws\_account\_id.signin.aws.amazon.com/console/](https://your_aws_account_id.signin.aws.amazon.com/console/) 

Nhập tên IAM user (không phải email) và mật khẩu vừa tạo. Sau khi đăng nhập, thanh điều hướng sẽ hiển thị "your\_user\_name @ your\_aws\_account\_id".

Nếu không muốn URL đăng nhập chứa ID tài khoản, bạn có thể tạo account alias. Từ IAM console, chọn **Dashboard** trong thanh điều hướng. Tại mục **IAM users sign-in link**, nhấn **Customize** và nhập alias (ví dụ: tên công ty). Sau đó dùng URL sau để đăng nhập:

[https://your\_account\_alias.signin.aws.amazon.com/console/](https://your_account_alias.signin.aws.amazon.com/console/) 

Để xác nhận URL đăng nhập cho IAM user, mở IAM console và kiểm tra mục **IAM users sign-in link** trên Dashboard.