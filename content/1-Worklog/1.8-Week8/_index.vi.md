---
title: "Worklog Tuần 8"
date: 2025-10-27
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 8:

* Nắm được yêu cầu kiến trúc cần xây dựng cho dự án.
* Thành thạo cách sử dụng draw.io để dựng sơ đồ hệ thống.
* Hiểu rõ mối quan hệ giữa các service AWS trong kiến trúc: Networking, Compute, Database, CI/CD, Monitoring.
* Hoàn thiện bản **Network Architecture Diagram** và gửi mentor review.


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | --------------- |
| 2 | - Thu thập yêu cầu kiến trúc từ mentor <br> - Xác định phạm vi kiến trúc cần vẽ (VPC, subnet, routing, frontend, backend, database, CI/CD…) | 27/10/2025 | 27/10/2025 | Nội bộ FCJ |
| 3 | - Bắt đầu dựng sơ đồ kiến trúc mạng trên draw.io <br> - Tạo VPC, public/private subnet, Internet Gateway <br> - Thêm Route 53, CloudFront, S3 FE | 28/10/2025 | 28/10/2025 | AWS Docs |
| 4 | - Thêm API Gateway, EC2, Security Group <br> - Thiết kế RDS trong private subnet <br> - Vẽ luồng xử lý FE → CloudFront → API → EC2 → RDS | 29/10/2025 | 29/10/2025 | AWS Architecture Icons |
| 5 | - Tích hợp CI/CD pipeline (CodePipeline, CodeBuild, CloudFormation) <br> - Thêm Cognito/Auth và hoàn thiện Security Layer | 30/10/2025 | 30/10/2025 | aws.amazon.com |
| 6 | - Tối ưu bố cục sơ đồ, chỉnh màu + border <br> - Đánh số thứ tự luồng xử lý <br> - Xuất bản sơ đồ và gửi mentor nhận xét | 31/10/2025 | 31/10/2025 | Nội bộ FCJ |
| 7 | - Nhận feedback từ mentor: cập nhật subnet, luồng xử lý API, lớp bảo mật <br> - Chỉnh sửa lại sơ đồ theo góp ý | 01/11/2025 | 01/11/2025 | Trao đổi trực tiếp |
| CN | - Tổng hợp bài học rút ra trong khi xây dựng kiến trúc <br> - Hoàn thiện Worklog tuần | 02/11/2025 | 02/11/2025 |  |


### Kết quả đạt được tuần 8:

* Hoàn thành sơ đồ **AWS Network Architecture Diagram** đầy đủ thành phần:
  * Route 53, CloudFront, S3 bucket frontend.
  * API Gateway → EC2 backend.
  * NAT Gateway + Internet Gateway.
  * RDS trong private subnet.
  * CI/CD: CodePipeline, CodeBuild, CloudFormation.
  * Monitoring & Security: CloudWatch, CloudTrail, IAM, Secrets Manager, SNS.

* Hiểu rõ cách các thành phần kết nối trong mô hình:
  * Luồng request của user đến FE/BE.
  * Cách tách biệt public/private subnet.
  * Cơ chế NAT để EC2 truy cập internet an toàn.
  * Luồng API Gateway → EC2 → RDS.

* Nắm được cách chuẩn hoá sơ đồ kỹ thuật theo chuẩn AWS:
  * Sử dụng đúng icon, nhóm dịch vụ, phân layer rõ ràng.
  * Đánh dấu số thứ tự các bước xử lý.

* Hoàn thiện bản diagram để đưa vào báo cáo và gửi cho mentor đánh giá.


