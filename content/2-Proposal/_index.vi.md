---
title: "Bản đề xuất"
date: 2025-09-10
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

Tại phần này, bạn cần tóm tắt các nội dung trong workshop mà bạn **dự tính** sẽ làm.

# Blood Donation Support System
## Phần mềm hỗ trợ hiến máu


### 1. Tóm tắt điều hành  
Blood Donation Support System (BDSS)** là nền tảng web hỗ trợ quản lý và kết nối người hiến máu với cơ sở y tế. Dự án được phát triển bởi nhóm sinh viên tại TP. Hồ Chí Minh nhằm tối ưu quy trình hiến máu, giảm tải khâu tìm kiếm người hiến và nâng cao hiệu quả truyền thông y tế.

Hệ thống được xây dựng trên **kiến trúc AWS Cloud**, sử dụng **Amazon EC2**, **Amazon RDS**, **API Gateway**, **Cognito** và **CI/CD Pipeline (GitLab + CodePipeline)** để tự động triển khai. BDSS hỗ trợ bốn nhóm người dùng (Guest, Member, Staff, Admin), cung cấp tính năng tra cứu, đăng ký hiến máu, quản lý kho máu, theo dõi quy trình hiến máu và báo cáo trực quan.

### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Các cơ sở y tế hiện đang quản lý quy trình hiến máu thủ công hoặc thông qua các công cụ rời rạc. Việc tìm kiếm người hiến máu phù hợp nhóm máu hoặc theo khu vực gặp khó khăn, đặc biệt trong tình huống khẩn cấp. Ngoài ra, hệ thống lưu trữ dữ liệu chưa đồng bộ, gây khó khăn trong việc phân tích, báo cáo và tối ưu chiến dịch hiến máu.  

*Giải pháp*  
Phát triển **nền tảng hỗ trợ hiến máu toàn diện trên AWS Cloud**, với các chức năng quản lý hiến máu, tìm kiếm người hiến và người cần máu theo nhóm máu hoặc vị trí địa lý, tích hợp xác thực người dùng qua Amazon Cognito và quản trị dữ liệu trên Amazon RDS. Frontend được triển khai qua **Route 53 + CloudFront**, backend thông qua **API Gateway – EC2**, cơ sở dữ liệu MySQL trên **Amazon RDS**, và pipeline tự động CI/CD bằng **GitLab – CodePipeline**.

*Lợi ích và hoàn vốn đầu tư (ROI)*  
Giảm 60–70% thời gian tìm kiếm người hiến máu phù hợp. Tăng độ chính xác thông tin nhóm máu và vị trí. Tối ưu chi phí vận hành với kiến trúc cloud linh hoạt, trả phí theo mức sử dụng. Cải thiện khả năng phản hồi trong các trường hợp máu khẩn cấp 

### 3. Kiến trúc giải pháp  
Nền tảng áp dụng kiến trúc AWS Serverless để quản lý dữ liệu từ 5 trạm dựa trên Raspberry Pi, có thể mở rộng lên 15 trạm. Dữ liệu được tiếp nhận qua AWS IoT Core, lưu trữ trong S3 data lake và xử lý bởi AWS Glue Crawlers và ETL jobs để chuyển đổi và tải vào một S3 bucket khác cho mục đích phân tích. Lambda và API Gateway xử lý bổ sung, trong khi Amplify với Next.js cung cấp bảng điều khiển được bảo mật bởi Cognito.  

![Blood Donation Support Software Architecture](/images/2-Proposal/edge_bdss.png)

![Blood Donation Support System Platform Architecture](/images/2-Proposal/platform_bdss.png)

Hệ thống được chia thành **4 lớp chính**:

1. *Edge Networking Layer:*
*Route 53* quản lý domain và DNS routing.
*CloudFront* tăng tốc độ tải trang và phân phối nội dung tĩnh.
*AWS WAF* bảo vệ chống tấn công web (SQL injection, DDoS).

2. *Application & Data Layer:*
*Amazon EC2*: Triển khai backend API và xử lý nghiệp vụ chính.
*Amazon RDS (MySQL)*: Lưu trữ dữ liệu người hiến máu, nhóm máu, lịch sử hiến.
*API Gateway*: Giao tiếp giữa frontend và backend.
*Elastic Load Balancer (ELB)*: Phân phối tải cho các instance EC2.
*NAT Gateway & Internet Gateway*: Hỗ trợ kết nối Internet an toàn.

3. *CI/CD & DevOps Layer:*
*GitLab*: Quản lý mã nguồn.
*AWS CodePipeline, CodeBuild*: Triển khai và cập nhật tự động.

