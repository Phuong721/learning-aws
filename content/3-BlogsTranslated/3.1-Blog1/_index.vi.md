---
title: "Blog 1"
date: 2025-08-21
weight: 1
chapter: false
pre: " <b> 3.1 </b> "
---

### Tăng tốc Chiến lược Đám mây của bạn với Kết nối Trực tiếp AWS được Lưu trữ 25 Gbps của Megaport

Khi các doanh nghiệp di chuyển khối lượng công việc quan trọng lên đám mây, hiệu suất mạng đã trở thành yêu cầu kinh doanh cơ bản. Dịch vụ web của Amazon (AWS) Direct Connect cung cấp kết nối mạng chuyên dụng giữa các trung tâm dữ liệu tại chỗ và AWS. Điều này bỏ qua internet công cộng để mang lại hiệu suất mạng ổn định và đáng tin cậy hơn với độ trễ thấp hơn. Sự giới thiệu của 25 Gbps hosted connections lấp đầy khoảng cách giữa các tùy chọn 10 Gbps (thường không đủ) và 100 Gbps (thường là quá mức), cho phép các tổ chức điều chỉnh kích thước kết nối phù hợp mà không ảnh hưởng đến hiệu suất. Megaport, một nhà cung cấp Mạng lưới dưới dạng Dịch vụ (NaaS) hàng đầu và AWS Marketplace Đối tác của chúng tôi là một trong những đơn vị đầu tiên cung cấp kết nối 25 Gbps này trên nhiều Địa điểm Kết nối Trực tiếp Edge thông qua Mạng lưới Định nghĩa Phần mềm Toàn cầu, trải dài hàng trăm trung tâm dữ liệu trên toàn thế giới. Để biết thông tin mới nhất, vui lòng tham khảo Magaport public network footprint page.

Sử dụng nền tảng tự phục vụ của Megaport, các tổ chức có thể cung cấp, mở rộng quy mô và quản lý kết nối AWS hiệu suất cao chỉ trong vài phút thay vì hàng tuần hoặc hàng tháng. Trong bài viết này, chúng tôi sẽ mô tả cách sự kết hợp mạnh mẽ giữa các dịch vụ AWS và Megaport cho phép các kiến ​​trúc sư đám mây và lãnh đạo CNTT xây dựng các mạng lai thế hệ tiếp theo hỗ trợ các ứng dụng dữ liệu chuyên sâu, tăng cường bảo mật và tối ưu hóa chi phí — đồng thời vẫn duy trì tính linh hoạt để thích ứng với nhu cầu kinh doanh thay đổi.

---

## Điều kiện tiên quyết

Chúng tôi giả định rằng bạn đã quen thuộc với các cấu trúc mạng cốt lõi trên AWS, đặc biệt là Direct Connect. Mặc dù chúng tôi không đi sâu vào định nghĩa, nhưng chúng tôi sẽ nêu bật vai trò của nó trong việc hỗ trợ các kiến ​​trúc kết nối lai liên quan đến các kết nối được lưu trữ trên Direct Connect. Nếu bạn chưa quen với những khái niệm này, chúng tôi khuyên bạn nên xem lại tài liệu Direct Connect để biết thêm chi tiết choosing between Direct Connect dedicated and hosted connections.

Đối với kiến ​​thức nền tảng, Getting Started with AWS Direct Connect hướng dẫn cũng là một nguồn tài nguyên hữu ích.

---

## Các trường hợp sử dụng chính cho Kết nối trực tiếp 25 Gbps

Các phần sau đây sẽ trình bày chi tiết các trường hợp sử dụng chính của Direct Connect 25 Gbps.

### 1. Di chuyển đám mây
Di chuyển dữ liệu doanh nghiệp quy mô lớn liên quan đến việc chuyển các tập dữ liệu khổng lồ. Kết nối lưu trữ 25 Gbps cho phép các tổ chức rút ngắn thời gian di chuyển từ vài ngày xuống còn vài giờ mà vẫn duy trì hiệu suất ổn định và an toàn. Việc di chuyển cơ sở dữ liệu 100 TB, vốn mất hơn 22 giờ với kết nối 10 Gbps, có thể hoàn thành trong khoảng 9 giờ, giúp rút ngắn đáng kể thời gian đưa vào sản xuất.  

