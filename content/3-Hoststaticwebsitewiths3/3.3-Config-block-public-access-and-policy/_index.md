---
title : "Cấu hình block public access và bucket policy"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3.3. </b> "
---

### 1. Cấu hình block public access
  - Tại giao diện [S3 console](https://s3.console.aws.amazon.com/s3/home), click chọn bucket của bạn.
  - Vào tab **Permisssions**:
    + Tại **Block public access (bucket settings)**, chọn **Edit**
    ![S3](/images/3.hoststaticwebsitewiths3/004-edit-block-public-access-setting.png)
    + Bỏ tích chọn **Block all pulbic access**, click nút **Save change**, và confirm thay đổi
    ![S3](/images/3.hoststaticwebsitewiths3/005-uncheck-block-public-access-setting.png)

### 2. Cấu hình S3 bucket policy
  - Tiếp tục tại tab **Permisssions**:
    + Tại **Bucket policy**, chọn **Edit**
    + Khai báo policy như sau:
    {{% notice info %}}
    {
      "Version": "2012-10-17",
      "Statement": [{
        "Sid": "AllowPublicRead",
        "Effect": "Allow",
        "Principal": "*",
        "Action": [
        "s3:GetObject"
      ],
        "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
      }]
    }
    {{% /notice %}}
    ![S3](/images/3.hoststaticwebsitewiths3/006-s3-bucket-policy-setting.png)
    + Click **Save change**
    ![S3](/images/3.hoststaticwebsitewiths3/007-save-s3-bucket-policy-setting.png)