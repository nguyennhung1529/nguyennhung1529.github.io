---
title : "Tự động deploy với GitHub Actions"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

### Giới thiệu

{{% notice note %}}
Như vậy, bạn đã thành công host một website tĩnh trên S3, sử dụng tên miền tùy chỉnh quản lý bởi Route 53 để tăng độ thân thiện cho phía end-user (người dùng cuối), sử dụng CloudFront để tăng tốc độ và an toàn khi truy cập web phía user, và tích hợp với AWS Certificate Manager (ACM) để cung cấp chứng chỉ SSL/TLS tăng cường bảo mật trên đường truyền.
{{% /notice %}}

Trong quá trình phát triển website, mỗi lần update source code dưới local, để deploy lên S3, cung cấp cho người dùng thông tin mới nhất, các bạn cần thực hiện các bước sau:
- Bước 1: Sau khi chỉnh sửa dưới local, các bạn **manual** copy cập nhật lên S3 bucket.
- Bước 2: Thực hiện **invalidateCDN** CloudFront (CloudFront sẽ xóa bỏ nội dung cũ đang được cache tại các Edge Location, và thực hiện renew cache nội dung mới nhất của website, để phân phối phía người dùng).

Vậy có cách nào có thể tự động deploy code mới nhất được update dưới local lên S3 bucket, và tự động renew nội dung cache tại CloudFront?
Để thực hiện được điều đó, bài lab này sẽ hướng dẫn bạn tận dụng tính năng **GitHub Actions** của GitHub để xây dựng workflow tự động deploy và review nội dung mới nhất tới người dùng.

![architect](/images/6.auto-deploy/000-architecture.png)

### Nội dung
6.1. [Tạo IAM User với policies quyền deploy và invalidateCDN](6.1-create-iam-user-and-policy/) \
6.2. [Thiết lập Hugo deploy](6.2-config-hugo-deploy/) \
6.3. [Tạo workflow với GitHub Actions](6.3-create-workflow-with-github-action/) \
6.4. [Kiểm tra workflow](6.4-test-results/)