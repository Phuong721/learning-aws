---
title: "Simplifying Multi-Tenant Encryption with a Cost-Efficient AWS KMS Key Strategy"
date: 2025-08-21
weight: 2
chapter: false
pre: "<b>Written by:</b> Itay Meller, Ran Isenberg, and Yossi Lagstein"
---

{{% notice info %}}
This article provides guidance on optimizing AWS KMS encryption-key management in multi-tenant SaaS environments, reducing both cost and system complexity.
{{% /notice %}}

## Introduction
Organizations face diverse challenges when it comes to managing encryption keys. While some scenarios require strict separation, there are practical use cases where a centralized approach can streamline operations and reduce complexity. In this post, we focus on Software-as-a-Service (SaaS) providers, but the principles can apply to large enterprises facing similar key-management challenges.

Managing encryption in a multi-tenant, multi-service architecture presents significant complexity. Many organizations struggle with the overhead and cost of provisioning separate AWS Key Management Service (AWS KMS) customer managed keys for each tenant and each service. While secure, this approach often increases operational overhead and KMS usage costs over time.

But what if there were a more efficient way?

In this article, we introduce a strategy for using a single customer-managed (symmetric) key per tenant across your services. After reading this post, you will learn:
- How to implement a scalable, secure, and cost-efficient encryption model  
- Techniques for sharing a single customer-managed key per tenant across multiple services and environments  
- How to encrypt tenant data stored in Amazon DynamoDB and other storage types while maintaining strong tenant isolation  

---

## Multi-Tenant Encryption Requirements in SaaS
Data isolation is a foundational requirement in SaaS multi-tenant architectures, supporting compliance and customer trust. Many SaaS providers must encrypt sensitive information—such as API keys, credentials, and personal data—in storage solutions like DynamoDB and Amazon Simple Storage Service (Amazon S3).

Although these services provide default encryption at rest, they often use a single shared key across many data records. Consider DynamoDB in a shared-pool model, where a single table stores data for multiple tenants. In this setup, tenant data is encrypted using the same AWS KMS key regardless of ownership.

A KMS key represents a top-level key container uniquely identified in AWS KMS. For more details about the hierarchy of keys involved when encrypting or decrypting data, see the AWS KMS key hierarchy.

This shared-key approach is often insufficient for SaaS providers operating under strict security or compliance frameworks. Some customers require:
- **Bring Your Own Key (BYOK)**  
- **Logical data isolation via dedicated encryption keys**

To meet these demands, a provider may create dedicated AWS KMS customer managed keys for each customer, ensuring their sensitive data remains isolated and inaccessible to other tenants.

Providers may also consider a silo model—separate tables per customer. However, that approach introduces challenges: as the customer base grows, managing numerous tables becomes increasingly complex, and AWS service quotas can become limiting.

---

## Scaling Concerns: Managing KMS Keys at Large Scale
As a SaaS platform grows, empowering service teams to develop independently is crucial. A common scaling pattern is enabling each team to build services in dedicated AWS accounts. This often leads to a decentralized model where each service manages its own KMS keys per customer.

However, this autonomy introduces hidden costs as both your customer base and service catalog expand.

### The Challenge of Key Proliferation
As the organization grows, the number of keys increases with each new tenant and service. This results in several challenges:
- **Cost impact:** Each AWS KMS key costs $1 per month, up to $3 per month with two or more key rotations.  
- **Operational complexity:** Managing many KMS keys across environments and accounts becomes error-prone and hard to scale.  
- **Organizational inefficiency:** Duplicate engineering efforts as teams build and maintain similar key-management logic.  
- **Governance cost:** Enforcing consistent policies and tracking KMS usage across multiple AWS accounts becomes difficult.  

---

## A Streamlined Approach
The solution lies in adopting a **centralized key-management strategy**—one KMS key per tenant, stored in a central AWS account. This approach effectively addresses cost, operational, and governance challenges while maintaining strong security guarantees.

