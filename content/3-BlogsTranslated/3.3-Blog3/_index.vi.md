---
title: "Giao thức mở cho khả năng tương tác của tác nhân Phần 4: Giao tiếp giữa các tác nhân trên A2A"
date: 2025-08-21
weight: 3
chapter: false
pre: " Artificial Intelligence, Customer Solutions, Generative AI, Open Source "
---


## Giới thiệu:
Chào mừng đến với Phần 4 của loạt bài viết trên blog của chúng tôi về Open Protocols for Agent Interoperability nơi chúng tôi sẽ đề cập đến giao thức Agent-to-Agent (A2A), sự tham gia của AWS với Linux Foundation-based open standard, và sự hỗ trợ của chúng tôi dành cho A2A trong Strands Agents SDK. Dưới đây là những gì chúng tôi đã đề cập cho đến nay:
- Part 1: Giao thức ngữ cảnh mô hình (MCP) tạo điều kiện thuận lợi cho giao tiếp giữa các tác nhân như thế nào và AWS đã nỗ lực cải tiến thông số kỹ thuật MCP ra sao để hỗ trợ tốt hơn cho giao tiếp giữa các tác nhân.
- Part 2: Chi tiết về các bản cập nhật thông số kỹ thuật MCP gần đây liên quan đến Xác thực.
- Part 3: Làm thế nào để xây dựng hệ thống liên tác nhân với cái mới Strands Agents SDK và MCP

Giao thức chuẩn là cách chính để kết nối các dịch vụ mạng. Thông thường, có nhiều giao thức khác nhau để giải quyết các cách kết nối mạng khác nhau. Ở tầng mạng, có hai giao thức chính: TCP và UDP. Mỗi giao thức phù hợp với các nhu cầu cụ thể và không giao thức nào mang tính phổ quát. Điều này cũng đúng khi kết nối các tác nhân AI. Trong phần 4 của loạt bài viết về giao tiếp giữa các tác nhân, chúng tôi sẽ giới thiệu về A2A, cách sử dụng nó để giao tiếp giữa các tác nhân và cách AWS hỗ trợ khách hàng xây dựng hệ thống với A2A.

MCP ban đầu được tạo ra để kết nối các tác nhân với các công cụ, nhưng cũng có thể được sử dụng để kết nối các tác nhân với nhau. A2A được tạo ra để kết nối các tác nhân với nhau và cũng có thể được sử dụng kết hợp với MCP để các tác nhân giao tiếp với các công cụ. Việc sử dụng giao thức nào cho kết nối tác nhân với tác nhân tùy thuộc vào nhu cầu của bạn. AWS hỗ trợ cả hai giao thức, cho phép khách hàng sử dụng MCP, A2A hoặc kết hợp cả hai để triển khai mã của họ trên AWS.

Khi các giao thức liên tác nhân và các khuôn khổ xung quanh chúng phát triển, nhiều khả năng chúng sẽ trở nên giống như TCP & UDP, nơi hầu hết các nhà phát triển tập trung nhiều hơn vào việc xây dựng các tác nhân của họ thay vì các giao thức nền tảng. Bước đầu tiên hướng tới điều đó là các khuôn khổ tác nhân hỗ trợ các giao thức và xây dựng hệ sinh thái xung quanh chúng. Tại AWS, chúng tôi đã thực hiện bước đầu tiên này bằng cách tham gia cộng đồng tiêu chuẩn A2A và bổ sung hỗ trợ cho A2A trong SDK Strands Agents nguồn mở của mình. Swami Sivasubramanian, Phó Chủ tịch AWS Agentic AI, tóm tắt nỗ lực này:

Tại AWS, chúng tôi tin rằng AI agentic sẽ đóng vai trò quan trọng đối với hầu hết mọi trải nghiệm của khách hàng. Chúng tôi hoan nghênh A2A tham gia Quỹ Linux và kỳ vọng điều này sẽ tạo ra nhiều cơ hội hơn cho bất kỳ ai xây dựng ứng dụng AI. Chúng tôi dự định hỗ trợ cộng đồng bằng các đóng góp dự án và tiếp cận bộ khung, giao thức và dịch vụ agentic rộng lớn và chuyên sâu nhất.

