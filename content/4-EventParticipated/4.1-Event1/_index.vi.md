---
title: "Event 1"
date: 2025-11-17
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Bài thu hoạch “AWS Mastery #2 – CloudFormation & CDK Workshop”

### Mục Đích Của Sự Kiện

Workshop “AWS Mastery #2 – CloudFormation & CDK” được tổ chức nhằm giúp người tham dự:

- Nắm bắt tư duy **Infrastructure as Code (IaC)** – phương pháp quản lý hệ thống hạ tầng bằng mã nguồn.
- Hiểu rõ cách AWS triển khai, tự động hóa và vận hành tài nguyên thông qua **CloudFormation** và **CDK**.
- Cung cấp góc nhìn tổng quan và thực tiễn về **Docker**, **container orchestration**, và các dịch vụ như ECS, EKS, App Runner.
- Trau dồi tư duy DevOps, khả năng kiểm soát thay đổi, tái sử dụng hạ tầng, và triển khai nhanh chóng.
- Trực tiếp quan sát các demo giúp củng cố khả năng triển khai hạ tầng thực tế.

Sự kiện phù hợp với lập trình viên, DevOps engineer, cloud engineer hoặc bất kỳ ai đang muốn tiếp cận tự động hóa trên AWS.

---

### Danh Sách Diễn Giả

- **Bao Huynh Thinh Nguyen** – AWS Community Builder  
- **Vi Tran** – AWS Community Builder  

Các diễn giả đều có nhiều kinh nghiệm triển khai hệ thống AWS thực tế, nên phần trình bày rất thực tiễn, dễ theo kịp và chứa nhiều kinh nghiệm áp dụng ngay.

---

# Nội Dung Nổi Bật

## 1. Tư duy Infrastructure as Code (IaC)

Workshop bắt đầu với việc chỉ ra lý do vì sao **ClickOps** (click chuột thủ công trên console) gây ra hạn chế:

- Dễ bị lỗi do thao tác người dùng.
- Khó tái tạo môi trường giữa các team.
- Không kiểm soát được các thay đổi ngoài quy trình.
- Khó audit, khó rollback và khó mở rộng.

IaC được giới thiệu như một bước chuyển đổi tất yếu trong DevOps:

- **Automation:** Hạ tầng được tạo và quản lý hoàn toàn tự động.
- **Reproducibility:** Môi trường được build ra giống 100%.
- **Scalability:** Mở rộng nhanh chóng bằng code.
- **Collaboration:** Mọi thay đổi được version-control (Git), dễ phối hợp nhóm.

---

## 2. AWS CloudFormation – Công cụ IaC “native” của AWS

### CloudFormation là gì?

CloudFormation cho phép mô tả toàn bộ hạ tầng bằng **YAML hoặc JSON** và AWS sẽ tự động tạo mọi thứ.

Các khái niệm quan trọng được trình bày:

### **CloudFormation Template Anatomy**
1. **Parameters:**  
   - Cho phép template tái sử dụng bằng cách truyền tham số.  
   - Ví dụ: AMI ID, instance type, VPC ID.

2. **Mappings:**  
   - Chứa các giá trị phụ thuộc vùng, ví dụ AMI khác nhau giữa us-east-1 và ap-southeast-1.

3. **Conditions:**  
   - Tạo tài nguyên theo điều kiện (ví dụ chỉ tạo EC2 nếu environment = production).

4. **Resources:**  
   - Phần quan trọng nhất của template.  
   - Mô tả full tài nguyên S3, EC2, IAM, VPC,...

5. **Outputs:**  
   - Xuất giá trị ra ngoài, dùng để cross-stack reference hoặc chia sẻ cho team.

### **Drift Detection**
- Tính năng cho phép phát hiện khi một tài nguyên bị thay đổi trực tiếp trên console.
- Giúp giữ hạ tầng “khớp” với template đã định nghĩa.

Diễn giả trình bày minh hoạ trực quan giúp tôi dễ hiểu về sự khác biệt giữa “state từ template” và “state ngoài đời thực”.

---

## 3. AWS CDK – Viết hạ tầng bằng ngôn ngữ lập trình

CDK được giới thiệu như phiên bản nâng cấp của CloudFormation:

- Dùng **ngôn ngữ lập trình** như TypeScript, Python, Java, Go.
- Code CDK sẽ được dịch thành CloudFormation template thông qua `cdk synth`.
- Dễ tái sử dụng, dễ tạo abstraction, dễ maintain.

### Các khái niệm cốt lõi:

#### **Constructs**
- L1: mapping 1:1 CloudFormation (chi tiết nhất).
- L2: API thân thiện hơn, có default best practice.
- L3: solution patterns triển khai trọn gói (như website hosting, pipeline).

#### **Stack & App**
- Stack = 1 CloudFormation stack.
- App có thể gồm nhiều stack.

