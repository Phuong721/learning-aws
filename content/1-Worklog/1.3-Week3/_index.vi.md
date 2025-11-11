---
title: "Worklog Tuần 3"
date: 2025-09-17
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 3:

* Nắm kiến thức cơ bản về **dịch vụ lưu trữ và bảo mật trên AWS**.  
* Làm quen với **AWS S3**, **IAM (Identity and Access Management)** và **CloudWatch** để quản lý, giám sát hệ thống.  

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | ---------------- | -------------- |
| 2 | - Giới thiệu về **Amazon S3** <br>&emsp; + Khái niệm và vai trò của S3 <br>&emsp; + Bucket & Object <br>&emsp; + Lớp lưu trữ (Storage Classes) <br>&emsp; + Cơ chế phân quyền cơ bản | 15/09/2025 | 15/09/2025 | <https://000048.awsstudygroup.com/> |
| 3 | - **Thực hành 1:** <br>&emsp; + Tạo S3 bucket <br>&emsp; + Upload / Download file <br>&emsp; + Thiết lập quyền truy cập (Public / Private) <br>&emsp; + Thử lifecycle policy đơn giản | 16/09/2025 | 16/09/2025 | <https://000048.awsstudygroup.com/> |
| 4 | - Tìm hiểu về **IAM**: <br>&emsp; + User, Group, Role <br>&emsp; + Chính sách (Policies) và quyền truy cập <br>&emsp; + Thực hành gán quyền cho IAM User để quản lý S3 | 17/09/2025 | 17/09/2025 | <https://000049.awsstudygroup.com/> |
| 5 | - **Thực hành 2:** <br>&emsp; + Tạo IAM User và Group <br>&emsp; + Gán quyền S3 ReadOnly / FullAccess <br>&emsp; + Kiểm tra đăng nhập bằng IAM User mới | 18/09/2025 | 18/09/2025 | <https://000049.awsstudygroup.com/> |
| 6 | - Giới thiệu về **CloudWatch**: <br>&emsp; + CloudWatch Metrics <br>&emsp; + CloudWatch Logs <br>&emsp; + CloudWatch Alarms <br>&emsp; + Use case: giám sát EC2 và S3 | 19/09/2025 | 19/09/2025 | <https://000057.awsstudygroup.com/> |
| 7 | - **Thực hành 3 + Tổng kết:** <br>&emsp; + Cấu hình CloudWatch Alarm cho EC2 CPU usage <br>&emsp; + Gửi thông báo qua SNS <br>&emsp; + Tổng kết toàn bộ quy trình (S3 → IAM → CloudWatch) | 20-21/09/2025 | 21/09/2025 | <https://000057.awsstudygroup.com/> |


### Kết quả đạt được tuần 3:

* **Amazon S3**:
  * Hiểu bucket, object và các lớp lưu trữ (Standard, IA, Glacier).
  * Thực hành tạo bucket, upload/download file, cài đặt quyền Public/Private.
  * Biết cách sử dụng lifecycle policy để tự động quản lý file.

* **IAM (Identity and Access Management)**:
  * Phân biệt User, Group, Role.
  * Biết cách viết và gán policy cho IAM User.
  * Tạo User mới, gán quyền S3 ReadOnly/FullAccess, đăng nhập kiểm chứng.

* **CloudWatch**:
  * Hiểu khái niệm Metrics, Logs, Alarms.
  * Thực hành cấu hình alarm cho CPU EC2.
  * Kết hợp với SNS để nhận thông báo qua email.

* **Kỹ năng tổng hợp cuối tuần**:
  * Tích hợp các dịch vụ cơ bản: S3 (lưu trữ) + IAM (quyền truy cập) + CloudWatch (giám sát).
  * Có thể tự triển khai và kết hợp các dịch vụ này trong môi trường thực hành AWS.  
  * Bước đầu nắm được cách bảo mật và giám sát hệ thống AWS cơ bản.  