Tương tự như cách chúng tôi đang hỗ trợ phát triển MCP, chúng tôi cũng đang hỗ trợ phát triển A2A để đáp ứng nhu cầu của khách hàng. Chúng tôi dự định sẽ tập trung vào một số lĩnh vực để A2A hoạt động hiệu quả trên AWS, bao gồm hỗ trợ Amazon Bedrock AgentCore, mở rộng giao thức A2A cho lưu trữ tác vụ tạm thời và SigV4, cải thiện quản lý đa tác vụ và cải tiến Java A2A SDK.


## Tổng quan về A2A
Giao thức A2A giải quyết một thách thức quan trọng trong bối cảnh AI. Nó cho phép các tác nhân AI được xây dựng trên các nền tảng đa dạng, được vận hành bởi các công ty khác nhau trên các máy chủ riêng biệt, giao tiếp và cộng tác hiệu quả — với tư cách là tác nhân, chứ không chỉ là công cụ. A2A đại diện cho một bước tiến đáng kể trong việc tạo ra các hệ thống AI có khả năng tương tác, hoạt động cùng nhau xuyên biên giới tổ chức. Giao thức này được hỗ trợ bởi một hệ sinh thái đối tác đang phát triển, bao gồm hơn 50 công ty công nghệ như Google, Atlassian, Confluent, Salesforce, SAP và MongoDB.

Trước A2A, các tổ chức phải đối mặt với những thách thức đáng kể trong việc triển khai các hệ thống AI đa tác tử ở quy mô lớn. Nếu không có giao thức chuẩn hóa, mỗi cặp tác tử đều yêu cầu mã tích hợp tùy chỉnh, dẫn đến chi phí phát triển quá mức và độ phức tạp trong bảo trì. Điều này tạo ra các hệ thống AI bị cô lập, nơi các tác tử chuyên biệt không thể dễ dàng chia sẻ năng lực hoặc phối hợp thực hiện các nhiệm vụ phức tạp. Giao thức này cung cấp cho các tác tử một ngôn ngữ chung, cho phép chúng duy trì tính tự chủ và các kỹ năng chuyên biệt trong khi hợp tác - các tác tử giao tiếp với nhau như những người ngang hàng, chứ không chỉ là những công cụ đơn thuần. Sự khác biệt này rất quan trọng vì nó cho phép các tác tử tham gia vào các tương tác qua lại phức tạp, đàm phán các yêu cầu nhiệm vụ và duy trì khả năng ra quyết định độc lập trong khi hướng tới các mục tiêu chung.

Đối với khách hàng AWS, A2A cung cấp một số tính năng hấp dẫn phù hợp với yêu cầu của doanh nghiệp. Giao thức này cho phép các khả năng của doanh nghiệp bao gồm phát hiện tác nhân an toàn thông qua thẻ tác nhân được chuẩn hóa, cơ chế xác thực và ủy quyền cho quyền truy cập được kiểm soát, hỗ trợ nhiều phương thức giao tiếp (văn bản, biểu mẫu, phương tiện) và khả năng cho phép các tác nhân cộng tác trong các tác vụ dài hạn mà không tiết lộ trạng thái nội bộ hoặc chi tiết triển khai của họ.

A2A giải quyết những thách thức độc đáo của cộng tác đa tác nhân thông qua các tính năng cho phép quy trình làm việc phức tạp, xử lý các quy trình kinh doanh thực tế phức tạp với khả năng quan sát và kiểm soát mà môi trường sản xuất yêu cầu. Cụ thể, nó hỗ trợ thẻ tác nhân, tác vụ có cấu trúc, nhiều tùy chọn vận chuyển và các nguyên hàm xác thực/ủy quyền.