| Connection Speed | Data volume | Estimated Migration Time | Performance Gain |
|----------------- |------------ |------------------------- |----------------  |
| 10 Gbps          | 100 TB      | ~22 hours                | Baseline         |
| 25 Gbps          | 100 TB      | ~9 hours                 | ~59% faster      |

*Table 1: Bandwidth effects on large-scale data migration*

### 2. Di chuyển dữ liệu
Các tổ chức thu thập dữ liệu từ các vị trí biên hoặc môi trường tại chỗ được hưởng lợi từ các kết nối có thông lượng cao, có thể dự đoán trước cho các khối lượng công việc phân tích, sao lưu và lưu trữ. Các công ty truyền thông có thể chuyển các tệp video lớn một cách hiệu quả giữa các bộ biên tập và AWS, trong khi các tổ chức chăm sóc sức khỏe có thể di chuyển các tập dữ liệu hình ảnh lên đám mây để phân tích AI mà vẫn duy trì tính tuân thủ thông qua kết nối riêng tư. Cấp độ 25 Gbps đặc biệt hữu ích cho các triển khai Internet vạn vật (IoT) tạo ra khối lượng lớn dữ liệu cảm biến, các hoạt động sao lưu quy mô lớn với các yêu cầu Mục tiêu Điểm Phục hồi (RPO) khắt khe, và các tổ chức đào tạo mô hình học máy (ML) với các tập dữ liệu tại chỗ đáng kể.

### 3. Hỗ trợ đám mây lai
Khi kiến ​​trúc lai ngày càng phổ biến, việc kết nối đáng tin cậy giữa các hệ thống tại chỗ và AWS là điều cần thiết. Kết nối lưu trữ 25 Gbps của Megaport cung cấp dung lượng cần thiết cho cơ sở dữ liệu phân tán, giải pháp lưu trữ lai và các dịch vụ vi mô trải rộng trên nhiều môi trường. Các tổ chức có thể triển khai các chính sách bảo mật nhất quán và trải nghiệm ứng dụng liền mạch trên toàn bộ ngăn xếp công nghệ của mình, đồng thời duy trì khoảng trống hiệu suất cần thiết cho các giai đoạn khối lượng công việc cao điểm và tăng trưởng trong tương lai.

### 4. Ứng dụng nhạy cảm với độ trễ
Các ứng dụng như nền tảng giao dịch tài chính, hệ thống tự động và công cụ cộng tác thời gian thực đều yêu cầu độ trễ tối thiểu. Kết nối chuyên dụng 25 Gbps duy trì hiệu suất ổn định, độ trễ thấp bằng cách bỏ qua internet công cộng, đồng thời cung cấp đủ băng thông để ngăn ngừa tắc nghẽn trong giờ cao điểm. Đối với các ngành công nghiệp đòi hỏi tốc độ tính bằng mili giây — chẳng hạn như giao dịch tần suất cao, trò chơi trực tuyến hoặc y tế từ xa — hiệu suất dự đoán được của Direct Connect mang lại lợi thế cạnh tranh đồng thời duy trì tính bảo mật thông qua kết nối riêng tư.  

Lợi ích cho các ngành như: giao dịch tần suất cao, trò chơi trực tuyến, y tế từ xa.

### 5. Kiểm soát chi phí
Gói 25 Gbps mang đến một giải pháp tiết kiệm chi phí để mở rộng dung lượng mạng mà không cần cung cấp quá mức. Các tổ chức trước đây buộc phải lựa chọn giữa kết nối 10 Gbps không đủ hoặc kết nối 100 Gbps quá mức giờ đây có thể chọn điểm cân bằng tối ưu, thường tiết kiệm 50-60% so với tùy chọn 100 Gbps. Nền tảng linh hoạt của Megaport cũng cho phép doanh nghiệp điều chỉnh băng thông khi nhu cầu thay đổi, hỗ trợ tối ưu hóa chi phí trong suốt vòng đời ứng dụng mà vẫn đảm bảo hiệu suất cần thiết cho khối lượng công việc đám mây hiện đại.

---

## Lợi ích triển khai AWS Direct Connect 25 Gbps với Megaport

Các phần sau đây sẽ hướng dẫn chi tiết về những lợi ích khi triển khai Direct Connect 25 Gbps với Megaport.