In the following sections, we'll explore how to implement this centralized model and securely share KMS keys across services and AWS accounts.

---

## Solution Overview: Centralized Tenant Key Management
At the core of the solution is a centralized Tenant Key Management Service (shown as Service A in the illustration). This service manages the entire life cycle of tenant KMS keys—from creation during tenant onboarding to alias management, access policies, and deletion.

The service enables safe, scalable cross-organization use of keys through cross-account AWS Identity and Access Management (IAM) access. It grants other services (such as a customer-facing service in Account B) permissions to perform specific encryption operations using the tenant's KMS key via role delegation. The design follows AWS best practices for cross-account IAM access using AWS Security Token Service (AWS STS), as described in AWS documentation and related blog posts.

---

## Centralized Key Management in Practice: Encrypting Customer Data
Let’s examine how this works in practice with a common scenario:

- **Service A**: The centralized tenant key-management service in Account A  
- **Service B**: A customer-facing workload running in Account B  

When a customer interacts with Service B, sensitive information—such as secrets, API keys, or license information—must be stored securely in a DynamoDB table. Instead of relying on a shared KMS key or default encryption, Service B encrypts data using the customer's dedicated KMS key managed by Service A.

This process uses cross-account IAM role delegation. Service B temporarily assumes a role (ServiceARole) in Account A, gaining scoped permissions for the specific tenant’s KMS key. Using these temporary credentials, Service B can perform client-side encryption using AWS SDK or AWS Encryption SDK.

---

## Solution Walkthrough
Assumptions and definitions:
- Incoming requests include an authentication header with a JWT containing the tenant identifier (<tenant-id>).  
- **Account A**: Centralized key-management service  
- **Account B**: Customer-facing service  
- **alias/customer-<tenant-id>**: The alias format in Account A, mapped to each tenant's KMS key  
- **ServiceARole**: A role in Account A allowed to encrypt and decrypt using tenant-key aliases  
- **ServiceBRole**: A role in Account B that may assume ServiceARole  

Let’s walk through the flow:

---

## Using the Service with JWT
A tenant-associated customer logs into the SaaS application and receives a JWT containing their tenant ID. The customer performs an action in Service B and sends sensitive data.

Service B processes the request, verifies the JWT, and must:
- Encrypt the customer's sensitive data  
- Store the encrypted value along with other data in DynamoDB  

---

## Assuming the Role
The Lambda execution role in Service B assumes ServiceARole in Account A. An alternative cross-account access method is KMS grants.

Example IAM policy for ServiceARole, allowing encryption/decryption based only on alias/customer-*:

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

To securely encrypt tenant secrets at scale, we grant application roles cross-account access to the KMS key—but only through their alias, which maps to the tenant identifier contained in their JWT authentication token, enforcing strong isolation.

You can control access to the KMS key based on the aliases associated with each KMS key. To do this, use the kms:RequestAlias ​​and kms:ResourceAliases conditional keys as specified in Use aliases to control access to KMS keys.

Additionally, the ServiceARole trust policy allows ServiceBRole in account B to assume:
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

Depending on your environment, you can add additional conditions to this trust policy to further narrow the scope of who can assume this role. For more information, see IAM and AWS STS condition context keys.

Each customer-managed KMS key will then have the following policy. For example, a KMS key for a customer with <tenant-id>: 123 will have a policy that restricts access to the key using a specific customer alias and only through ServiceRoleA.
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

Here is a Python code example that illustrates how Service B automatically assumes a role in Account A to encrypt data for a specific tenant using a session-scoped IAM policy that only allows access to that tenant's KMS key alias.

This pattern follows the same principles outlined in Isolating SaaS Tenants with Dynamically Generated IAM Policies. The idea is to create and attach a tenant-specific IAM policy at runtime that grants the minimum permissions required to operate on tenant-owned resources—in this case, a KMS key alias. The credentials will allow the Lambda function to only use the KMS key that belongs to the customer (identified by tenant_id).

