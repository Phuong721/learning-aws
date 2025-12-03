---
title: "Đơn giản hóa mã hóa đa thuê bao với chiến lược khóa AWS KMS tiết kiệm chi phí"
date: 2025-08-21
weight: 2
chapter: false
pre: "<b>Bài viết bởi:</b> Itay Meller, Ran Isenberg, và Yossi Lagstein"
---

{{% notice info %}}
Bài viết này hướng dẫn cách tối ưu hoá quản lý khóa mã hóa AWS KMS trong môi trường SaaS đa thuê bao, giảm chi phí và độ phức tạp hệ thống.
{{% /notice %}}

## Giới thiệu
Các tổ chức phải đối mặt diverse challenges when it comes to managing encryption keys. Mặc dù một số kịch bản yêu cầu sự tách biệt nghiêm ngặt, nhưng có những trường hợp sử dụng thiết thực mà phương pháp tập trung có thể hợp lý hóa hoạt động và giảm độ phức tạp. Trong bài viết này, chúng tôi tập trung vào kịch bản nhà cung cấp phần mềm dưới dạng dịch vụ (SaaS), nhưng các nguyên tắc chúng tôi thảo luận có thể được áp dụng bởi các tổ chức lớn đang đối mặt với những thách thức quản lý quan trọng tương tự.

Việc quản lý mã hóa trên một kiến ​​trúc đa thuê bao, đa dịch vụ đặt ra một thách thức đáng kể. Nhiều tổ chức đang phải vật lộn với sự phức tạp và chi phí liên quan đến việc cung cấp các dịch vụ riêng biệt AWS Key Management Service (AWS KMS) customer managed keys cho từng đối tượng thuê bao và dịch vụ. Cách tiếp cận này, mặc dù an toàn, nhưng thường dẫn đến chi phí vận hành tăng cao và chi phí sử dụng AWS KMS tăng theo thời gian.

Nhưng nếu có cách hiệu quả hơn thì sao?

Trong bài viết này, chúng tôi sẽ giới thiệu một chiến lược sử dụng một khóa duy nhất do khách hàng quản lý (đối xứng) cho mỗi đối tượng thuê trên các dịch vụ. Sau khi đọc hết bài viết này, bạn sẽ tìm hiểu:
- Làm thế nào để triển khai một mô hình mã hóa có khả năng mở rộng, an toàn và tiết kiệm chi phí
- Các kỹ thuật sử dụng một khóa do khách hàng quản lý cho mỗi đối tượng thuê trên nhiều dịch vụ và môi trường
- Phương pháp mã hóa dữ liệu người thuê trong Amazon DynamoDB và các loại lưu trữ khác trong khi vẫn duy trì sự cô lập của người thuê.


---

## Yêu cầu mã hóa đa thuê bao trong SaaS
Việc cô lập dữ liệu là nền tảng cơ bản của các kiến ​​trúc SaaS đa thuê bao, đáp ứng cả yêu cầu tuân thủ và sự tin tưởng của khách hàng. Nhiều nhà cung cấp SaaS cần mã hóa thông tin nhạy cảm - từ khóa API và thông tin đăng nhập đến dữ liệu cá nhân - trên các giải pháp lưu trữ như DynamoDB và Amazon Simple Storage Service (Amazon S3).

Mặc dù các dịch vụ lưu trữ này cung cấp mã hóa mặc định khi lưu trữ, nhưng chúng thường sử dụng một khóa chung duy nhất trên các mục dữ liệu. Hãy xem xét DynamoDB in a shared pool model, trong đó một bảng chứa dữ liệu từ nhiều đối tượng thuê. Trong thiết lập này, dữ liệu đối tượng thuê được mã hóa bằng cùng một AWS KMS Key, bất kể quyền sở hữu.

Khóa KMS đại diện cho một vùng chứa tài liệu khóa cấp cao nhất và được xác định duy nhất trong KMS, để biết thêm thông tin về các khóa khác nhau liên quan khi mã hóa hoặc giải mã dữ liệu bằng KMS, hãy xem AWS KMS key hierarchy.

Phương pháp khóa chia sẻ này thường tỏ ra không đủ hiệu quả đối với các nhà cung cấp SaaS hoạt động theo khuôn khổ bảo mật và tuân thủ nghiêm ngặt. Một số khách hàng yêu cầu
- Khả năng mang theo chìa khóa riêng (BYOK)
- Cô lập dữ liệu một cách hợp lý thông qua các khóa mã hóa chuyên dụng

