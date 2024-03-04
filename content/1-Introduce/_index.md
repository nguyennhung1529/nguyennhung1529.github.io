---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

Tổng quan kiến trúc mà chúng ta sẽ xây dựng
![architecture](/images/architecture-host-static-web-on-s3.png) 

Trong đó:
* **Hugo** là một công cụ tạo trang web tĩnh (static site generator) rất nhanh và hiệu quả. Đây là một ứng dụng được viết bằng ngôn ngữ lập trình Go, thiết kế để giúp bạn tạo ra các trang web hoặc blog chỉ từ các file văn bản đơn giản (Ví dụ như các file nội dung tĩnh **Markdown**) mà không cần một cơ sở dữ liệu phức tạp.
* **Amazon S3 (Simple Storage Service)**: là một dịch vụ lưu trữ đối tượng (object) của AWS, cung cấp độ bảo mật, khả năng chịu lỗi, khả năng scale và availability cao, và giá thành lưu trữ rẻ. S3 thường được sử dụng để lưu trữ và phục vụ các file lớn như hình ảnh, video, hoặc file tải về. Và trong trường hợp này nó được sử dụng để lưu trữ các tệp tin của trang web tĩnh.
* **AWS CloudFront**: là một dịch vụ mạng phân phối nội dung (CDN) của AWS giúp phân phối nội dung của trang web tới người dùng với độ trễ thấp và tốc độ cao. CloudFront tích hợp với S3 và cung cấp khả năng phân phối nội dung an toàn qua HTTPS.
* **AWS Certificate Manager (ACM)**: dùng để cấp phát, quản lý và triển khai **chứng chỉ SSL/TLS** dùng để mã hóa dữ liệu truyền qua internet (**encrypt in transit**). Trong mô hình trên, ACM cung cấp chứng chỉ để mã hóa kết nối giữa người dùng (end user) và CloudFront, đảm bảo tính bảo mật.
* **Amazon Route 53**: là một dịch vụ DNS web có khả năng định tuyến yêu cầu người dùng tới cơ sở hạ tầng AWS phù hợp, như CloudFront. Nó cũng có thể được sử dụng để quản lý tên miền và các DNS record.
* **GitHub**: là nơi để lưu trữ và quản lý source code của website, cung cấp tính năng **GitHub Actions**, cho phép bạn tự động hóa workflow phát triển phần mềm, bao gồm việc triển khai trang web lên S3.

Quy trình tổng thể bắt đầu từ Admin/Editer/Dev thực hiện các thay đổi trên source code và push chúng lên GitHub. GitHub Actions sau đó sẽ thực hiện build website tĩnh và đồng bộ code lên S3. Khi người dùng (end-user) truy cập website thông qua tên miền web, Route 53 sẽ phân giải tên miền đó và hướng requests tới distribution CloudFront. CloudFront sẽ tích hợp với AWS Certificate Manager (ACM) để thêm SSL/TLS certification giúp mã hóa nội dung giao tiếp qua HTTPS <=> thiết lập một kênh truyền dữ liệu an toàn, đảm bảo tính bảo mật của dữ liệu được truyền giữa người dùng (end-user) và CDN.

Mô hình triển khai trên đảm bảo nội dung website được phân phối nhanh chóng (CloudFront), an toàn (HTTPS & SSL/TLS) và được tự động cập nhật nội dung (GitHub Actions).