---
title : "Tạo workflow với GitHub Actions"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 6.3 </b> "
---

Để tạo một quy trình tự động cập nhật thay đổi code lên S3 bucket, và tự động invalidateCDN của Cloudfront, trong lab này sẽ hướng dẫn bạn sử dụng GitHub Actions để tự động hóa workflow đó.

#### Tạo Github workflow config file 
  - Tạo Github workflow config YAML file mới tại thư mục **.github/workflows/**, đặt tên `main.yml` (bạn có thể đặt tên bất kỳ).
  - Paste vào file main.yml đoạn code dưới đây:
  ```
  name: Deploy to Amazon S3 bucket

  on:
    push:
      branches:
        - main

  jobs:
    deploy:
      runs-on: ubuntu-latest

      steps:
        - name: Check out the repo
          uses: actions/checkout@v2

        - name: Setup Hugo
          uses: peaceiris/actions-hugo@v2
          with:
            hugo-version: 'latest'
            extended: true

        - name: Configure AWS Credentials
          uses: aws-actions/configure-aws-credentials@v1
          with:
            aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
            aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
            aws-region: ${{ secrets.AWS_REGION }}
            
        - name: Build website
          run: hugo --minify

        - name: Hugo deploy static site to S3 bucket and invalidate Cloudfront cache
          run: hugo deploy --maxDeletes -1 --invalidateCDN
  ```
  ![hugo](/images/6.auto-deploy/016-github-add-secrets.png)
  {{% notice info %}}
  GitHub Actions sẽ chỉ được kích hoạt khi code được push lên remote nhánh main. Với ubuntu docer container, repository của bạn sẽ được kiểm tra với tất cẩ các submodules cho các themes mà bạn sử dụng. Phiên bản mới nhất của Hugo extended sẽ được cài đặt, thông tin xác thực AWS (AWS Credentials) sẽ được thiết lập, trang web của bạn sẽ được build, và deploy lên AWS.
  {{% /notice %}}

{{% notice warning %}}
Đoạn code trên bạn sẽ giữ nguyên, không điền <Access-key-ID> hay <Secret-access-key>. Secret keys như AWS Credentials không nên được đặt trong code, mà thay vào đó, bạn sẽ quản lý các secret key này với tính năng lưu trữ secure secret của GitHub trong repository của bạn.
{{% /notice %}}

#### Khai báo và quản lý các secrets trên GitHub
  - Truy cập [github](https://github.com/), vào repository của bạn.
  - Vào **Settings** > **Secrets and variables** > **Actions**:
  ![hugo](/images/6.auto-deploy/013-github-add-secrets.png)
    + Click chọn **New repository secret**.
    + Name = `AWS_ACCESS_KEY_ID`, Value = `<Access-key-ID>` (lấy thông tin ở file csv access key mà bạn đã tải về máy ở bước trước đó).
    + Chọn **Add Secret**.
    ![hugo](/images/6.auto-deploy/014-github-add-secrets.png)
    + Thực hiện tương tự với secret **AWS_SECRET_ACCESS_KEY** và **AWS_REGION**.
  ![hugo](/images/6.auto-deploy/015-github-add-secrets.png)

Như vậy bạn đã thành công tạo workflow GitHub Actions. Tiếp theo, bạn sẽ thử test hoạt động của workflow này.