Để đáp ứng các yêu cầu này, nhà cung cấp có thể triển khai khóa được quản lý AWS KMS dành riêng cho khách hàng, giúp đảm bảo dữ liệu nhạy cảm của mỗi khách hàng vẫn được tách biệt và không thể truy cập được bởi những người thuê khác.

Ngoài ra, các nhà cung cấp có thể cân nhắc mô hình silo với các bảng riêng biệt cho mỗi khách hàng. Tuy nhiên, cách tiếp cận này cũng đặt ra những thách thức riêng - khi cơ sở khách hàng tăng lên, việc quản lý nhiều bảng riêng lẻ trở nên ngày càng phức tạp và service quota giới hạn có thể trở thành một ràng buộc.

---

## Quản lý tăng trưởng: Quản lý khóa KMS ở quy mô lớn
Khi mở rộng quy mô nền tảng SaaS, việc trao quyền cho các nhóm phát triển dịch vụ một cách độc lập là rất quan trọng. Một cách nhanh chóng để mở rộng quy mô là có each team develop independently using a dedicated account. Điều này thường dẫn đến phương pháp tiếp cận phi tập trung, trong đó mỗi dịch vụ quản lý khóa KMS riêng cho từng khách hàng. Tuy nhiên, tính tự chủ này đi kèm với những chi phí ẩn khi cơ sở khách hàng và danh mục dịch vụ của bạn mở rộng.

## Thách thức của sự phổ biến chìa khóa
Khi công ty phát triển, số lượng khóa sẽ tăng lên theo mỗi khách hàng và dịch vụ mới được bổ sung. Sự gia tăng này tạo ra một số thách thức cho tổ chức:
- Tác động về chi phí: Một khóa AWS KMS có giá 1 đô la mỗi tháng, tăng lên tối đa 3 đô la mỗi tháng với hai hoặc nhiều lần luân chuyển khóa.
- Độ phức tạp trong vận hành: Việc quản lý nhiều khóa KMS trên nhiều môi trường và tài khoản dễ xảy ra lỗi và khó mở rộng quy mô.
- Lãng phí tổ chức: Nỗ lực trùng lặp giữa các nhóm vì mỗi nhóm phát triển và duy trì mã riêng để quản lý vòng đời khóa khách hàng.
- Chi phí quản lý: Việc thực thi các chính sách nhất quán hoặc theo dõi việc sử dụng khóa KMS trên nhiều tài khoản AWS trở nên khó khăn.

## Một cách tiếp cận hợp lý
Giải pháp nằm ở việc thực hiện một centralized key management strategy. Một khóa KMS cho mỗi đối tượng thuê, được lưu trữ trong một tài khoản AWS trung tâm. Phương pháp này giải quyết hiệu quả các thách thức về chi phí, vận hành và quản trị, đồng thời vẫn đảm bảo tính bảo mật.

Trong các phần sau, chúng tôi sẽ khám phá cách triển khai phương pháp tập trung này và chia sẻ khóa KMS một cách an toàn trên nhiều dịch vụ và tài khoản AWS khác nhau.


## Tổng quan về giải pháp: Tập trung quản lý khóa đối tượng thuê
Cốt lõi của giải pháp của chúng tôi là dịch vụ quản lý khóa thuê bao tập trung (được hiển thị là Dịch vụ A trong hình sau). Dịch vụ này xử lý mọi khía cạnh của vòng đời khóa KMS của khách hàng—từ việc tạo khóa trong quá trình đăng ký thuê bao đến việc quản lý bí danh, chính sách truy cập và xóa khóa.

Dịch vụ này đạt được khả năng sử dụng khóa an toàn, có thể mở rộng trên toàn tổ chức thông qua quyền truy cập AWS Identity and Access Management (IAM) liên tài khoản. Nó cấp cho các dịch vụ khác (ví dụ: dịch vụ dành cho khách hàng trong Tài khoản B trong hình sau) quyền thực hiện các hoạt động mã hóa cụ thể bằng khóa KMS dành riêng cho đối tượng thuê thông qua phân quyền vai trò. Việc triển khai này tuân thủ các thông lệ tốt nhất của AWS về truy cập liên tài khoản, sử dụng IAM và AWS Security Token Service (AWS STS) giả định vai trò như được mô tả trong the AWS documentation và điều này blog post.


