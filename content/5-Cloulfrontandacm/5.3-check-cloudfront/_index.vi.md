---
title : "Kiểm tra CloudFront"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 5.3 </b> "
---

  - Trong giao diện CloudFront, chọn **ID**.
    ![CF](/images/5.cloudfront-and-acm/022-CF-access-cloudfront.png)
  - Tại mục Distribution domain name:
    + Đảm bảo rằng CloudFront đã deploy xong bằng cách xem nội dung ở mục **Last modified**.
    + Tại **Distribution domain name**, Copy URL.
      ![CF](/images/5.cloudfront-and-acm/023-CF-get-CF-url.png)
    + Bật một tab khác và dán giá trị CloudFront URL vào thanh tìm kiếm rồi nhấn enter.
      ![CF](/images/5.cloudfront-and-acm/024-CF-success-access-s3.png)
      
Chúc mừng bạn đã triển khai thành công CloudFront để phân phối một website tĩnh được host trên S3 có xác thực thông qua User-Agent header với khóa bí mật tự quản lý, giúp giới hạn truy cập vào S3 từ các nơi khác.