## Thẻ đại lý
Giao tiếp đa tác nhân hiệu quả đòi hỏi các tác nhân phải khám phá và hiểu rõ khả năng của nhau. A2A hỗ trợ điều này thông qua Thẻ Tác nhân — các tài liệu siêu dữ liệu nắm bắt ý nghĩa ngữ nghĩa về những gì mỗi tác nhân có thể làm, cách thức hoạt động ưa thích và loại nhiệm vụ mà tác nhân đó giỏi. Thẻ Tác nhân cho phép các tác nhân khác đưa ra quyết định thông minh về thời điểm và cách thức hợp tác. Thẻ Tác nhân cũng mô tả các yêu cầu xác thực/ủy quyền của một tác nhân và hỗ trợ các khả năng được mở rộng dần dần sau khi xác thực, sử dụng Thẻ Tác nhân Mở rộng Đã Xác thực.

## Thực hiện nhiệm vụ có cấu trúc
Các tác nhân làm việc cùng nhau để giải quyết vấn đề bằng cách tận dụng các tác vụ để cấu trúc giao tiếp; họ sắp xếp thông điệp của mình thành các đơn vị công việc thông minh, mang ngữ cảnh, theo dõi tiến độ và lưu trữ các hiện vật đầu ra. Thông qua các tác vụ, các tác nhân có thể tham chiếu các hiện vật đã tạo trước đó, hiểu được sự phụ thuộc giữa các tác vụ trong quy trình làm việc và đưa ra quyết định sáng suốt dựa trên toàn bộ lịch sử hội thoại. Các tác vụ hỗ trợ cả thực thi tuần tự và song song cho các quy trình làm việc phức tạp. Các tác nhân có thể tạo ra nhiều tác vụ tiếp theo đồng thời và tạo ra các chuỗi hoạt động phụ thuộc. Điều này mang lại cho các nhà phát triển ứng dụng sự linh hoạt để mô hình hóa các quy trình kinh doanh trong thế giới thực.

Bằng cách tận dụng ID tác vụ và ngữ cảnh, các ứng dụng có thể theo dõi nguồn gốc tác vụ, lần theo chuỗi tác vụ đến tận gốc để khôi phục thông tin về cách tạo ra kết quả đầu ra. Điều này cải thiện khả năng quan sát bằng cách cung cấp cho các tác nhân khả năng tạo nhật ký hoạt động phong phú để gỡ lỗi và kiểm tra.

## Nhiều lựa chọn vận chuyển
A2A hỗ trợ các nhà phát triển ứng dụng bằng cách hỗ trợ ba giao thức cốt lõi có khả năng tương đương: JSON-RPC 2.0, gRPC và REST. Điều này cho phép các nhà phát triển lựa chọn phương thức vận chuyển phù hợp nhất với chuyên môn, cơ sở hạ tầng hiện có và yêu cầu hiệu suất của nhóm. Đối với các hoạt động dài hạn, A2A tăng cường mỗi phương thức vận chuyển với Server-Sent Events (SSE) để phát trực tuyến và gửi thông báo đẩy dựa trên webhook. Các nhà phát triển có các tùy chọn trực quan để xử lý cập nhật tác vụ không đồng bộ và giám sát tiến độ theo thời gian thực mà không cần logic thăm dò phức tạp.

## Bảo mật A2A
Bảo mật cấp doanh nghiệp là một yêu cầu không thể thương lượng đối với các hệ thống agent. A2A cho phép kiến ​​trúc bảo mật mạnh mẽ bằng cách hỗ trợ một số giao thức xác thực; bao gồm OAuth 2.0, OpenID Connect và mTLS, cho phép các tổ chức tích hợp agent với cơ sở hạ tầng nhận dạng hiện có của họ, trong khi siêu dữ liệu ủy quyền theo kỹ năng cụ thể và hỗ trợ xác thực thứ cấp cho phép các chính sách kiểm soát truy cập chi tiết có thể được thực thi ở cấp ứng dụng.