We'll call assume_role_for_tenant for every tenant.

Status of "StringEquals" - "kms:RequestAlias": alias is the magic formula of AWS STS, it restricts ServiceB from using the current tenant's alias in its encrypted SDK calls and relies on alias authorization

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

## Encrypt data and store it in DynamoDB
Now, all that's left to do is use the assumed role credentials and use the AWS SDK to encrypt sensitive customer data and store it in a DynamoDB table.

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


This article is not about isolation between different services, only isolation between tenants. If you need such service isolation, you can use an encryption context, an optional set of non-secret key/value pairs that can contain additional contextual information about the data, such as a service identifier. This helps ensure that services can only encrypt or decrypt data using their respective service encryption context.

## Benefits of Centralized Key Management
Let's see how this solution addresses our previous challenges.

# Tenant Isolation Design
While reducing the total number of KMS keys, we still maintain strict tenant isolation. Each customer's sensitive data is still encrypted with a dedicated key, identified by a unique alias (alias/customer-<tenant-id>). Access control to the tenant key is tightly managed through IAM role delegation, following the principles of least privilege:

- Service A has exclusive control over the tenant's KMS key management.

- Service B can only assume the role of granting restricted encryption, decryption, and GenerateDataKey access to the customer-managed key specified by the alias: alias/customer-<tenant-id>.

## Optimized Cost Management
Our approach significantly reduces costs by moving from multiple service-specific KMS keys per tenant to a single KMS key per tenant, securely shared across multiple services and environments. This approach introduces a new centralized account (Account A) that provides access to encryption keys in appropriate circumstances. It is important to understand AWS STS limits, specific to calls, and consider mechanisms for storing temporary IAM credentials if those limits become a bottleneck. Additionally, if KMS limits are a bottleneck, consider using data key caching using the AWS Encryption SDK.

## Streamlined Operations and Governance
By centralizing key management in Service A, you can achieve:
- Consistent KMS key lifecycle management across the organization
- Improved auditability by using AWS CloudTrail to better understand key access patterns by service
- Reduced operational costs
- Simplified compliance monitoring

The only additional complexity is setting up initial cross-account role delegation between Service A and other services. Once established, this framework can be extended to accommodate new subscribers and services.

It is best to encapsulate the logic for role assignment, policy generation, and AWS SDK client initialization in a common SDK for the entire organization. This abstraction reduces the cognitive load on developers and minimizes the risk of misconfiguration. You can go further by providing high-level utility functions like encrypt_tenant_data() and decrypt_tenant_data(), which hide the underlying complexity while promoting secure and consistent usage patterns across the team.

## Conclusion
In this article, we explored an effective approach to managing encryption keys in multi-tenant SaaS environments through centralization. We looked at common challenges faced by growing SaaS providers, including key proliferation, rising costs, and operational complexity across multiple AWS accounts and services. This centralized key management solution uses AWS best practices for IAM role delegation and cross-account access, allowing organizations to maintain security and compliance while minimizing operational costs. By implementing this approach, SaaS providers or large organizations facing similar challenges can effectively manage their encryption infrastructure as they scale, without compromising security or increasing complexity.

## About the Authors
- Itay Meller is a Security Specialist Solutions Architect at AWS, with a strong background in cybersecurity R&D and leadership roles at multiple security-focused companies. With extensive expertise in cloud security, Itay helps organizations securely adopt and scale AWS environments by solving complex security and compliance challenges.

- Ran Isenberg is an AWS Serverless Hero, Principal Software Architect at CyberArk, blogger and speaker. He maintains the blog RanTheBuilder.cloud, where he shares his knowledge and experience in the Serverless world.

- Yossi Lagstein is a Senior Solutions Architect at Amazon Web Services. Yossi has over 30 years of experience as an expert and manager developing infrastructure components for a variety of projects and products. Yossi helps AWS customers develop, design, and build well-architected solutions. Outside of work, Yossi enjoys running, swimming, and hiking.