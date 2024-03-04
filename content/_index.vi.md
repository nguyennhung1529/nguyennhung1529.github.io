---
title : "Session Management"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Host website tĩnh trên AWS 

Trong bài lab này, bạn sẽ tìm hiểu về Hugo, S3, CloudFront, AWS Certificate Manager, và Route 53. Tiến hành quản lý một website tĩnh trên AWS một cách an toàn.

Dưới đây là tổng quan kiến trúc mà chúng ta sẽ xây dựng
![ConnectPrivate](/images/architecture-host-static-web-on-s3.png) 

### Nội dung
 1. [Giới thiệu ](1-introduce/)
 2. [Các bước chuẩn bị](2-prerequiste/)
 3. [Host website tĩnh trên S3](3-hoststaticwebsitewiths3/)
 4. [CloudFront và TLS certification](4-route53/)
 5. [DNS với Route 53](5-cloulfrontandacm/)
 6. [Tự động deploy với Github Actions](6-autodeploywithgithubactions/)
 7. [Dọn dẹp tài nguyên](7-cleanup/)

### Tài liệu tham khảo
* https://docs.aws.amazon.com/whitepapers/latest/build-static-websites-aws/using-https-with-amazon-cloudfront.html
* https://000057.awsstudygroup.com/vi/