## Quản lý khóa tập trung trong thực tế: Mã hóa dữ liệu khách hàng
Chúng ta hãy cùng xem xét cách thức hoạt động này trong thực tế với một kịch bản phổ biến:
- Dịch vụ A: Dịch vụ quản lý khóa thuê tập trung của chúng tôi trong Tài khoản A
- Dịch vụ B: Khối lượng công việc hướng tới khách hàng đang chạy trong Tài khoản B

Khi khách hàng tương tác với Dịch vụ B, họ cần lưu trữ thông tin nhạy cảm một cách an toàn, cho dù đó là bí mật, khóa API hay thông tin giấy phép trong bảng DynamoDB. Thay vì dựa vào khóa KMS dùng chung hoặc mã hóa mặc định, Dịch vụ B mã hóa dữ liệu bằng khóa KMS chuyên dụng của khách hàng do Dịch vụ A quản lý. Quy trình này hoạt động thông qua AWS Identity and Access Management (IAM) ủy quyền vai trò. Dịch vụ B tạm thời đảm nhận một vai trò (ServiceARole) trong Tài khoản A, nhận được các quyền chi tiết, được thu hẹp phạm vi cho khóa KMS của đối tượng thuê cụ thể. Với các thông tin xác thực tạm thời này, Dịch vụ B có thể thực hiện các hoạt động mã hóa phía máy khách trên thông tin nhạy cảm bằng AWS SDK hoặc AWS Encryption SDK.

Trong bài đăng trên blog này, chúng tôi đã sử dụng Boto3. Đối với các trường hợp sử dụng nâng cao hơn yêu cầu data key caching hoặc keyrings, sử dụng AWS Encryption SDK.


## Hướng dẫn giải pháp
Hãy cùng mở rộng các khía cạnh kỹ thuật của giải pháp được mô tả ở trên. Giả định và định nghĩa:
- Các yêu cầu đến bao gồm một tiêu đề xác thực với JSON Web Token (JWT) bao gồm dữ liệu xác định người thuê OF hiện tại. Các mã thông báo này được ký bởi nhà cung cấp danh tính, đảm bảo JWT không thể bị sửa đổi và danh tính người thuê có thể được tin cậy.
- Tài khoản A: Dịch vụ quản lý khóa tập trung.
- Tài khoản B: Dịch vụ kinh doanh phục vụ nhu cầu của khách hàng.
- alias/customer-<tenant-id> là định dạng của các bí danh trong tài khoản A. Mỗi bí danh trỏ đến khóa KMS của khách hàng tương ứng được xác định theo giá trị của <tenant-id> . Dịch vụ A tạo các bí danh này trong quá trình đưa người thuê lên hệ thống và xóa chúng trong quá trình đưa người thuê rời khỏi hệ thống.
- ServiceARole: Một vai trò trong Tài khoản A có thể mã hóa và giải mã khóa KMS có tiền tố bí danh là alias/customer-*. Các quyền được thu hẹp phạm vi hơn nữa bằng cách sử dụng  session policies khi ServiceBRole  giả định ServiceARole.
- ServiceBRole:Một vai trò trong Tài khoản B có thể đảm nhận ServiceARole  trong Tài khoản A để có quyền truy cập vào khóa KMS của khách hàng. Đây sẽ là AWS Lambda vai trò thực thi của hàm.

Lưu ý rằng lớp tính toán của Dịch vụ B trong trường hợp này là một hàm Lambda, nhưng giải pháp này cũng được áp dụng cho các kiến ​​trúc tính toán khác. Hãy cùng xem xét kỹ năng hơn về xử lý luồng:


## Sử dụng dịch vụ với JWT
Khách hàng thuộc về một đối tượng thuê đăng nhập vào giải pháp SaaS và được cấp JWT để xác định đối tượng thuê của mình bằng ID đối tượng thuê (<tenant-id>). Khách hàng thực hiện một hành động trong ServiceB và gửi thông tin nhạy cảm.

ServiceB xử lý yêu cầu (trong hàm Lambda), xác minh mã thông báo JWT và muốn:
- Mã hóa dữ liệu nhạy cảm của khách hàng
- Lưu dữ liệu được mã hóa cùng với dữ liệu khác trong bảng DynamoDB


