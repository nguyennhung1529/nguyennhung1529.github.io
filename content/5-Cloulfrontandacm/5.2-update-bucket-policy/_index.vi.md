---
title : "Cập nhật S3 bucket policy"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 5.2 </b> "
---

Cập nhật **S3 bucket policy** cho phép quyền truy cập chỉ đọc đối với resouce có **User-Agent** header match với khóa bí mật
  - Truy cập [S3 console](https://s3.console.aws.amazon.com/s3/home), click chọn bucket của bạn.
  - Tại tab **Permisssions** > mục **Bucket policy**, chọn **Edit**. cập nhật policy như sau:
    {{% notice info %}}
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "AllowCloudfrontHeader",
          "Effect": "Allow",
          "Principal": "*",
          "Action": "s3:GetObject",
          "Resource": "arn:aws:s3:::<S3-Bucket-Name>/*",
          "Condition": {
            "StringEquals": {
              "aws:UserAgent": "<khóa-bí-mật-tự-định-nghĩa>"
            }
          }
        }
      ]
    }
    {{% /notice %}}
    - Như vậy, bạn đã giới hạn quyền truy cập của S3. Dù hiện chúng ta đang Unblock all public access, nhưng để các truy cập public có thể truy cập được S3 sẽ cần xác thực **User-Agent header** <=> Đã thành công giới hạn quyền truy cập.