---
title : "Cấu hình CloudFront Distribution"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

Trong bước này, bạn sẽ **CloudFront distribution** và cấu hình dịch vụ này phục vụ s3 Bucket mà chúng ta đã tạo trước đó.
##### 1. Truy cập [Amazon CloudFront console](https://us-east-1.console.aws.amazon.com/cloudfront/v4/home).
##### 2. Click vào **Create distribution**.
  ![CF](/images/5.cloudfront-and-acm/006-CF-create-distribution.png)
##### 3. Chỉ định các cài đặt sau cho distribution:
  {{% notice info %}}
  Cách ưu tiên để cho phép truy cập vào **S3 Bucket** là thông qua **Origin Access Identity**. Nhưng nếu S3 bucket được config như là một **website endpoint**, thì chúng ta phải dùng **Custom Headers** để giới hạn quyền truy cập vào S3 Bucket. \
  \
  Trong lab này, chúng ta sẽ khai báo **User-Agent** header trong **Cloudfront** với một khóa bí mật (secret key), giúp block truy cập tới bucket từ mọi người khác, và sẽ chỉ cho phép CloudFront (có header mang thông tin khóa) sẽ được truy cập S3 bucket.
  {{% /notice %}}
  - Tại **Origin domain**, chọn **S3 bucket** mà bạn đã tạo, sau đó chọn **Use website endpoint**.
    ![CF](/images/5.cloudfront-and-acm/007-CF-use-website-endpoint.png)
    
  {{% notice info %}}
  Trong Cloudfront distribution, chúng ta không thể sử dụng trực tiếp S3 bucket endpoint cho static website. Tên Origin Domain nên được trỏ tới S3-website endpoint tại đúng region.
  {{% /notice %}}

  - Tại **Add custom header - optional**, click **Add header**:
    + Header Name = **User-Agent**.
    + Value = **<khóa-bí-mật-tự-định-nghĩa>**.
    ![CF](/images/5.cloudfront-and-acm/008-CF-add-header.png)
  
  - Tại phần **Default cache behavior** > **Viewer protocol policy**, tích chọn **Redirect HTTP to HTTPS**.
    ![CF](/images/5.cloudfront-and-acm/010-CF-distribution-protocol-policy.png)
  
  - Tại phần **Web Application Firewall (WAF)**, chọn **Enable security protections**.
    ![CF](/images/5.cloudfront-and-acm/011-CF-distribution-enable-waf.png)

  - Trong phần **Settings**, chọn **Use only North America and Europe** (Rẻ nhất).
  
  - Tại **Alternate domain name (CNAME)**, điền domain name của website.
    ![CF](/images/5.cloudfront-and-acm/012-CF-distribution-settings.png)
  
  - Tại **Custom SSL certificate**, trỏ vào **Request certificate**, một cửa sổ mới **request certificate** của ACM hiện lên. Chúng ta sẽ tạm dừng để setting cho SSL certificate trước:
    + Tại cửa sổ **Request certificate**, chọn **Next** => config certificate.
      ![CF](/images/5.cloudfront-and-acm/013-ACM-request-certificate.png)
    + Domain names: Điền domain name của website.
    + Có thể add tag để về sau dễ quản lý.
      ![CF](/images/5.cloudfront-and-acm/014-ACM-config-certificate.png)
    + Click **Request**.
    + Tại mục **List certificate**, chọn certificate vừa mới request
      ![CF](/images/5.cloudfront-and-acm/015-ACM-view-certificate.png)
      Chọn **Create records in Route 53**
      Tại trang **Create DNS records in Amazon Route 53**, chọn **Create Record**
      ![CF](/images/5.cloudfront-and-acm/016-ACM-create-records.png)
    + Mở **Route 53** > **Hosted zone** > chọn Hosted zone của bạn, bạn sẽ thấy một record CNAME của certificate mới vừa được add vào. 
      ![CF](/images/5.cloudfront-and-acm/017-Route53-new-certificate-records.png)
    + Tại **ACM console** > **List certificate**, bạn sẽ thấy trạng thái của certificate bạn vừa mới register. Khi nào trạng thái là **issued**, thì certificate này đã có thể được sử dụng.
      ![CF](/images/5.cloudfront-and-acm/018-ACM-is-ready-to-use.png)
  - Sau khi đã tạo certificate mới thành công, tiếp tục với mục Setting của Cloudfront Distribution, tại **Custom SSL certificate**, bấm biểu tượng **reload** > chọn ACM certificate vừa tạo.
    ![CF](/images/5.cloudfront-and-acm/019-CF-add-ACM-certificate.png)
  - Kiểm tra lại thông tin config và click **Create distribution**.
  - Đợi vài phút để CloudFront Distribution được deploy thành công. Trong lúc chờ, bạn có thể thực hiện bước [5.2. Cập nhật S3 bucket policy](../5.2-update-bucket-policy/).