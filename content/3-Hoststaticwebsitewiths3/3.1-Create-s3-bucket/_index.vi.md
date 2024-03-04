---
title : "Tạo S3 bucket"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---

Truy cập vào [S3 console](https://s3.console.aws.amazon.com/s3/home).
  * Click chọn **Create bucket**.
  * Tại mục **General configuration**:
    - AWS Region: <Your-Region>. Ở đây mình chọn **ap-southeast-1**
    - Bucket name: <Your-Bucket-Name>
    - Tags: Key: 'project', Value: 'fcj-mission-1'.
    - Click **Create bucket**.
    ![S3](/images/3.hoststaticwebsitewiths3/001-create-bucket.png)

{{% notice info %}}
Cần đặt **bucket name khớp với custom domain** mà bạn đã đăng ký. Do S3 host web tĩnh dựa vào DNS để ánh xạ tên bucket tới web S3 endpoint. Khi bạn sử dụng custom domain như **abc.example.com**, bạn thường tạo record trong cài đặt DNS trỏ đến **abc.example.com.s3-website-region.amazonaws.com**. Để tính năng này hoạt động chính xác, tên bucket phải khớp với custom domain.
Ví dụ: Nếu bạn sử dụng custom domain là **abc.example.com**, thì tên S3 bucket tương ứng sẽ là **abc.example.com**.
{{% /notice %}}