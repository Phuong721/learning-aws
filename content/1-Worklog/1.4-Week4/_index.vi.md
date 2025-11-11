---
title: "Worklog Tuần 4"
date: 2025-09-22
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 4:

* Nắm vững kiến thức về **Amazon S3** và quản lý dữ liệu trên cloud.  
* Hiểu về **IAM (Identity and Access Management)** để quản lý người dùng và phân quyền.  
* Làm quen với **AWS Billing & Cost Management** để giám sát chi phí dịch vụ.  

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | ---------------- | -------------- |
| 2 | - Giới thiệu Amazon S3 <br>&emsp; + Khái niệm Bucket & Object <br>&emsp; + Các loại Storage Class (Standard, IA, Glacier...) <br>&emsp; + Cơ chế Versioning và Lifecycle | 22/09/2025 | 22/09/2025 | <https://000005.awsstudygroup.com/> |
| 3 | - **Thực hành 1:** <br>&emsp; + Tạo Bucket S3 <br>&emsp; + Upload / Download file <br>&emsp; + Bật Versioning và kiểm tra | 23/09/2025 | 23/09/2025 | <https://000005.awsstudygroup.com/> |
| 4 | - IAM cơ bản: <br>&emsp; + User, Group, Role, Policy <br>&emsp; + Root user vs IAM user <br>&emsp; + Best Practices trong quản lý tài khoản | 24/09/2025 | 24/09/2025 | <https://000045.awsstudygroup.com/> |
| 5 | - **Thực hành 2:** <br>&emsp; + Tạo IAM user <br>&emsp; + Gán quyền (Policy) <br>&emsp; + Đăng nhập với IAM user để kiểm tra quyền hạn | 25/09/2025 | 25/09/2025 | <https://000045.awsstudygroup.com/> |
| 6 | - Quản lý chi phí AWS: <br>&emsp; + Giới thiệu Billing Dashboard <br>&emsp; + Cost Explorer cơ bản <br>&emsp; + Thiết lập Billing Alarm với CloudWatch | 26/09/2025 | 26/09/2025 | <https://000046.awsstudygroup.com/> |
| 7 | - **Thực hành 3 + Tổng kết:** <br>&emsp; + Kiểm tra hóa đơn (Billing) trong Free Tier <br>&emsp; + Thực hành với Cost Explorer <br>&emsp; + Tổng hợp kiến thức S3 + IAM + Billing | 27/09/2025 | 28/09/2025 | <https://000046.awsstudygroup.com/> |


### Kết quả đạt được tuần 4:

* Hiểu rõ kiến thức cơ bản về **Amazon S3**:  
  * Bucket, Object, và các loại Storage Class.  
  * Cách sử dụng Versioning để quản lý nhiều phiên bản file.  
  * Lifecycle rule để tự động hóa việc lưu trữ / xóa dữ liệu.  

* Thực hành thành công với **S3 Bucket**:  
  * Tạo Bucket, upload / download file.  
  * Bật Versioning và kiểm tra thay đổi phiên bản.  

* Làm quen với **IAM**:  
  * Phân biệt Root user và IAM user.  
  * Tạo IAM user, gán Policy phù hợp.  
  * Đăng nhập và xác minh quyền hạn đã được cấp.  

* Hiểu về **AWS Billing & Cost Management**:  
  * Sử dụng Billing Dashboard để theo dõi chi phí.  
  * Trải nghiệm Cost Explorer để xem biểu đồ chi phí dịch vụ.  
  * Thiết lập Billing Alarm để cảnh báo khi chi phí vượt ngưỡng.  

* Kỹ năng tổng hợp cuối tuần:  
  * Có thể triển khai quy trình từ quản lý dữ liệu (S3) → quản lý người dùng (IAM) → giám sát chi phí (Billing).  
  * Hiểu được mối liên hệ giữa tài nguyên, bảo mật và chi phí khi vận hành trên AWS.  
