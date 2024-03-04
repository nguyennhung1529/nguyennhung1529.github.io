---
title : "Tạo IAM User với policies quyền deploy và invalidateCDN"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 6.1 </b> "
---

Trong phần lab này sẽ hướng dẫn bạn tạo IAM user với quyền thao tác với S3 bucket object và invalidateCDN của CloudFront

{{% notice info %}}
Policy tùy chỉnh sẽ chỉ cung cấp quyền để push các thay đổi vào S3 bucket và vô hiệu hóa (invalidate) bộ nhớ đệm trên Cloudfront. Việc cấp quyền đủ dùng sẽ đáp ứng được nguyên tắc đặc quyền tối thiêu (Principle of Least Privilege). Nếu access key của user (user chỉ liên kết với policy này) bị leak, thì việc mà các hacker có thể làm nhiều nhất với access key đó là thực hiện các thay đổi đối với S3 bucket và vô hiệu hóa cache của Cloudfront.
{{% /notice %}}

#### Tạo policy cấp quyền thao tác với S3 bucket object và invalidateCDN của CloudFront
  * Truy cập **IAM console**, chọn **Policies** ở thanh điều hướng bên trái.
  * Chọn **Create policy**
    ![iam](/images/6.auto-deploy/001-IAM-create-policy.png)
  * Tại phần **Specify permissions**:
    - Chọn **JSON**
    - Gán policy sau vào **Policy editor**:
      ```
      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Sid": "GithubActionsWebsite",
            "Effect": "Allow",
            "Action": [
              "s3:ListBucket",
              "s3:GetObject",
              "s3:PutObject",
              "s3:DeleteObject",
              "cloudfront:CreateInvalidation"
            ],
            "Resource": [
              "arn:aws:s3:::nhungnt3299.cloudjourneys.net",
              "arn:aws:s3:::nhungnt3299.cloudjourneys.net/*",
              "<CF-Distribution-ARN>"
            ]
          }
        ]
      }
      ```
    - Click **Next**.
  * Tại **Review and create**:
    - **Policy name**: điền `DeployWebsite`.
    - Chọn **Add new tag**: key - `project`, value - `fcj-mission-1`.
    - Click **Create policy**.
    ![iam](/images/6.auto-deploy/002-IAM-create-policy.png)
    ![iam](/images/6.auto-deploy/003-IAM-create-policy.png)

#### Tạo User attack tới policy vừa tạo
  * Truy cập **IAM console**, chọn **Users** ở thanh điều hướng bên trái.
  * Chọn **Create user**
    ![iam](/images/6.auto-deploy/004-IAM-create-user.png)
  * Tại mục **Specify user details**:
    - User name: điền `GitHub-Actions`.
    - Click **Next**.
      ![iam](/images/6.auto-deploy/005-IAM-create-user.png)
  * Tại mục **Set permissions**:
    - Tại **Permissions options**, chọn **Attach policies directly**.
    - Tại **Permissions policies**, tích chọn policy **DeployWebsite** vừa mới tạo ở bước trên.
    - Click **Next**.
      ![iam](/images/6.auto-deploy/006-IAM-create-user.png)
  * Tại mục **Review and create**:
    - Review lại thông tin.
    - Chọn **Add new tag**: key - `project`, value - `fcj-mission-1`.
    - Click **Create user**.
      ![iam](/images/6.auto-deploy/007-IAM-create-user.png)

#### Tạo User Access key
  * Truy cập **IAM console**, chọn **Users** ở thanh điều hướng bên trái.
  * Chọn user **GitHub-Actions** bạn vừa tạo.
  * Tại tab **Security credentials** > tại mục **Access keys**, click chọn **Create access key**
    ![iam](/images/6.auto-deploy/009-IAM-create-access-key.png)
    ![iam](/images/6.auto-deploy/010-IAM-create-access-key.png)
    - Tại mục **Access key best practices & alternatives**:
      + Chọn **Application running outside AWS**.
      + Chọn **Next**.
      ![iam](/images/6.auto-deploy/011-IAM-create-access-key.png)
    - Tại mục **Set description tag - optional**:
      + Điền mô tả nếu muốn.
      + Click chọn **Create access key**.
    - Tại mục **Retrieve access keys**:
      + Click chọn **Download .csv file**.
      + Lưu file về máy (Ta sẽ dùng access key này để cấp quyền cho GitHub Actions ở phần sau).
      + Click **Done**.
      ![iam](/images/6.auto-deploy/012-IAM-create-access-key.png)
  {{% notice info %}}
  User được tạo sẽ chỉ được sử dụng để cập nhật website và invalidateCDN. Nếu mất access key, bạn phải tạo key mới và vô hiệu hóa access key cũ.
  {{% /notice %}}

Như vậy, bạn đã hoàn thành tạo một User với Access Key cung cấp quyền update website trên <Your-Bucket-Name> và vô hiệu hóa cache tại <CF-Distribution-ARN>.