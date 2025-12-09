---
title: "Worklog Tuần 3"
date: 2025-09-22
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Thực hành triển khai AWS Backup và đảm bảo phục hồi dữ liệu.  
* Triển khai S3, Storage Gateway, quản lý dữ liệu và file shares.  
* Thiết lập và quản lý website tĩnh trên S3 cùng với CloudFront.  
* Tìm hiểu các tính năng nâng cao của S3: versioning, replication, quản lý quyền truy cập.  
* Dọn dẹp tài nguyên sau khi thử nghiệm để tránh phát sinh chi phí.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Deploy AWS Backup to the system - Introduction (Module 03-Lab13-01) <br> - Triển khai hạ tầng Backup (Module 03-Lab13-02.2) <br> - Tạo Backup Plan (Module 03-Lab13-03) | 22/09/2025 | 22/09/2025 | <https://000013.awsstudygroup.com/> |
| 3   | - Thử nghiệm khôi phục dữ liệu (Module 03-Lab13-05) <br> - Dọn dẹp tài nguyên Backup (Module 03-Lab13-06) | 23/09/2025 | 23/09/2025 | <https://000013.awsstudygroup.com/> |
| 4   | - Tạo S3 Bucket & EC2 cho Storage Gateway (Module 03-Lab24-01.1 & 01.2) <br> - Tạo Storage Gateway và File Shares (Module 03-Lab24-02.1 & 02.2) | 24/09/2025 | 24/09/2025 | <https://000024.awsstudygroup.com/> |
| 5   | - Tạo S3 Bucket, load dữ liệu, enable static website (Module 03-Lab57-02.1, 02.2 & 03) <br> - Cấu hình quyền truy cập công khai và test website (Module 03-Lab57-04, 05, 06) | 25/09/2025 | 25/09/2025 | <https://000057.awsstudygroup.com/> |
| 6   | - Block all public access, cấu hình CloudFront & test (Module 03-Lab57-07.1 đến 07.3) <br> - Sử dụng bucket versioning, di chuyển đối tượng, replication multi-region (Module 03-Lab57-08, 09, 10) | 26/09/2025 | 26/09/2025 | <https://000057.awsstudygroup.com/> |
| 7   | - Dọn dẹp tài nguyên S3 & CloudFront (Module 03-Lab57-11) | 27/09/2025 | 27/09/2025 | <https://000057.awsstudygroup.com/> |
| CN  | - Tổng kết tuần 3, đánh giá kết quả, ghi nhận kinh nghiệm triển khai Backup, Storage Gateway và S3/CloudFront | 28/09/2025 | 28/09/2025 | N/A |

### Kết quả đạt được tuần 3:

* AWS Backup:
  * Triển khai Backup Plan và thử nghiệm khôi phục dữ liệu thành công.  
  * Dọn dẹp tài nguyên backup sau khi kiểm tra.

* Storage Gateway & S3:
  * Tạo S3 Bucket và EC2 cho Storage Gateway.  
  * Thiết lập Storage Gateway và file shares, load dữ liệu thành công.

* Website tĩnh & CloudFront:
  * Triển khai website tĩnh trên S3, cấu hình public access, và kiểm tra hiển thị.  
  * Cấu hình CloudFront để phân phối nội dung, kiểm tra hoạt động.  
  * Sử dụng versioning, di chuyển đối tượng và replication multi-region.

* Tự đánh giá:
  * Nắm vững các bước triển khai AWS Backup, Storage Gateway, S3 và CloudFront.  
  * Thực hành test restore, versioning, replication và dọn dẹp tài nguyên.  
  * Sẵn sàng cho tuần tiếp theo với các bài tập AWS nâng cao về bảo mật và tối ưu chi phí.
