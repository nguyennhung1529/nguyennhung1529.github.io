---
title : "Cập nhật DNS record"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---

Trong bài lab này sẽ cập nhật Route 53 DNS record để trỏ tên miền của website của bạn tới **Cloudfront Distribution**.
  - Truy cập Route **53 console**, chọn **Hosted zones** ở trên thanh điều hướng phía bên trái.
  - Click chọn hosted zones của bạn. Tại tab **Records**, click chọn DNS record của website.
  - Tại **Record details**, chọn **Edit record**:
  ![Route53](/images/5.cloudfront-and-acm/025-Route53-update-record-to-CF.png)
    + Route traffic to endpoint: chọn **Alias to CloudFront distribution**.
    + Choose Distribution: chọn Cloudfront distribution.
    + Chọn **Save**.
    ![Route53](/images/5.cloudfront-and-acm/026-Route53-save-update-record-to-CF.png)
  - Chờ 30-60s để trạng thái chuyển qua **INSYNC**. Khi đó, bạn có thể thử truy cập vào website bằng domain name.