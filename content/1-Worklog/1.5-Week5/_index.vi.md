---
title: "Worklog Tuần 5"
date: 2025-10-06
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Thực hành AWS Security Hub và đánh giá bảo mật.  
* Quản lý VPC, EC2 và Lambda với Web-hooks và Tagging.  
* Quản lý IAM Users, Policies, Roles và Switch Roles nâng cao.  
* Thực hành kiểm soát quyền hạn người dùng IAM và giới hạn truy cập.  
* Quản lý CloudTrail, Athena và dữ liệu S3 được mã hóa.  
* Triển khai và quản lý EC2, S3 và IAM Role/Key.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Bật AWS Security Hub (Module 05-Lab18-02) <br> - Đánh giá score theo tiêu chí (Module 05-Lab18-03) <br> - Dọn dẹp tài nguyên Security Hub (Module 05-Lab18-04) | 06/10/2025 | 06/10/2025 | <https://000018.awsstudygroup.com/> |
| 3   | - Tạo VPC, Security Group, EC2 (Module 05-Lab22-2.1 đến 2.3) <br> - Cấu hình Incoming Web-hooks Slack (Module 05-Lab22-2.4) <br> - Tạo Tag Instance (Module 05-Lab22-3) <br> - Tạo Role cho Lambda (Module 05-Lab22-4) <br> - Stop/Start function, kiểm tra kết quả (Module 05-Lab22-5.1 đến 6) <br> - Dọn dẹp tài nguyên (Module 05-Lab22-7) | 07/10/2025 | 07/10/2025 | <https://000022.awsstudygroup.com/> |
| 4   | - Quản lý Tag trên EC2 và AWS Resources (Module 05-Lab27-2.1.1 đến 2.2) <br> - Tạo Resource Group (Module 05-Lab27-3) <br> - Dọn dẹp tài nguyên (Module 05-Lab27-4) | 08/10/2025 | 08/10/2025 | <https://000027.awsstudygroup.com/> |
| 5   | - Tạo IAM Users, Policies, Roles (Module 05-Lab28-2.1 đến 4) <br> - Switch Roles & kiểm tra truy cập EC2 ở nhiều Region (Module 05-Lab28-5.1 đến 5.2.5) <br> - Dọn dẹp tài nguyên (Module 05-Lab28-6) | 09/10/2025 | 09/10/2025 | <https://000028.awsstudygroup.com/> |
| 6   | - Tạo IAM Limited User & Restriction Policy, test hạn chế quyền (Module 05-Lab30-3 đến 5) <br> - Dọn dẹp tài nguyên (Module 05-Lab30-6) | 10/10/2025 | 10/10/2025 | <https://000030.awsstudygroup.com/> |
| 7   | - Tạo Policy, Role, Group, User, KMS, Bucket S3, upload dữ liệu, CloudTrail, Athena, test mã hóa dữ liệu (Module 05-Lab33-2.1 đến 6) <br> - Dọn dẹp tài nguyên (Module 05-Lab33-7) | 11/10/2025 | 11/10/2025 | <https://000033.awsstudygroup.com/> |
| CN  | - Quản lý IAM Group, User, Admin Role, Switch Role, hạn chế theo IP & thời gian (Module 05-Lab44) <br> - Tạo EC2, S3, IAM Role, Access Key và dọn dẹp tài nguyên (Module 05-Lab48) | 12/10/2025 | 12/10/2025 | <https://000044.awsstudygroup.com/> <br> <https://000048.awsstudygroup.com/> |

### Kết quả đạt được tuần 5:

* AWS Security Hub:
  * Bật Security Hub, đánh giá score theo tiêu chí, dọn dẹp tài nguyên.  

* VPC, EC2 & Lambda:
  * Tạo VPC, Security Group, EC2, Lambda functions với stop/start, Incoming Web-hooks Slack.  
  * Sử dụng Tags để quản lý resource, tạo Resource Group, kiểm tra kết quả.  

* IAM Management:
  * Tạo Users, Policies, Roles, Switch Roles nâng cao.  
  * Triển khai IAM Limited User với hạn chế quyền và giới hạn truy cập theo IP/Time.  
  * Quản lý nhiều Region với EC2 console, kiểm tra Tag & Policy.  

* CloudTrail, Athena & S3:
  * Tạo Bucket, upload dữ liệu, bật CloudTrail, truy xuất dữ liệu bằng Athena, test mã hóa dữ liệu.  

* Quản lý tài nguyên:
  * Dọn dẹp toàn bộ tài nguyên đã triển khai sau khi thực hành để tránh phát sinh chi phí.  

* Tự đánh giá:
  * Nắm vững thực hành Security Hub, VPC, EC2, Lambda, Tag, IAM, CloudTrail & Athena.  
  * Hiểu và triển khai các hạn chế truy cập nâng cao cho IAM Users.  
  * Sẵn sàng cho tuần tiếp theo với các nội dung tối ưu bảo mật và chi phí.