### 1. Chuyển dữ liệu riêng tư, an toàn
Các kết nối lưu trữ của Megaport cung cấp một đường dẫn riêng tư đến AWS, bỏ qua internet công cộng, giúp tăng cường quyền riêng tư dữ liệu, giảm thiểu nguy cơ bị tấn công bởi các mối đe dọa bảo mật phổ biến và đảm bảo tuân thủ cho các khối lượng công việc nhạy cảm. Kết nối riêng tư này ngày càng quan trọng khi các quy định như Quy định Bảo vệ Dữ liệu Chung (GDPR), Đạo luật Khả năng Chuyển đổi và Trách nhiệm Giải trình Bảo hiểm Y tế (HIPAA) và các yêu cầu cụ thể của ngành áp đặt các biện pháp kiểm soát chặt chẽ hơn đối với việc di chuyển và bảo vệ dữ liệu. Cấp độ 25 Gbps mang lại khả năng bảo mật này mà không ảnh hưởng đến hiệu suất cần thiết cho các ứng dụng dữ liệu chuyên sâu hiện đại.

### 2. Dễ sử dụng
Cổng thông tin tự phục vụ của Megaport cho phép khách hàng cung cấp, mở rộng và quản lý kết nối Direct Connect chỉ trong vài phút. Tính linh hoạt này giúp các nhóm thích ứng nhanh chóng với nhu cầu dự án thay đổi mà không phải chịu chi phí quản lý thủ công. Các tổ chức có thể thiết lập kết nối với AWS Regions gần như theo thời gian thực thay vì phải chờ hàng tuần hoặc hàng tháng cho các mạch viễn thông truyền thống, do đó đẩy nhanh các sáng kiến ​​đám mây và giảm thời gian tạo ra giá trị cho các dự án mới.

### 3. Khả năng tiếp cận toàn cầu
Sự hiện diện của Megaport tại hơn 975 trung tâm dữ liệu trên hơn 26 quốc gia cho phép nó cung cấp quyền truy cập gần như phổ biến vào Direct Connect locations. Các tổ chức có dấu chân phân tán có thể chuẩn hóa phương pháp kết nối nhất quán trên khắp các Vùng AWS, tinh giản kiến ​​trúc và vận hành đồng thời duy trì hiệu suất cao. Phạm vi phủ sóng toàn cầu này đặc biệt có giá trị đối với các doanh nghiệp đa quốc gia triển khai hoạt động theo mặt trời hoặc các tổ chức có yêu cầu nghiêm ngặt về chủ quyền dữ liệu.

### 4. Tính linh hoạt và khả năng mở rộng
Khi nhu cầu tăng lên, khách hàng có thể điều chỉnh băng thông linh hoạt thông qua cổng Megaport. Tính linh hoạt này cho phép các nhóm CNTT mở rộng quy mô một cách hiệu quả về chi phí mà vẫn duy trì hiệu suất tối ưu cho các khối lượng công việc quan trọng. Cấp 25 Gbps cung cấp một giải pháp trung gian lý tưởng, có thể được triển khai như một giải pháp dài hạn hoặc làm bước đệm cho chiến lược mạng lưới đám mây rộng lớn hơn.

---

## Bắt đầu với AWS và Megaport 25 Gbps

Các phần sau đây sẽ hướng dẫn bạn cách sử dụng AWS và Megaport với kết nối lưu trữ 25 Gbps.

### Điều kiện tiên quyết
1. Tài khoản Megaport đang hoạt động và có chức năng thanh toán.  
2. Tài khoản AWS có quyền truy cập Direct Connect.

### Bước 1: Tạo MCR Megaport
1. Đăng nhập vào Megaport Portal.  
2. Lựa chọn +Add Service và chọn MCR (Bộ định tuyến đám mây Megaport) như thể hiện trong Hình 1. Đảm bảo rằng MCR hỗ trợ dung lượng tối thiểu là 25 Gbps, vì điều này sẽ quyết định tốc độ kết nối tối đa khả dụng cho kết nối lưu trữ của bạn.  
3. Làm theo hướng dẫn trên màn hình để hoàn tất thiết lập. Bạn có thể tìm thêm thông tin chi tiết trong Creating MCR Documentation.


### Bước 2: Tạo kết nối lưu trữ từ Megaport đến AWS
1. Trong Cổng thông tin Megaport, hãy chọn MCR của bạn và nhấp vào + Add Connection.
2. Chọn AWS Direct Connect từ các tùy chọn Đám mây.  
3.  Cung cấp thông tin cần thiết và làm theo hướng dẫn:
- Creating a Hosted Connection
- Connection Name: tên mô tả cho kết nối của bạn.
- Service Level Reference: cung cấp mã định danh duy nhất cho mục đích thanh toán hoặc theo dõi.
- Rate Limit: đặt thành 25.000 Mbps để cung cấp kết nối 25 Gbps.  
4. Gửi và triển khai kết nối.