Quyết định của A2A trong việc giữ cho các tác nhân không minh bạch với nhau hỗ trợ kiến ​​trúc không tin cậy bằng cách coi mỗi tác nhân là một ranh giới bảo mật độc lập và việc giao thức hỗ trợ kiểm tra tác vụ cung cấp nền tảng cho việc giám sát bảo mật toàn diện và báo cáo tuân thủ.

## Inter-Agent với Strands Agents & A2A
Các tính năng độc đáo của A2A khiến nó trở nên hoàn hảo cho khả năng tương tác giữa các nền tảng tác nhân. Một số nền tảng tác nhân nguồn mở hiện đã hỗ trợ nó. Bộ SDK Strands Agents nguồn mở gần đây đã bổ sung hỗ trợ cho A2A để các tác nhân có thể dễ dàng communicate with other agents.

Strands Agents áp dụng phương pháp tiếp cận dựa trên mô hình để xây dựng và vận hành các tác nhân AI chỉ trong vài dòng mã. Strands mở rộng từ các trường hợp sử dụng tác nhân đơn giản đến phức tạp, và từ phát triển cục bộ đến triển khai trong môi trường sản xuất. Nhiều nhóm tại AWS đã sử dụng Strands cho các tác nhân AI trong môi trường sản xuất, bao gồm Amazon Q Developer, AWS Glue và VPC Reachability Analyzer.

Với hỗ trợ A2A tích hợp sẵn trong Strands Agents, bạn có thể dễ dàng sử dụng một agent như một máy chủ A2A và giao tiếp từ một Agent Strands này đến các agent A2A khác. Để minh họa điều này, hãy xem xét ví dụ về một agent Nhân sự (HR) có thể trả lời các câu hỏi về nhân viên. Để làm điều này, bạn có thể tưởng tượng agent HR giao tiếp với một số agent khác như agent dữ liệu nhân viên, agent Hoạch định Nguồn lực Doanh nghiệp (ERP), agent hiệu suất, agent mục tiêu, v.v. Trong ví dụ này, hãy bắt đầu với một kiến ​​trúc cơ bản, trong đó REST API cung cấp quyền truy cập vào một agent HR kết nối với một agent Thông tin Nhân viên: Kiến trúc của hệ thống liên agent bao gồm hai agent (HR & Employee Info), được kết nối bằng A2A.

Note: The complete, working version of the following example is available in our Agentic AI samples repo.

- Công cụ thông tin nhân viên của chúng tôi sử dụng Amazon Bedrock và công cụ MCP để lấy dữ liệu nhân viên (xem mã đầy đủ cho các khía cạnh đó):
employee_agent = Agent(
    model=bedrock_model,
    name="Employee Agent",
    description="Answers questions about employees",
    tools=tools,
    system_prompt="you must abbreviate employee first names and list all their skills"
)

- Để hiển thị tác nhân này thông qua A2A, chúng ta chỉ cần tạo máy chủ A2A và khởi động nó khi chương trình chạy:
a2a_server = A2AServer(agent=employee_agent, host=urlparse(EMPLOYEE_AGENT_URL).hostname, port=urlparse(EMPLOYEE_AGENT_URL).port)

if __name__ == "__main__":
    a2a_server.serve(host="0.0.0.0", port=8001)

Lưu ý rằng chúng tôi vượt qua EMPLOYEE_AGENT_URL thông qua một biến môi trường. Điều này giúp định nghĩa cơ sở hạ tầng của chúng ta biết URL điểm cuối có thể thiết lập máy chủ và cổng được sử dụng trong thẻ tác nhân A2A (được máy khách A2A sử dụng để khám phá tác nhân).

- Hiện tại, chúng ta có thể truy cập vào tác nhân Thông tin nhân viên thông qua A2A và chúng ta có thể tạo tác nhân HR:
provider = A2AClientToolProvider(known_agent_urls=[EMPLOYEE_AGENT_URL])

agent = Agent(model=bedrock_model, tools=provider.tools)