4. *Monitoring & Security Layer:*
*Amazon Cognito*: Xác thực và phân quyền (Guest, Member, Staff, Admin).
*CloudWatch, CloudTrail, IAM, Secrets Manager*: Giám sát, bảo mật, cảnh báo hệ thống.
*SNS*: Gửi thông báo khi có sự kiện (máu khẩn cấp, người hiến phù hợp).


### 4. Triển khai kỹ thuật  
*Các giai đoạn triển khai*  
1. *Phân tích & thiết kế (Tháng 1)* 
* Thu thập yêu cầu, xác định use case, thiết kế ERD và kiến trúc AWS.

2. *Thiết lập hạ tầng & pipeline (Tháng 2)*
* Cấu hình Route 53, CloudFront, EC2, RDS và CI/CD trên AWS.

3. *Phát triển & kiểm thử (Tháng 3–4)*
* Xây dựng các module chính: đăng ký hiến máu, tìm kiếm, quản lý kho máu.
* Tích hợp Cognito và hệ thống cảnh báo SNS.

4. *Triển khai & vận hành (Tháng 5)*
* Triển khai sản phẩm chính thức và giám sát bằng CloudWatch.

*Yêu cầu kỹ thuật chính:*
*Frontend:* React/Next.js hoặc Angular (deploy qua S3/CloudFront).
*Backend:* Node.js/Express trên EC2, giao tiếp qua REST API Gateway.
*Database:* Amazon RDS MySQL, tối ưu query và backup định kỳ.
*CI/CD:* GitLab → CodeBuild → CodePipeline → EC2.
*Auth:* Cognito (4 vai trò: Guest, Member, Staff, Admin).
*Alert & Logs:* SNS + CloudWatch + CloudTrail.

### 5. Lộ trình & Mốc triển khai  
| Thời gian | Giai đoạn | Kết quả chính |
| ------------- | ---------------------------- | ------------------------------------------------ |
| **Tháng 1** | Phân tích yêu cầu & thiết kế | Kiến trúc AWS + sơ đồ use case |
| **Tháng 2** | Thiết lập hạ tầng & pipeline | EC2, RDS, API Gateway hoạt động |
| **Tháng 3–4** | Phát triển & kiểm thử | Hoàn thiện các module chính |
| **Tháng 5** | Triển khai chính thức | Hệ thống hoạt động ổn định, có báo cáo Dashboard |

 

### 6. Ước tính ngân sách  
| Dịch vụ | Ước tính chi phí/tháng (USD) | Ghi chú |
| ------------------------------- | ---------------------------- | -------------------- |
| EC2 (t2.micro) | 3.50 | Backend REST API |
| Amazon RDS (MySQL) | 2.80 | 20 GB storage |
| API Gateway | 0.50 | 5.000 request |
| CloudFront + S3 | 0.80 | Website + CDN |
| Route 53 | 0.50 | Domain & DNS |
| Cognito | 0.10 | <100 người dùng |
| CloudWatch + Logs | 0.30 | Giám sát và cảnh báo |
| CI/CD (CodePipeline, CodeBuild) | 0.40 | Triển khai tự động |
| **Tổng cộng** | **8.9 USD/tháng** | ~106.8 USD/năm |

> Toàn bộ chi phí có thể điều chỉnh dựa trên AWS Free Tier hoặc sử dụng spot instance.

### 7. Đánh giá rủi ro  
| Rủi ro | Ảnh hưởng | Xác suất | Biện pháp giảm thiểu |
| -------------------------- | ---------- | ---------- | --------------------------------- |
| Mất kết nối Internet | Trung bình | Trung bình | Dự phòng trên EC2 backup |
| Tấn công DDoS | Cao | Thấp | AWS WAF + CloudFront |
| Lỗi dữ liệu người dùng | Cao | Thấp | RDS backup + IAM hạn chế truy cập |
| Chi phí vượt mức | Trung bình | Thấp | Cảnh báo ngân sách AWS |
| Gián đoạn triển khai CI/CD | Thấp | Trung bình | Kiểm tra pipeline trước khi merge |

### 8. Kết quả kỳ vọng  
*Kỹ thuật:* Hệ thống cloud-native, CI/CD tự động, hỗ trợ đa người dùng và bảo mật cao.
*Ứng dụng:* Giúp cơ sở y tế quản lý hiến máu hiệu quả, giảm thiểu quy trình thủ công.
*Mở rộng:* Có thể nhân rộng cho nhiều bệnh viện khác, tích hợp thêm AI phân tích nhu cầu nhóm máu hoặc dự đoán đợt hiến máu sắp tới.