Bạn cũng có thể tạo VIF lưu trữ và các loại kết nối khác (ví dụ: VIF công cộng, VIF trung chuyển), tùy thuộc vào trường hợp sử dụng của bạn.


### Bước 3: Chấp nhận kết nối được lưu trữ trong AWS
1. Đăng nhập vào AWS Console và đi đến AWS Direct Connect.
2. Trong ngăn điều hướng, chọn Connections.
3. Chọn kết nối được lưu trữ và chọn View details.
4. Select the confirmation check box and choose Accept.

### Bước 4: Tạo Giao diện ảo cho kết nối được lưu trữ:
1. Sau khi chấp nhận kết nối, hãy chọn nó và chọn Create Virtual Interface như thể hiện trong Hình 3. 
2. Chọn loại giao diện – thông thường Private để truy cập vào VPC.  
3. Cấu hình như sau:
- Tên giao diện ảo.
- ID VLAN (phải khớp với VLAN được sử dụng trong cấu hình Megaport).
- BGP ASN (mặc định của bạn hoặc AWS).
- Địa chỉ IP ngang hàng BGP (AWS cung cấp một bên; bạn chỉ định bên của mình).
4. Hiệp hội Cổng kết nối: Chọn Cổng kết nối riêng ảo hoặc AWS Transit Gateway được đính kèm vào VPC của bạn.
5. Chọn Create.


### Bước 5: Cấu hình BGP trên Megaport MCR
1. Quay lại Cổng Megaport.
2. Chỉnh sửa Virtual Cross Connect (VXC) để khớp với thông tin chi tiết BGP do AWS cung cấp. 
3. Hiển thị thông tin bạn cần nhập:
- Địa chỉ IP ngang hàng BGP (của bạn và của AWS).
- ASN của bạn (hoặc ASN do AWS chỉ định).
4. Lưu và áp dụng cấu hình.


---

## Kết luận
Trong bài viết này, chúng tôi đã khám phá cách các kết nối lưu trữ 25 Gbps của AWS Direct Connect thông qua Megaport có thể chuyển đổi chiến lược kết nối đám mây của bạn. Chúng tôi đã đề cập đến các trường hợp sử dụng thiết yếu như di chuyển lên đám mây quy mô lớn, ứng dụng dữ liệu chuyên sâu, triển khai đám mây lai và khối lượng công việc nhạy cảm với độ trễ. Bạn đã tìm hiểu cách giải pháp này mang lại khả năng truyền dữ liệu riêng tư, an toàn với khả năng mở rộng linh hoạt, đồng thời tiết kiệm chi phí đáng kể so với các giải pháp thay thế 100 Gbps. Chúng tôi cũng hướng dẫn từng bước thiết lập kết nối lưu trữ 25 Gbps bằng nền tảng tự phục vụ của Megaport.

### Kêu gọi hành động
- Đánh giá yêu cầu về thông lượng mạng hiện tại và tương lai của bạn.
- Khám phá các tùy chọn Kết nối trực tiếp được lưu trữ 25 Gbps trên AWS Direct Connect Partners page.
- Di chuyển đến Megaport’s AWS solution page để tìm hiểu thêm hoặc bắt đầu cung cấp dịch vụ tự phục vụ.

---

## Về các tác giả

**Mokshith Kumar**  
Kiến trúc sư Giải pháp Chuyên gia GTM Cấp cao về Mạng Lõi tại AWS, hỗ trợ ISV và FSI Bắc Mỹ.  
- Vai trò: phát triển chiến lược GTM, dẫn dắt sáng kiến chiến lược, thúc đẩy áp dụng dịch vụ mạng AWS.  
- Sở thích: bơi lội, âm nhạc.

**Miranda Li**  
Kiến trúc sư Giải pháp Cấp cao tại AWS, chuyên ISV và kiến trúc đám mây gốc.  
- 4 năm kinh nghiệm hỗ trợ ISV đổi mới, mở rộng trên AWS.  
- Chuyên môn: IaaS, kiến trúc mạng, bảo mật, phân tích dữ liệu.  
- Sở thích: cầu lông, chạy bộ, các hoạt động ngoài trời.