Tác nhân này giờ đây có thể được gọi theo nhiều cách khác nhau. Trong ví dụ này, chúng tôi gọi nó từ một yêu cầu REST. Xem mã đầy đủ để biết các khía cạnh REST. Sau đây là những gì xảy ra khi yêu cầu REST được thực hiện:
- Người dùng (có thể thông qua ứng dụng web hoặc ứng dụng di động) gửi truy vấn như "liệt kê những nhân viên có kỹ năng liên quan đến AI"
- Nhân viên HR sử dụng mô hình Amazon Nova để hiểu truy vấn của người dùng và quyết định rằng truy vấn đó cần được gửi đến nhân viên thông tin nhân viên.
- Khi sử dụng A2A, truy vấn sẽ được gửi đến tác nhân Thông tin nhân viên.
- Tác nhân Thông tin nhân viên sử dụng mô hình Amazon Nova để hiểu truy vấn và quyết định cần gọi máy chủ MCP Dữ liệu nhân viên.
- Tác nhân Thông tin nhân viên gọi máy chủ MCP Dữ liệu nhân viên để truy vấn cơ sở dữ liệu nhân viên và trả dữ liệu về mô hình Nova.
- Với yêu cầu của hệ thống là viết tắt tên của nhân viên, mô hình sẽ lấy danh sách nhân viên, định dạng danh sách một cách đẹp mắt, viết tắt tên và trả lại văn bản cho tác nhân Thông tin nhân viên.
- Tác nhân Thông tin nhân viên trả lại văn bản cho tác nhân HR, tác nhân này trả lại văn bản trong phản hồi REST.

Tất nhiên, tất cả những điều này đều có thể chạy trên AWS bằng nhiều môi trường thời gian chạy khác nhau (Amazon Elastic Kubernetes Service (Amazon EKS), Amazon Elastic Container Service (Amazon ECS), Amazon Bedrock AgentCore, AWS Lambda, v.v.). Ví dụ này chứa AWS CloudFormation deployment template triển khai các tác nhân và máy chủ MCP trên Amazon ECS (tất cả trong một VPC) và một Bộ cân bằng tải ứng dụng để công khai dịch vụ REST. 

- Chúng ta có thể thử nghiệm với curl:
curl -X POST --location "http://something.us-east-1.elb.amazonaws.com/inquire" \
-H "Content-Type: application/json" \
-d '{"question": "list employees that have skills related to AI programming"}'

Và chúng ta quay lại: Here are the employees with skills related to AI programming:

- A. Rosalez - Machine Learning, REST API
- E. Owusu - DevOps, Machine Learning, Python
- J. Doe- Machine Learning, JavaScript
- K. Mensah - REST API, Kubernetes, Machine Learning, Node.js
- M. Rivera - AWS, Kubernetes, GraphQL, Machine Learning
- M. Major - MongoDB, Angular, Kotlin, Machine Learning, REST API
- C. Salazar - React, Machine Learning, SQL, Kotlin
- N. Wolf - SQL, Machine Learning, Docker, DevOps, Git

If you need more detailed information about any of these employees or require further assistance, please let me know!

Lấy  the complete source cho ví dụ này.

Với Strands Agents, chỉ cần vài dòng mã là có thể hiển thị các agent dưới dạng máy chủ A2A và giao tiếp giữa các agent với nhau bằng A2A. Trong các bài viết tiếp theo, chúng tôi sẽ đề cập đến các dạng agent nâng cao hơn như Swarms, Graphs và Workflows.

## Quan điểm của khách hàng
Chúng tôi đã nhận được phản hồi từ một số khách hàng và đối tác rất hào hứng với dịch vụ hỗ trợ A2A của chúng tôi. Dưới đây là một số chia sẻ của họ:

