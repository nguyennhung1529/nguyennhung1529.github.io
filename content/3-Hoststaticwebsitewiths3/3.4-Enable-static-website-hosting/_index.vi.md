---
title : "Enable static website hosting"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 3.4. </b> "
---

### 1. Enable static website hosting
  - Tại giao diện [S3 console](https://s3.console.aws.amazon.com/s3/home), click chọn bucket của bạn.
  - Vào tab **Properties**:
    + Tại **Static website hosting**, chọn **Edit**
    ![S3](/images/3.hoststaticwebsitewiths3/008-edit-static-web-hosting-setting.png)
    + Tại **Static website hosting**, chọn **Enable**.
    + Tại **Index document**, điền **index.html**.
    + Tại **Error document**, điền **404.html**.
    ![S3](/images/3.hoststaticwebsitewiths3/009-enable-static-website-hosting.png)
    + Click nút **Save change**

### 2. Truy cập thử website thông qua S3 endpoint
  - Tại giao diện [S3 console](https://s3.console.aws.amazon.com/s3/home), click chọn bucket của bạn.
  - Vào tab **Properties**, tại **Static website hosting**, truy cập thông qua bucket website endpoint
  ![S3](/images/3.hoststaticwebsitewiths3/010-access-website-with-s3-website-endpoint.png)
  ![S3](/images/3.hoststaticwebsitewiths3/011-access-website.png)

Như vậy, bạn đã thành công host website tĩnh trên S3.
![S3](/images/3.hoststaticwebsitewiths3/000-architecture.png)