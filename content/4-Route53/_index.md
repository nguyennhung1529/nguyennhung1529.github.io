---
title : "Tên miền với Route 53"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

{{% notice info %}}
Như các bạn có thể thấy ở bước trên chúng ta đã thành công host website tĩnh trên S3, và có thể truy cập vào website đó thông qua S3 website endpoint. Nhưng đường link endpoint đó quá dài và khó nhớ đối với người dùng. Chính vì vậy, trong phần blog này, bạn sẽ tiến hành thiết lập custom domain cho website, để website có thể trở nên thân thiện hơn với người dùng hơn. 
{{% /notice %}}

Trong phần này, bạn sẽ tạo và quản lý custom domain trên **Route 53**, và thiết lập website chúng ta vừa tạo sử dụng tên miền đó.
![Route53](/images/4.route53/000-architecture.png) 

### Tạo DNS record cho website
Chúng ta sẽ sử dụng dịch vụ DNS của Route 53 để trỏ custome domain tới S3 website endpoint.
  - Truy cập Route **53 console**, chọn **Hosted zones** ở trên thanh điều hướng phía bên trái.
  - Click chọn hosted zones mà bạn đã khởi tạo (Tham khảo thực hiện ở bước [1-Yêu cầu chuẩn bị](2-prerequiste/))
  ![Route53](/images/4.route53/001-hosted-zones.png)
  - Tại tab **Records**, click chọn **Create record**.
  ![Route53](/images/4.route53/002-records.png) 
  - Nếu S3 bucket bạn tạo đặt tên là **abc.cloudjourneys.com** (tương ứng sẽ khớp tên với custome domain bạn khai báo), thì bạn sẽ tạo record set với thông tin sau:
    + Record name: **abc**.
    + Record type: **A**.
    + Tick chọn **Alias**.
    + Route traffic to endpoint: chọn **Alias to S3 website endpoint**.
    + Route traffic to region: chọn region bạn khởi tạo web bucket.
    + S3 endpoint: chọn S3 endpoint của web bucket tương ứng.
    ![Route53](/images/4.route53/003-create-record-set.png) 
  - Click **Create record**.
  - Bạn sẽ cần chờ khoảng 30-60s để Route 53 tạo thành công record set.
  ![Route53](/images/4.route53/004-record-ready-to-use.png) 

### Truy cập website
Hiện tại, thay vì truy cập website bằng chuỗi S3 endpoint dài và khó nhớ, bạn đã có thể thay thế bằng tên miền ngắn gọn, đơn giản hơn.
  - Quay trở lại giao diện các Records đã tạo, chọn record bạn vừa tạo (record trỏ vào S3 endpoint).
  ![Route53](/images/4.route53/005-get-record-name.png) 
  - Tại góc bên phải, copy record name, và bạn sẽ truy cập website bằng record name này thay thế cho S3 endpoint.
  ![Route53](/images/4.route53/007-access-website-not-secure.png) 
Như vậy bạn đã thành công truy cập vào website host bởi S3, thông qua custome domain name mà bạn tạo. Tuy nhiên, bạn có thể thấy, ở góc trên cùng bên trái thanh url, trình duyệt hiện thông báo rằng kết nối của bạn tới website này là không bảo mật.

{{% notice info %}}
Chỉ với mỗi Route 53, request của người dùng sẽ thông qua giao thức HTTP được chuyển thẳng trực tiếp tới máy chủ hosting, nơi mà S3 bucket đang được lưu trữ, không thông qua bất kỳ phương thức bảo mật nào => Nguy cơ về mặt an ninh.
Và ngoài ra, tại một số điểm cuối của người dùng ở các Region cách xa so với Region host web, tốc độ tải trang web sẽ rất chậm => Hiệu suất thấp, giảm trải nghiệm người dùng.\
\
Để giải quyết vấn đề trên, phần lab tới sẽ hướng dẫn bạn sử dụng CloudFront kết hợp với SSL/TLS certificate được quản lý bởi AWS Certificate Manager (ACM) 
{{% /notice %}}
