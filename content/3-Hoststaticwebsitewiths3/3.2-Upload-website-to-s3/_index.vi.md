---
title : "Upload file lên S3"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---

Hugo hỗ trợ build website tĩnh một cách nhanh chóng. Khi bạn thực hiện lệnh `hugo`, sẽ có một folder **public** - nơi chứa toàn bộ khung website được gen dựa trên các file content **Markdown** mà các bạn đã định nghĩa trước. Và thư mục **public** cũng là thư mục chứa toàn bộ code cần thiết để tạo website mà chúng ta sẽ đẩy lên S3.

 - Tại giao diện [S3 console](https://s3.console.aws.amazon.com/s3/home), click chọn bucket bạn vừa tạo.
 - Để upload files lên S3, bạn có thể thực hiện ngay trên trình duyệt web hoặc thực hiện thông qua AWS CLI hoặc AWS SDK.
 ![S3](/images/3.hoststaticwebsitewiths3/002-upload-files-to-bucket.png)
 - Click chọn **Upload**.
 ![S3](/images/3.hoststaticwebsitewiths3/003-upload-files.png)
 - Chờ cho đến khi các files được tải lên thành công.