“Tại Autodesk, chúng tôi cam kết thúc đẩy các tiêu chuẩn mở cho AI đại diện và khả năng tương tác khi chúng tôi định hình tương lai của thiết kế và kỹ thuật. Thông qua sự hợp tác với AWS và cộng đồng A2A, chúng tôi rất hào hứng được góp phần xây dựng một hệ sinh thái nơi các đại diện thông minh có thể giao tiếp liền mạch trên các nền tảng Autodesk. Khi chúng tôi tiếp tục cải tiến Dịch vụ Nền tảng Autodesk với các khả năng AI tạo sinh, chúng tôi nhận thấy tiềm năng to lớn trong cách các đại diện AI có khả năng tương tác có thể chuyển đổi quy trình làm việc trong lĩnh vực kiến ​​trúc, kỹ thuật, xây dựng và sản xuất. Hợp tác cùng AWS, chúng tôi cam kết tạo ra các giải pháp cho phép cộng tác đại diện an toàn và hiệu quả, đồng thời duy trì các tiêu chuẩn cấp doanh nghiệp.” – Ritesh Bansal, Phó Chủ tịch Phân tích Dữ liệu, Thông tin chi tiết và Nền tảng AI/ML, Autodesk

“Cam kết của chúng tôi trong việc phát triển Agentic AI, các giao thức mở và khả năng tương tác là cốt lõi trong tầm nhìn của chúng tôi về các mạng lưới an toàn và thông minh. Bằng cách hợp tác với AWS và cộng đồng A2A, chúng tôi đang thúc đẩy đổi mới để thiết lập các chuẩn mực mới về bảo mật dựa trên AI, cho phép các tổ chức hoạt động với khả năng phục hồi và sự tự tin cao hơn trong kỷ nguyên AI đang phát triển nhanh chóng.” – Raj Chopra, Phó Chủ tịch Cấp cao kiêm Giám đốc Sản phẩm, Bộ phận An ninh, Cisco

“Khi các tổ chức thiết kế các hệ thống AI agentic ngày càng tinh vi, việc phối hợp giữa các agent và công cụ đang trở nên thiết yếu. Chúng tôi rất vui mừng khi thấy AWS thúc đẩy những nỗ lực như A2A, hỗ trợ các kiến ​​trúc tương tác tốt hơn, giúp các tổ chức và khách hàng của Datadog xây dựng các ứng dụng agent-based dễ quan sát, đáng tin cậy và an toàn hơn.” — Yrieix Garnier, Phó Chủ tịch Sản phẩm, Datadog

“MongoDB và AWS cùng cam kết xây dựng một hệ sinh thái mở, có khả năng kết hợp, cho phép các nhà phát triển tự do sáng tạo hơn. Việc áp dụng các tiêu chuẩn mở như A2A là một bước quan trọng hướng tới tầm nhìn này, giúp đơn giản hóa cách các tác nhân tương tác với mô hình tài liệu phong phú của MongoDB, khả năng tìm kiếm vector tích hợp và các mô hình AI Voyage.” – Abhinav Mehla, Phó Chủ tịch Chương trình Đối tác Toàn cầu & Hệ sinh thái, MongoDB

“Khả năng tương tác rất quan trọng để các tác nhân AI hoạt động liền mạch và hiệu quả trên các hệ thống và công cụ doanh nghiệp, đó là lý do tại sao chúng tôi hợp tác với toàn ngành để phát triển tiêu chuẩn A2A, và tại sao chúng tôi sẽ hỗ trợ các tiêu chuẩn mở như A2A và MCP trong Agentforce. Việc AWS hỗ trợ A2A sẽ tiếp tục giúp phá vỡ rào cản giữa các nhà cung cấp, thúc đẩy đổi mới và mang lại giá trị đáng kể cho khách hàng chung của chúng tôi bằng cách cho phép các tác nhân làm việc trên toàn bộ cơ sở hạ tầng và hệ sinh thái công cụ và tác nhân của công ty.” — Gary Lerhaupt, Phó Chủ tịch Kiến trúc Sản phẩm, Salesforce