## Đảm nhận vai trò
Trong ví dụ này, hàm Lambda sử dụng execution role thông tin đăng nhập để đảm nhận vai trò Dịch vụ trong tài khoản Dịch vụ. Một cách khác để cấp quyền truy cập liên tài khoản vào khóa KMS là sử dụng KMS grants,để tìm hiểu thêm, hãy xem Allowing users in other accounts to use a KMS key.

Hãy cùng xem lại chính sách IAM ServiceRoleA:

Cấp quyền mã hóa và giải mã cho khóa KMS bằng cách sử dụng alias/customer-* mẫu.
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowKMSByAlias",
      "Effect": "Allow",
      "Action": [
        "kms:Encrypt",
        "kms:Decrypt",
        "kms:GenerateDataKey*"
      ],
      "Resource": "*",
      "Condition": {
        "StringLike": {
          "kms:RequestAlias": "alias/customer-*"
        }
      }
    }
  ]
}


Để mã hóa bí mật của người thuê một cách an toàn và trên quy mô lớn, chúng tôi cấp cho các vai trò ứng dụng quyền truy cập liên tài khoản vào khóa KMS—nhưng chỉ thông qua bí danh của họ, bí danh này ánh xạ tới mã định danh người thuê có trong mã thông báo xác thực JWT của họ, thực thi sự cô lập mạnh mẽ.

Bạn có thể kiểm soát quyền truy cập vào khóa KMS dựa trên các bí danh được liên kết với mỗi khóa KMS. Để thực hiện việc này, hãy sử dụng kms:RequestAlias và kms:ResourceAliases các phím điều kiện như được chỉ định trong Use aliases to control access to KMS keys.

Ngoài ra, chính sách quan hệ tin cậy của ServiceARole cho phép ServiceBRole trong tài khoản B đảm nhận:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<ACCOUNT_B_ID>:role/ServiceBRole"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}

Tùy thuộc vào môi trường của bạn, bạn có thể thêm các điều kiện bổ sung vào chính sách ủy thác này để thu hẹp hơn nữa phạm vi những người có thể đảm nhận vai trò này. Để biết thêm thông tin, hãy xem IAM and AWS STS condition context keys.

Sau đó, mỗi khóa KMS do khách hàng quản lý sẽ có chính sách sau. Ví dụ: khóa KMS cho khách hàng có <tenant-id>: 123 sẽ có chính sách hạn chế quyền truy cập vào khóa bằng cách sử dụng bí danh khách hàng cụ thể và chỉ thông qua ServiceRoleA.
{
  "Version": "2012-10-17",
  "Id": "TenantKeyPolicy",
  "Statement": [
    {
      "Sid": "AllowServiceARoleViaAlias",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<ACCOUNT_A_ID>:role/ServiceARole"
      },
      "Action": [
        "kms:Encrypt",
        "kms:Decrypt",
        "kms:GenerateDataKey*"
      ],
      "Resource": "*",
      "Condition": {
        "StringLike": {
          "kms:RequestAlias": "alias/customer-123"
        }
      }
    }
  ]
}

Sau đây là ví dụ mã Python minh họa cách Dịch vụ B tự động đảm nhận vai trò trong Tài khoản A để mã hóa dữ liệu cho một đối tượng thuê cụ thể bằng chính sách IAM có phạm vi phiên, chính sách này chỉ cho phép truy cập vào bí danh khóa KMS của đối tượng thuê đó.

Mẫu này tuân theo các nguyên tắc tương tự được nêu trong Isolating SaaS Tenants with Dynamically Generated IAM Policies. Ý tưởng là tạo và đính kèm một chính sách IAM dành riêng cho đối tượng thuê trong thời gian chạy, cấp các quyền tối thiểu cần thiết để vận hành trên các tài nguyên do đối tượng thuê sở hữu—trong trường hợp này là một bí danh khóa KMS. Thông tin xác thực sẽ cho phép hàm Lambda chỉ sử dụng khóa KMS thuộc về khách hàng (được xác định bởi tenant_id).

Chúng tôi sẽ gọi assume_role_for_tenant cho mọi người thuê nhà.

