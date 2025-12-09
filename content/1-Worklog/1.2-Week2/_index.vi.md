---
title: "Worklog Tuần 2"
date: 2025-09-15
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Học và thực hành thiết lập mạng AWS bằng VPC, Subnet, Route Table, Internet Gateway, NAT Gateway và các cơ chế bảo mật.  
* Cấu hình EC2 instances trong các subnet và kiểm tra kết nối.  
* Thiết lập Hybrid DNS với Route 53 Resolver.  
* Tìm hiểu và triển khai VPC Peering và AWS Transit Gateway.  

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Giới thiệu Amazon VPC và AWS VPN Site-to-Site (Module 02-Lab03-01) <br> - Subnets (Module 02-Lab03-01.1) <br> - Route Table (Module 02-Lab03-01.2) <br> - Internet Gateway (IGW) (Module 02-Lab03-01.3) <br> - NAT Gateway (Module 02-Lab03-01.4) | 15/09/2025 | 15/09/2025 | <https://000003.awsstudygroup.com/> |
| 3   | - Cấu hình Security Group (Module 02-Lab03-02.1) <br> - Network ACLs (Module 02-Lab03-02.2) <br> - VPC Resource Map (Module 02-Lab03-02.3) | 16/09/2025 | 16/09/2025 | <https://000003.awsstudygroup.com/> |
| 4   | - Tạo VPC (Module 02-Lab03-03.1) <br> - Tạo Subnet (Module 02-Lab03-03.2) <br> - Tạo Internet Gateway (Module 02-Lab03-03.3) <br> - Tạo Route Table cho Outbound Internet Routing qua IGW (Module 02-Lab03-03.4) <br> - Tạo Security Groups (Module 02-Lab03-03.5) | 17/09/2025 | 17/09/2025 | <https://000010.awsstudygroup.com/> |
| 5   | - Tạo EC2 Instances trong Subnets (Module 02-Lab03-04.1) <br> - Kiểm tra kết nối (Module 02-Lab03-04.2) <br> - Tạo NAT Gateway (Module 02-Lab03-04.3) <br> - EC2 Instance Connect Endpoint (Module 02-Lab03-04.5) | 18/09/2025 | 18/09/2025 | <https://000010.awsstudygroup.com/> |
| 6   | - Thiết lập Hybrid DNS với Route 53 Resolver (Module 02-Lab10-01) <br> - Tạo Key Pair (Module 02-Lab10-02.1) <br> - Khởi tạo CloudFormation Template (Module 02-Lab10-02.2) <br> - Cấu hình Security Group (Module 02-Lab10-02.3) <br> - Kết nối đến RDGW (Module 02-Lab10-03) | 19/09/2025 | 19/09/2025 | <https://000019.awsstudygroup.com/> |
| 7   | - Thiết lập DNS: Route 53 Outbound Endpoint (Module 02-Lab10-05.1) <br> - Tạo Resolver Rules (Module 02-Lab10-05.2) <br> - Tạo Inbound Endpoints (Module 02-Lab10-05.3) <br> - Kiểm tra kết quả (Module 02-Lab10-05.4) <br> - Dọn dẹp tài nguyên (Module 02-Lab10-06) | 20/09/2025 | 20/09/2025 | <https://000019.awsstudygroup.com/> |
| CN  | - VPC Peering setup: Giới thiệu (Module 02-Lab19-01) <br> - Khởi tạo CloudFormation Templates (Module 02-Lab19-02.1) <br> - Tạo Security Group (Module 02-Lab19-02.2) <br> - Tạo EC2 instance (Module 02-Lab19-02.3) <br> - Cập nhật Network ACLs (Module 02-Lab19-03) <br> - Tạo peering connection (Module 02-Lab19-04) <br> - Cấu hình Route Tables (Module 02-Lab19-05) <br> - Bật Cross-Peer DNS (Module 02-Lab19-06) <br> - Dọn dẹp tài nguyên (Module 02-Lab19-07) <br> - AWS Transit Gateway setup: Giới thiệu (Module 02-Lab20-01) <br> - Các bước chuẩn bị (Module 02-Lab20-02) <br> - Tạo Transit Gateway (Module 02-Lab20-03) <br> - Tạo TGW Attachments (Module 02-Lab20-04) <br> - Tạo TGW Route Tables (Module 02-Lab20-05) <br> - Thêm TGW Routes vào VPC Route Tables (Module 02-Lab20-06) <br> - Dọn dẹp tài nguyên (Module 02-Lab20-07) | 21/09/2025 | 21/09/2025 | <https://000020.awsstudygroup.com/> |

### Kết quả đạt được tuần 2:

* Mạng AWS:
  * Tạo và cấu hình VPC, Subnet, Route Table, Internet Gateway, NAT Gateway, Security Groups.  
  * Triển khai EC2 instances trong các subnet và kiểm tra kết nối thành công.  
  * Cấu hình EC2 Instance Connect Endpoint để truy cập dễ dàng hơn.

* Hybrid DNS:
  * Tạo Key Pairs và khởi tạo CloudFormation Templates.  
  * Cấu hình Security Groups và kết nối đến RDGW.  
  * Tạo Route 53 Outbound/Inbound Endpoints, thiết lập Resolver Rules và kiểm tra kết quả.  
  * Dọn dẹp tài nguyên DNS sau khi kiểm tra.

* VPC Peering & Transit Gateway:
  * Thiết lập VPC Peering, cấu hình Route Tables và bật Cross-Peer DNS.  
  * Tạo AWS Transit Gateway, attachments, route tables, thêm routes vào VPC route tables.  
  * Dọn dẹp các tài nguyên để tránh phát sinh chi phí không mong muốn.

* Tự đánh giá:
  * Có kinh nghiệm thực hành với mạng AWS, Hybrid DNS, VPC Peering và Transit Gateway.  
  * Triển khai, kiểm tra và dọn dẹp tài nguyên thành công.  
  * Sẵn sàng cho các tuần tiếp theo với kiến thức nâng cao hơn.
