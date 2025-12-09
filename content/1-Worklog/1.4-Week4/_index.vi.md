---
title: "Worklog Tuần 4"
date: 2025-09-29
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Thực hành AWS Backup nâng cao và thiết lập thông báo.  
* Triển khai và quản lý máy ảo từ On-Premises lên AWS bằng AMI.  
* Thực hành S3, Storage Gateway và File Shares nâng cao.  
* Triển khai Multi-AZ file system với SSD và HDD, giám sát hiệu suất và quản lý người dùng.  
* Quản lý website tĩnh S3, CloudFront, versioning, replication và dọn dẹp tài nguyên.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Tạo S3 Bucket (Module 04-Lab13-02.1) <br> - Triển khai hạ tầng Backup (Module 04-Lab13-02.2) <br> - Tạo Backup Plan (Module 04-Lab13-03) <br> - Thiết lập thông báo (Module 04-Lab13-04) | 29/09/2025 | 29/09/2025 | <https://000013.awsstudygroup.com/>, <https://000014.awsstudygroup.com/> |
| 3   | - Thử nghiệm khôi phục dữ liệu (Module 04-Lab13-05) <br> - Dọn dẹp tài nguyên Backup (Module 04-Lab13-06) | 30/09/2025 | 30/09/2025 | <https://000013.awsstudygroup.com/>, <https://000014.awsstudygroup.com/> |
| 4   | - Làm việc với VMWare Workstation (Module 04-Lab14-01) <br> - Export VM từ On-Premises (Module 04-Lab14-02.1) <br> - Upload VM lên AWS (Module 04-Lab14-02.2) <br> - Import VM vào AWS (Module 04-Lab14-02.3) <br> - Triển khai Instance từ AMI (Module 04-Lab14-02.4) | 01/10/2025 | 01/10/2025 | <https://000024.awsstudygroup.com/>, <https://000025.awsstudygroup.com/> |
| 5   | - Quản lý S3 Bucket ACL (Module 04-Lab14-03.1) <br> - Export VM từ Instance (Module 04-Lab14-03.2) <br> - Dọn dẹp tài nguyên VM & AWS (Module 04-Lab14-05) | 02/10/2025 | 02/10/2025 | <https://000024.awsstudygroup.com/>, <https://000025.awsstudygroup.com/> |
| 6   | - Tạo Storage Gateway (Module 04-Lab24-2.1) <br> - Tạo File Shares (Module 04-Lab24-2.2) <br> - Mount File Shares trên máy On-Premises (Module 04-Lab24-2.3) <br> - Dọn dẹp tài nguyên (Module 04-Lab24-3) | 03/10/2025 | 03/10/2025 | <https://000024.awsstudygroup.com/> |
| 7   | - Tạo SSD & HDD Multi-AZ File System (Module 04-Lab25-2.2 & 2.3) <br> - Tạo file shares, test & monitor performance (Module 04-Lab25-3, 4, 5) <br> - Enable deduplication, shadow copies, quản lý user & quotas, scale throughput & storage (Module 04-Lab25-6 đến 12) | 04/10/2025 | 04/10/2025 | <https://000024.awsstudygroup.com/> |
| CN  | - Dọn dẹp môi trường Multi-AZ (Module 04-Lab25-13) <br> - Tạo S3 Bucket, load dữ liệu, website tĩnh, CloudFront, versioning & replication, test & cleanup (Module 04-Lab57-2.1 đến 11) | 05/10/2025 | 05/10/2025 | <https://000057.awsstudygroup.com/> |

### Kết quả đạt được tuần 4:

* AWS Backup nâng cao:
  * Triển khai Backup Plan, thiết lập thông báo, test restore dữ liệu thành công.  
  * Dọn dẹp tài nguyên backup.

* Máy ảo & AMI:
  * Export VM từ On-Premises, upload & import vào AWS.  
  * Triển khai Instance từ AMI và quản lý S3 Bucket ACL.  
  * Dọn dẹp VM & tài nguyên sau thử nghiệm.

* Storage Gateway & Multi-AZ File System:
  * Tạo Storage Gateway, File Shares, mount trên máy On-Premises.  
  * Triển khai SSD & HDD Multi-AZ File System, tạo file shares, test & monitor performance.  
  * Quản lý user, enable deduplication, shadow copies, quotas, scale throughput & storage.

* S3 & CloudFront:
  * Tạo S3 Bucket, load dữ liệu, triển khai website tĩnh, cấu hình CloudFront.  
  * Sử dụng versioning, replication multi-region, test & dọn dẹp tài nguyên.

* Tự đánh giá:
  * Nắm vững triển khai Backup nâng cao, Storage Gateway, Multi-AZ File System, quản lý VM & website tĩnh.  
  * Thực hành dọn dẹp tài nguyên đúng cách, tránh phát sinh chi phí.  
  * Sẵn sàng cho tuần tiếp theo với các bài học về bảo mật, IAM & tối ưu chi phí.
