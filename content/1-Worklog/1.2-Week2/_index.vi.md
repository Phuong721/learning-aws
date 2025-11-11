---
title: "Worklog Tuần 2"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 2:

* Kết nối, làm quen với các thành viên trong First Cloud Journey.
* Hiểu dịch vụ AWS cơ bản, cách dùng console & CLI.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | ---------------- | -------------- |
| 2 | - Giới thiệu EC2 <br>&emsp; + Khái niệm EC2 <br>&emsp; + Instance Types (t2.micro, t3, m5...) <br>&emsp; + AMI (Amazon Machine Image) <br>&emsp; + EBS cơ bản | 08/09/2025 | 08/09/2025 | <https://000002.awsstudygroup.com/> |
| 3 | - **Thực hành 1:** <br>&emsp; + Tạo EC2 instance (Amazon Linux 2) <br>&emsp; + Hiểu cấu hình cơ bản khi khởi tạo <br>&emsp; + Tìm hiểu Key Pair để kết nối | 09/09/2025 | 09/09/2025 | <https://000002.awsstudygroup.com/> |
| 4 | - Bảo mật và mạng: <br>&emsp; + Security Groups (firewall cho EC2) <br>&emsp; + Elastic IP (cố định IP) <br>&emsp; + Networking cơ bản (VPC mặc định, Subnet) | 10/09/2025 | 10/09/2025 | <https://000003.awsstudygroup.com/> |
| 5 | - **Thực hành 2:** <br>&emsp; + Kết nối SSH vào EC2 qua key pair <br>&emsp; + Thực hành remote và thao tác trên Linux instance <br>&emsp; + Test Elastic IP gán vào instance | 11/09/2025 | 11/09/2025 | <https://000003.awsstudygroup.com/> |
| 6 | - Quản lý lưu trữ: <br>&emsp; + Gắn thêm EBS Volume vào EC2 <br>&emsp; + Mount và kiểm tra dung lượng <br>&emsp; + Tìm hiểu snapshot cơ bản | 12/09/2025 | 12/09/2025 | <https://000004.awsstudygroup.com/> |
| 7 | - **Thực hành 3 + Tổng kết:** <br>&emsp; + Tạo thêm 1 instance để luyện tập <br>&emsp; + Gắn / tháo EBS volume <br>&emsp; + Kiểm tra toàn bộ quy trình (Tạo → Kết nối → Elastic IP → EBS) | 13/09/2025 | 13/09/2025 | <https://000004.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Hiểu rõ kiến thức cơ bản về **Amazon EC2**:  
  * Các loại Instance Types (t2.micro, t3, m5...) và mục đích sử dụng.
  * AMI (Amazon Machine Image) và cách chọn hệ điều hành khi tạo máy ảo.
  * Hiểu EBS (Elastic Block Store) và vai trò của nó trong lưu trữ dữ liệu cho EC2.

* Thực hành thành công việc **tạo EC2 instance** trên AWS Console:
  * Lựa chọn AMI (Amazon Linux 2).
  * Chọn cấu hình instance phù hợp (Free Tier).
  * Tạo và tải về Key Pair để chuẩn bị kết nối.

* Làm quen với **Security Groups** và hiểu cách thiết lập firewall cho instance.

* Thực hành với **Elastic IP**: tạo, gán và kiểm tra tính ổn định của IP tĩnh so với Public IP mặc định.

* Thành thạo cách **kết nối SSH** vào EC2: 
  * Dùng key pair `.pem` để kết nối.
  * Kiểm tra hệ thống, chạy lệnh cơ bản trên Linux instance.

* Quản lý **lưu trữ với EBS**:
  * Gắn thêm 1 EBS volume vào instance.
  * Mount volume, format và kiểm tra dung lượng khả dụng.
  * Hiểu snapshot là gì và khi nào nên dùng để backup.

* Kỹ năng thực hành cuối tuần:
  * Triển khai toàn bộ quy trình từ **Tạo → Kết nối → Elastic IP → Gắn EBS → Kiểm tra snapshot**.
  * Có thể lặp lại các bước này một cách độc lập.

* Nắm được sự kết hợp giữa lý thuyết và thực hành trong quản lý EC2 và tài nguyên đi kèm.