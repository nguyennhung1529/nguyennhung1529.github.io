---
title : "Kiểm tra workflow"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 6.4 </b> "
---

Để kiểm tra workflow GitHub Actions có hoạt động đúng như mong đợi, bạn thực hiện các bước sau:
1. Cập nhật code dưới local.
2. Commit và push code lên remote nhánh main.
3. Theo dõi Github Actions workflow.
![web](/images/6.auto-deploy/017-github-actions-workflow-results.png)
5. Reload lại website xem kết quả.
Ta có, nội dung web khi chưa chỉnh sửa:
![web](/images/6.auto-deploy/018-old-content.png)
Ta có, nội dung web sau khi cập nhật:
![web](/images/6.auto-deploy/019-new-content.png)

Chúc mừng bạn đã thành công tạo một workflow tự động cập nhật thay đổi của website trên S3 bucket, và tự động invalidateCDN Cloudfront để refresh nội dung website.
![architect](/images/6.auto-deploy/000-architecture.png)