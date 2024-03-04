---
title : "Thiết lập Hugo deploy"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 6.2 </b> "
---

Trước khi tạo workflow với GitHub Actions thực hiện update thay đổi trên S3 bucket và invalidateCDN Cloudfront, bạn cần config thêm thông tin. Tại project hugo của bạn, thêm thông tin sau vào file **config.toml**:
```
[deployment]

[[deployment.targets]]
# Name of the target
name = "<Your-Domain>"
# S3 bucket to deploy to
URL = "s3://<Your-Bucket-Name>?region=<Your-Region>"

cloudFrontDistributionID = "<CF-Distribution-ID>"

[[deployment.matchers]]
# Only include files from the 'public' directory, and cache static assets for 20 years
pattern = "public/*"
cacheControl = "max-age=630720000, no-transform, public"
gzip = true

[[deployment.matchers]]
pattern = "^.+\\.(html|xml|json)$"
gzip = true
```
![hugo](/images/6.auto-deploy/008-hugo-deploy-config.png)