Tình trạng của "StringEquals" - "kms:RequestAlias": alias  là công thức kỳ diệu của AWS STS, nó hạn chế ServiceB sử dụng bí danh của người thuê hiện tại trong các cuộc gọi SDK mã hóa của nó và dựa vào alias authorization

import boto3
def assume_role_for_tenant(tenant_id: str):
    alias = f"alias/customer-{tenant_id}"
    # Session policy scoped to only the specific alias
    session_policy = {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "kms:Encrypt",
                    "kms:Decrypt",
                    "kms:GenerateDataKey*"
                ],
                "Resource": "*",
                "Condition": {
                    "StringEquals": {
                        "kms:RequestAlias": alias
                    }
                }
            }
        ]
    }
    # Assume ServiceARole in Account A with inline session policy
    sts = boto3.client("sts")
    assumed = sts.assume_role(
        RoleArn="arn:aws:iam::<ACCOUNT_A_ID>:role/ServiceARole",
        RoleSessionName=f"Tenant{tenant_id}Session",
        Policy=json.dumps(session_policy)
    )
    return assumed["Credentials"]

## Mã hóa dữ liệu và lưu trong DynamoDB
Bây giờ, việc còn lại cần làm là sử dụng thông tin xác thực vai trò đã được giả định và sử dụng AWS SDK để mã hóa dữ liệu khách hàng nhạy cảm và lưu trữ dữ liệu đó trong bảng DynamoDB.

# Use temporary credentials to create a KMS client
    creds = assume_role_for_tenant(tenant_id, plaintext)
    kms = boto3.client(
        "kms",
        region_name="us-east-1",
        aws_access_key_id=creds["AccessKeyId"],
        aws_secret_access_key=creds["SecretAccessKey"],
        aws_session_token=creds["SessionToken"]
    )
    # Encrypt using the alias
    response = kms.encrypt(
        KeyId= f"alias/customer-{tenant_id}"
        Plaintext=plaintext
    )
    # store response["CiphertextBlob"] in DynamoDB table

Bài viết này không đề cập đến việc cô lập giữa các dịch vụ khác nhau, mà chỉ đề cập đến việc cô lập giữa các đối tượng thuê. Nếu cần cô lập dịch vụ như vậy, bạn có thể sử dụng encryption context, một tập hợp tùy chọn các cặp khóa/giá trị không bí mật có thể chứa thông tin ngữ cảnh bổ sung về dữ liệu, ví dụ như mã định danh dịch vụ. Điều này giúp đảm bảo rằng các dịch vụ chỉ có thể mã hóa hoặc giải mã dữ liệu bằng ngữ cảnh mã hóa dịch vụ tương ứng.


## Lợi ích của quản lý khóa tập trung
Hãy cùng xem giải pháp này giải quyết những thách thức trước đây của chúng ta như thế nào.

## Thiết kế cô lập người thuê nhà
Mặc dù giảm tổng số khóa KMS, chúng tôi vẫn duy trì việc cô lập nghiêm ngặt đối với người thuê. Dữ liệu nhạy cảm của mỗi khách hàng vẫn được mã hóa bằng khóa chuyên dụng, được xác định bằng một bí danh duy nhất (alias/customer-<tenant-id>). Quyền kiểm soát truy cập vào khóa thuê được quản lý chặt chẽ thông qua việc phân quyền vai trò IAM, tuân theo các nguyên tắc đặc quyền tối thiểu:

- Dịch vụ A kiểm soát độc quyền việc quản lý khóa KMS của người thuê.
- Dịch vụ B chỉ có thể đảm nhận vai trò cấp quyền truy cập mã hóa, giải mã và GenerateDataKey bị hạn chế cho khóa do khách hàng quản lý được chỉ định bởi bí danh: alias/customer-<tenant-id>.


## Quản lý chi phí tối ưu
Phương pháp của chúng tôi giúp giảm đáng kể chi phí bằng cách chuyển từ nhiều khóa KMS dành riêng cho từng dịch vụ cho mỗi đối tượng thuê sang một khóa KMS duy nhất cho mỗi đối tượng thuê, được chia sẻ an toàn trên nhiều dịch vụ và môi trường. Cách tiếp cận này giới thiệu một tài khoản tập trung mới (Tài khoản A) cung cấp quyền truy cập vào khóa mã hóa trong những trường hợp phù hợp. Điều quan trọng là phải hiểu AWS STS limits, cụ thể cho  các cuộc gọi và xem xét các cơ chế lưu trữ thông tin xác thực IAM tạm thời nếu những giới hạn đó trở thành nút thắt cổ chai. Ngoài ra, nếu KMS limits là một nút thắt cổ chai, hãy cân nhắc sử dụng data key caching bằng cách sử dụng AWS Encryption SDK.