“Thật phấn khích khi thấy những công ty hàng đầu trong ngành như AWS ủng hộ giao thức Agent2Agent. Khởi đầu là một ý tưởng táo bạo, giờ đây nó đang nhanh chóng trở thành một tiêu chuẩn chung của ngành – một tiêu chuẩn dựa trên tính mở, bảo mật và khả năng cộng tác đa nền tảng. Với sự hỗ trợ từ AWS và các đối tác khác, hệ sinh thái A2A đang thực sự phát triển mạnh mẽ, và ServiceNow tự hào dẫn đầu xu hướng này bằng cách hiện thực hóa các tác nhân AI cấp doanh nghiệp có khả năng tương tác.” – Joe Davis, Phó Chủ tịch Điều hành Nhóm Kỹ thuật Nền tảng & Công nghệ AI tại ServiceNow.

Snowflake tin chắc rằng một số cải tiến lớn nhất trong ngành đến từ các giao thức mở và cộng đồng hỗ trợ chúng. Việc tối đa hóa tiềm năng của AI agentic phụ thuộc vào các giao thức mở như A2A, cũng như kiến ​​thức được chia sẻ và các phương pháp hay nhất mà chúng cung cấp. Chúng tôi rất vui mừng khi thấy AWS thể hiện cam kết của họ đối với các giao thức mở cho khả năng tương tác của agent bằng cách bổ sung hỗ trợ A2A vào Strands Agents. Cùng với sự hỗ trợ của cộng đồng công nghệ rộng lớn hơn, ngành công nghiệp sẽ có thể tự động hóa công việc tri thức với các hệ thống agentic an toàn như Strands Agents và Snowflake Cortex Agents. – Dwarak Rajagopal, Phó Chủ tịch Kỹ thuật & Nghiên cứu AI, Snowflake

“Trong tương lai, một lực lượng lao động phân mảnh gồm con người và các tác nhân AI chắc chắn sẽ cản trở sự phát triển. Chúng tôi tin rằng các giao thức mở, đặc biệt là Giao thức Agent-to-Agent (A2A), đóng vai trò quan trọng trong sự phát triển của lực lượng lao động hỗn hợp này. Chúng cho phép giao tiếp an toàn, hợp tác, đảm bảo khả năng tương tác giữa các hệ sinh thái tác nhân đa dạng. Hệ thống Agent System of Record (ASOR) của Workday mở rộng nền tảng đáng tin cậy của chúng tôi một cách độc đáo để quản lý con người, tài chính và các tác nhân cùng nhau. Hợp tác với AWS và cộng đồng A2A, chúng tôi cam kết thúc đẩy giao tiếp agent an toàn, tương tác. Điều này không chỉ là về công nghệ mới; mà còn là về việc mở khóa một cách an toàn các cấp độ năng suất và đổi mới mới trên toàn doanh nghiệp, đồng thời duy trì khả năng kiểm soát toàn diện.” —Dean Arnold, Phó Chủ tịch Hệ thống Record, Workday

## Bắt đầu và cung cấp phản hồi
Để bắt đầu xây dựng các tác nhân AI tương tác bằng A2A, hãy xem Strands Agents A2A docs. Chúng tôi rất mong nhận được phản hồi của bạn về việc sử dụng A2A với Strands Agents! Hãy tham gia discussions on the open source Strands Agents Python SDK repo để cho chúng tôi biết bạn cần thêm những gì khi xây dựng hệ thống liên tác nhân.

- Nick Aldridge là Kỹ sư Chính tại AWS. Trong 6 năm qua, Nick đã tham gia nhiều sáng kiến ​​AI/ML, bao gồm Amazon Lex và Amazon Bedrock. Gần đây nhất, anh là người lãnh đạo nhóm ra mắt Amazon Bedrock Knowledge Bases. Hiện tại, anh làm việc về AI tạo sinh và cơ sở hạ tầng AI, tập trung vào cộng tác giữa các tác nhân và gọi hàm. Trước khi làm việc tại AWS, Nick đã lấy bằng Thạc sĩ tại Đại học Chicago.

- James Ward is a Principal Developer Advocate at AWS. James travels the world helping enterprise developers learn how to build reliable systems. His current focus is on helping developers build systems of AI agents using Spring AI, Embabel, Strands Agents, Amazon Bedrock, MCP, and A2A.
