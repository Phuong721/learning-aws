---
title: "Worklog Tuần 6"
date: 2025-10-13
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Thực hành triển khai VPC, EC2, RDS và các cấu hình bảo mật.  
* Triển khai ứng dụng và thực hiện backup/restore.  
* Quản lý kết nối EC2 qua RDP và Fleet Manager.  
* Thực hiện cấu hình SQL Server và Oracle database.  
* Thực hiện chuyển đổi schema từ MSSQL/Oracle sang Aurora MySQL.  
* Thực hành Serverless Migration, kiểm tra logs và troubleshoot các kịch bản test.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Tạo VPC (Module 06-Lab05-2.1) <br> - Tạo EC2 Security Group (Module 06-Lab05-2.2) <br> - Tạo RDS Security Group (Module 06-Lab05-2.3) <br> - Tạo DB Subnet Group (Module 06-Lab05-2.4) <br> - Triển khai EC2 instance (Module 06-Lab05-3) <br> - Triển khai RDS database instance (Module 06-Lab05-4) <br> - Deploy ứng dụng (Module 06-Lab05-5) <br> - Backup & Restore (Module 06-Lab05-6) <br> - Dọn dẹp tài nguyên (Module 06-Lab05-7) | 13/10/2025 | 13/10/2025 | <https://000006.awsstudygroup.com/> |
| 3   | - Kết nối EC2 bằng RDP Client (Module 06-Lab43-01) <br> - Kết nối EC2 bằng Fleet Manager (Module 06-Lab43-02) <br> - Cấu hình SQL Server Source DB (Module 06-Lab43-03) | 14/10/2025 | 14/10/2025 | <https://000043.awsstudygroup.com/> |
| 4   | - Kết nối và cấu hình Oracle Source DB (Module 06-Lab43-04 & 05) <br> - Drop Constraint (Module 06-Lab43-06) <br> - MSSQL → Aurora MySQL target config (Module 06-Lab43-07) <br> - Tạo project migration (Module 06-Lab43-08) | 15/10/2025 | 15/10/2025 | <https://000043.awsstudygroup.com/> |
| 5   | - Chuyển đổi schema MSSQL/Oracle sang Aurora MySQL (Module 06-Lab43-09 & 10) <br> - Tạo Migration Task và Endpoints (Module 06-Lab43-11) <br> - Kiểm tra dữ liệu trên S3 (Module 06-Lab43-12) | 16/10/2025 | 16/10/2025 | <https://000043.awsstudygroup.com/> |
| 6   | - Tạo Serverless Migration (Module 06-Lab43-13) <br> - Tạo Event Notification (Module 06-Lab43-14) <br> - Kiểm tra logs (Module 06-Lab43-15) <br> - Troubleshoot Mem Pressure & Table Errors (Module 06-Lab43-16 & 17) | 17/10/2025 | 17/10/2025 | <https://000043.awsstudygroup.com/> |
| 7   | - Tổng hợp kết quả, kiểm tra và dọn dẹp toàn bộ tài nguyên thực hành | 18/10/2025 | 18/10/2025 | N/A |
| CN  | - Tự đánh giá tuần, chuẩn bị kiến thức cho tuần tiếp theo | 19/10/2025 | 19/10/2025 | N/A |

### Kết quả đạt được tuần 6:

* Triển khai mạng & cơ sở dữ liệu:
  * Tạo và cấu hình VPC, EC2 Security Group, RDS Security Group, DB Subnet Group.  
  * Triển khai EC2 & RDS instance thành công, deploy ứng dụng và thực hiện backup/restore.  

* Quản lý kết nối EC2:
  * Kết nối EC2 bằng RDP Client và Fleet Manager, quản lý Source DB SQL Server & Oracle.  

* Chuyển đổi dữ liệu & Migration:
  * Thực hiện schema conversion từ MSSQL/Oracle sang Aurora MySQL.  
  * Tạo Migration Task, Endpoints, kiểm tra dữ liệu trên S3.  

* Serverless Migration & Troubleshooting:
  * Tạo Serverless Migration, cấu hình Event Notification, kiểm tra logs.  
  * Xử lý các kịch bản test Mem Pressure và Table Errors thành công.  

* Quản lý tài nguyên:
  * Dọn dẹp toàn bộ tài nguyên đã triển khai để tránh phát sinh chi phí ngoài ý muốn.  

* Tự đánh giá:
  * Nắm vững triển khai VPC, EC2, RDS, backup/restore, kết nối database và Serverless Migration.  
  * Hiểu quy trình chuyển đổi dữ liệu và kiểm soát logs.  
  * Chuẩn bị tốt cho tuần tiếp theo với các nội dung nâng cao về bảo mật và tối ưu hạ tầng.