## Hoạt động và quản trị hợp lý
Bằng cách tập trung quản lý khóa trong Dịch vụ A, bạn có thể đạt được:
- Quản lý vòng đời khóa KMS nhất quán trên toàn tổ chức
- Cải thiện khả năng kiểm toán bằng cách sử dụng  AWS CloudTrail để hiểu rõ hơn về các mẫu truy cập chính theo dịch vụ
- Giảm chi phí hoạt động
- Giám sát tuân thủ đơn giản hóa

Sự phức tạp bổ sung duy nhất là việc thiết lập phân quyền vai trò liên tài khoản ban đầu giữa Dịch vụ A và các dịch vụ khác. Sau khi được thiết lập, khuôn khổ này có thể được mở rộng để đáp ứng các đối tượng thuê bao và dịch vụ mới.

Tốt nhất là đóng gói logic đảm nhiệm vai trò, tạo chính sách và khởi tạo máy khách AWS SDK trong một SDK dùng chung cho toàn tổ chức. Sự trừu tượng hóa này giúp giảm tải nhận thức cho các nhà phát triển và giảm thiểu rủi ro cấu hình sai. Bạn có thể tiến xa hơn bằng cách cung cấp các hàm tiện ích cấp cao như encrypt_tenant_data() và  decrypt_tenant_data(), ẩn đi sự phức tạp tiềm ẩn trong khi thúc đẩy các mô hình sử dụng an toàn và nhất quán trong toàn nhóm.


## Phần kết luận
Trong bài viết này, chúng tôi đã khám phá một phương pháp hiệu quả để quản lý khóa mã hóa trong môi trường SaaS đa thuê bao thông qua tập trung hóa. Chúng tôi đã xem xét những thách thức phổ biến mà các nhà cung cấp SaaS đang phát triển phải đối mặt, bao gồm sự gia tăng khóa, chi phí tăng cao và tính phức tạp trong vận hành trên nhiều tài khoản và dịch vụ AWS. Giải pháp tập trung hóa quản lý khóa này sử dụng các phương pháp hay nhất của AWS để phân quyền vai trò IAM và truy cập liên tài khoản, cho phép các tổ chức duy trì bảo mật và tuân thủ đồng thời giảm thiểu chi phí vận hành. Bằng cách triển khai phương pháp này, các nhà cung cấp SaaS hoặc các tổ chức lớn đang gặp phải những thách thức tương tự có thể quản lý hiệu quả cơ sở hạ tầng mã hóa của họ khi mở rộng quy mô, mà không ảnh hưởng đến bảo mật hoặc tăng tính phức tạp.


## Về các tác giả
- Itay Meller là Kiến trúc sư Giải pháp Chuyên gia Bảo mật tại AWS, với nền tảng vững chắc về Nghiên cứu & Phát triển an ninh mạng và vai trò lãnh đạo tại nhiều công ty tập trung vào bảo mật. Với chuyên môn sâu rộng về bảo mật đám mây, Itay giúp các tổ chức áp dụng và mở rộng môi trường AWS một cách an toàn bằng cách giải quyết các thách thức phức tạp về bảo mật và tuân thủ.

- Ran Isenberg là một Anh hùng Không máy chủ của AWS, Kiến trúc sư Phần mềm Chính tại CyberArk, một blogger và diễn giả. Anh duy trì blog RanTheBuilder.cloud, nơi anh chia sẻ kiến ​​thức và kinh nghiệm trong thế giới Không máy chủ.

- Yossi Lagstein là Kiến trúc sư Giải pháp Cấp cao tại Amazon Web Services. Yossi có hơn 30 năm kinh nghiệm trong vai trò chuyên gia và quản lý phát triển các thành phần cơ sở hạ tầng cho nhiều dự án và sản phẩm. Yossi hỗ trợ khách hàng AWS phát triển, thiết kế và xây dựng các giải pháp được kiến ​​trúc tốt. Ngoài giờ làm việc, Yossi thích chạy bộ, bơi lội và đi bộ đường dài.
