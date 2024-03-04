---
title : "Các bước chuẩn bị"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

### 1. Tạo website tĩnh
 Bước đầu tiên, chúng ta cần tạo website tĩnh, trong lab này chúng ta sẽ sử dụng **Hugo** làm trình viết web tĩnh.
 Tham khảo cách viết webs tĩnh bằng Hugo: [Workshop](https://van-hoang-kha.github.io/vi/2-prerequiste/2.1-downloadhugotheme/)

### 2. Quản lý source code trên GitHub
 Bài lab này sẽ dùng GitHub để quản lý source code trong toàn bộ quá trình phát triển website
 ![GitHub](/images/2.prerequisite/001-manage-source-code-with-GitHub.png)
### 3. Đăng ký tên miền
 Trong bài lab này, mình sẽ đăng ký tên miền và sử dụng hosted zone trên Route 53.  
  * Vào Route **53 consoles**, truy cập **Registered domains**.
  * Tại giao diện **Registered domains**, bấm nút **Registered domains**.
    ![RegisterDomainRoute53](/images/2.prerequisite/002-route53-register-domains.png)
    - Điền tên miền muốn check, chọn **Search**.
    - Select tên miền muốn đăng ký, chọn **Proceed to checkout**.
      ![RegisterDomainRoute53](/images/2.prerequisite/003-route53-proceed-to-checkout.png)
  * Tại giao diện **Pricing**:
    - Chọn thời hạn đăng ký tên miền (từ 1 tới 10 năm).
    - Nếu không muốn AWS tự động gia hạn tên miền định kỳ, thì bỏ tick **Auto-renew**.
    - Kiểm tra thông tin, bấm **Next**.
      ![RegisterDomainRoute53](/images/2.prerequisite/004-route53-pricing.png)
  * Tại giao diện **Contact information**, Điền thông tin liên hệ, và bấm **Next**.
  * Tại giao diện **Review and submit**, kiểm tra lại toàn bộ thông tin, bấm **Submit**.
  * Sau khi bấm Submit, check mail được gửi từ AWS để confirm mail.
 Và như vậy là bạn đã thành công đăng ký tên miền trên Route 53.

 {{% notice info %}}
 Khi bạn đăng ký một tên miền mới trên Amazon Route 53, dịch vụ này sẽ tự động tạo một hosted zone công khai (public hosted zone) cho tên miền đó. Hosted zone này chứa các bản ghi DNS cho tên miền và được quản lý trong Route 53. Mỗi khi bạn thêm, xóa hoặc sửa đổi bản ghi trong hosted zone, những thay đổi đó sẽ giúp định hướng traffic cho tên miền của bạn.
 Đối với các tên miền đã được đăng ký ở nhà cung cấp khác (VD: GoDaddy, MatBao, .v.v) và bạn muốn quản lý DNS thông qua Route 53, bạn sẽ cần phải tạo một hosted zone và cập nhật các nameserver của tên miền đó để trỏ về nameserver của Route 53.
 {{% /notice %}}
 
 Tham khảo thêm: [Route53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)