---
title : "Kiểm tra kết nối"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

  - Mở trình duyệt ẩn danh, truy cập vào tên miền thử với 2 giao thức http và https
    ![Route53](/images/5.cloudfront-and-acm/028-Route53-check-result.png)
  - Có thể thấy dù truy cập bằng protocal **http**, CloudFront cũng đã tự động điều hướng sang protocal **https**.

Như vậy, bạn đã thành công host website tĩnh được tạo bởi **Hugo** trên **Amazon S3 bucket**, sử dụng **Route 53** để khai báo và quản lý tên miền của website, đồng thời kết hợp với **CloudFront** và **AWS Certificate Manager (ACM)** để tăng cường độ bảo mật, cũng như giảm độ trễ khi truy cập website.
![architecture](/images/architecture-on-process.png) 

Trong các bài lab sau sẽ hướng dẫn bạn cách tự động deploy code khi có sự thay đổi bằng cách tận dụng tính năng **GitHub Actions**.