#### **CDK CLI**
Một số lệnh quan trọng:
- `cdk init` – tạo project.
- `cdk bootstrap` – chuẩn bị môi trường lần đầu.
- `cdk synth` – generate CloudFormation template.
- `cdk deploy` – triển khai.
- `cdk destroy` – xóa.
- `cdk diff` – so sánh thay đổi.
- `cdk drift` – kiểm tra drift.

CDK giúp người làm DevOps và developer tự động hóa dễ dàng hơn rất nhiều so với viết YAML thủ công.

---

## 4. Docker & Container Services trên AWS

Phần này rất quan trọng vì container gần như là tiêu chuẩn hiện nay.

### **Docker Fundamentals**
- Container nhẹ, khởi động nhanh hơn VM.
- Dockerfile: mô tả cách build image.
- Image: blueprint tạo container.

### **Amazon ECR**
- Registry chứa images.
- Hỗ trợ scanning, immutable tags và IAM authorization.

---

## 5. Orchestration: ECS, EKS và App Runner

### **Amazon ECS**
- Dịch vụ orchestration “simple & native”.
- 2 kiểu chạy:
  - EC2 launch type (tự quản lý server)
  - Fargate launch type (serverless)
- Thành phần:
  - **Cluster – Task Definition – Service**

### **Amazon EKS**
- Managed Kubernetes.
- Dùng cho workloads cần multi-cloud hoặc cần đầy đủ sức mạnh Kubernetes.

### **App Runner**
- Dịch vụ đơn giản nhất để chạy web app/container.
- Tự build → deploy → scale.
- Thích hợp cho team nhỏ hoặc prototype.

---

# Những Gì Học Được

## 1. Tư duy quản trị hạ tầng hiện đại

- IaC không chỉ là công cụ, mà còn là **triết lý quản lý hạ tầng chuẩn hoá**, giảm rủi ro vận hành.
- Drift detection là công cụ hữu ích để đảm bảo sự ổn định.

## 2. Kiến thức chuyên sâu về IaC

- Hiểu chi tiết các component của CloudFormation template giúp tôi có thể đọc – viết template tốt hơn.
- Học được cách viết CDK với construct L2/L3 nhanh và “clean” hơn nhiều so với YAML.

## 3. Kiến trúc container hiện đại

- Khả năng phân biệt rõ khi nào dùng ECS, khi nào dùng Fargate, khi nào dùng EKS.
- Biết cách đánh giá workloads dựa trên chi phí – hiệu suất – yêu cầu vận hành.

## 4. Kinh nghiệm thực tế trong DevOps

- `cdk diff` cực kỳ hữu ích trước khi deploy production.
- IaC giúp các team rất dễ review code trước khi bản thân hạ tầng được tạo ra.

---

# Ứng Dụng Vào Công Việc

- **Bắt đầu chuyển hạ tầng nhỏ sang IaC** bằng CloudFormation hoặc CDK.
- Viết template cho S3 bucket, IAM role, hoặc VPC cơ bản để thực hành.
- Triển khai ứng dụng mẫu bằng ECS Fargate để hiểu end-to-end pipeline.
- Tự xây dựng demo CDK áp dụng constructs ở cả L1–L3.
- Đề xuất áp dụng container registry ECR cho pipeline CI/CD của team.
- Tạo tài liệu nội bộ hướng dẫn cách dùng `cdk diff` để kiểm soát thay đổi.

---

# Trải Nghiệm Trong Event

- Buổi workshop có không khí chuyên nghiệp nhưng rất gần gũi, diễn giả nhiệt tình trả lời câu hỏi.
- Demo trực tiếp CDK và ECS giúp tôi hiểu rõ bản chất “as code” của toàn bộ hệ thống AWS.
- Tôi đặc biệt thích phần so sánh ECS vs EKS vì giúp tôi định hình khi nào sử dụng orchestration đơn giản hoặc Kubernetes.
- Kết nối với những người tham gia khác giúp tôi học thêm nhiều kinh nghiệm trong nghề DevOps.

## Một số hình ảnh trong sự kiện
![Workshop Session 2](../../../static/images/4-EventParticipated/Image1.jpg)
![Workshop Session 2](../../../static/images/4-EventParticipated/Image2.jpg)
![Workshop Session 3](../../../static/images/4-EventParticipated/Image3.jpg)
![Workshop Session 4](../../../static/images/4-EventParticipated/Image4.jpg)
![Group Photo](../../../static/images/4-EventParticipated/Image5.jpg)


> Sau sự kiện, tôi cảm thấy mình tự tin hơn rất nhiều trong việc tiếp cận AWS Infrastructure as Code và container orchestration, đồng thời có định hướng rõ ràng để áp dụng chúng vào công việc thực tế.

