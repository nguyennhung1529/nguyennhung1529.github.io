---
title : "Tăng tốc và bảo mật kết nối với CloudFront và SSL"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

Bài lab này sẽ hướng dẫn bạn các bước để lưu trữ nội dung web tĩnh trong Amazon S3 bucket, được bảo vệ và tăng tốc bởi Amazon CloudFront. Ngoài ra, để tăng cường độ bảo mật trên đường truyền, bài lab sẽ hướng dẫn bạn kết hợp CloudFront với chứng chỉ SSL được quản lý bởi AWS Certificate Manager (ACM) giúp mã hóa kết nối HTTPS trong quá trình truyền dữ liệu. 

![Route53](/images/5.cloudfront-and-acm/000-architecture.png)

### Chi phí
  - Thường ít hơn $ 1 mỗi tháng (tùy thuộc vào số lượng request)
  - [Giá Amazon S3](https://aws.amazon.com/s3/pricing/)
  - [Giá Amazon CloudFront](https://aws.amazon.com/cloudfront/pricing/)

### Tài liệu tham khảo
  - [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
  - [Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)

### Các bước thực hiện
5.1. [Cấu hình CloudFront Distribution](5.1-config-cloudfront-distribution/) \
5.2. [Cập nhật S3 bucket policy](5.2-update-s3-policy/) \
5.3. [Kiểm tra Cloudfront](5.3-check-cloudfront/) \
5.4. [Cập nhật Route 53 record set](5.4-update-route53-record-set/) \
5.5. [Kiểm tra kết nối tới website](5.5-check-connection/)