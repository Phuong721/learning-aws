---
title: "Accelerate Your Cloud Strategy with Megaport’s 25 Gbps Hosted AWS Direct Connect"
date: 2025-08-21
weight: 1
chapter: false
pre: "<b>Article by:</b> Mokshith Kumar and Miranda Li"
---

{{% notice info %}}
This article is published in collaboration with Chris Cabel, Senior Director, Global Cloud Solutions at Megaport.
{{% /notice %}}

As businesses move critical workloads to the cloud, network performance has become a fundamental business requirement. Amazon Web Services (AWS) Direct Connect provides a dedicated network connection between on-premises data centers and AWS. This bypasses the public internet to deliver more stable and reliable network performance with lower latency. The introduction of **25 Gbps hosted connections** fills the gap between 10 Gbps options (often insufficient) and 100 Gbps options (often excessive), allowing organizations to right-size their connections without sacrificing performance. Megaport, a leading Network-as-a-Service (NaaS) provider and AWS Marketplace Partner, is among the first to offer this 25 Gbps connection across multiple Direct Connect Edge Locations through its Global Software-Defined Network, spanning hundreds of data centers worldwide. For the latest information, please refer to the Megaport public network footprint page.

Using Megaport’s self-service platform, organizations can provision, scale, and manage high-performance AWS connections in minutes rather than weeks or months. In this article, we describe how the powerful combination of AWS and Megaport services enables cloud architects and IT leaders to build next-generation hybrid networks that support data-intensive applications, enhance security, and optimize costs—while maintaining the flexibility to adapt to evolving business needs.

---

## Prerequisites

We assume you are familiar with core networking structures on AWS, particularly Direct Connect. While we won’t dive deeply into definitions, we will highlight its role in supporting hybrid connection architectures involving hosted Direct Connect connections. If you are not familiar with these concepts, we recommend reviewing the Direct Connect documentation for more details on choosing between Direct Connect dedicated and hosted connections.

For foundational knowledge, the **Getting Started with AWS Direct Connect** guide is also a helpful resource.

---

## Key Use Cases for 25 Gbps Direct Connect

The following sections outline key use cases for Direct Connect 25 Gbps.

### 1. Cloud Migration
Large-scale enterprise data migrations involve transferring massive datasets. A 25 Gbps hosted connection allows organizations to reduce migration time from days to hours while maintaining stable and secure performance. For example, migrating a 100 TB database, which would take over 22 hours with a 10 Gbps connection, can be completed in approximately 9 hours, significantly shortening time-to-production.

| Connection Speed | Data Volume | Estimated Migration Time | Performance Gain |
|----------------- |------------ |------------------------- |----------------- |
| 10 Gbps          | 100 TB      | ~22 hours                | Baseline         |
| 25 Gbps          | 100 TB      | ~9 hours                 | ~59% faster      |

*Table 1: Bandwidth effects on large-scale data migration*

### 2. Data Transfer
Organizations collecting data from edge locations or on-premises environments benefit from high-throughput, predictable connections for analytics, backup, and storage workloads. Media companies can efficiently transfer large video files between studios and AWS, while healthcare organizations can move imaging datasets to the cloud for AI analysis while maintaining compliance through private connectivity. The 25 Gbps tier is particularly useful for IoT deployments generating high volumes of sensor data, large-scale backups with strict Recovery Point Objective (RPO) requirements, and organizations training ML models with substantial on-premises datasets.

### 3. Hybrid Cloud Support
As hybrid architectures become more prevalent, reliable connectivity between on-premises systems and AWS is essential. Megaport’s 25 Gbps hosted connection provides the capacity needed for distributed databases, hybrid storage solutions, and microservices spanning multiple environments. Organizations can implement consistent security policies and seamless application experiences across their entire technology stack, while maintaining performance headroom for peak workloads and future growth.

### 4. Latency-Sensitive Applications
Applications such as financial trading platforms, automation systems, and real-time collaboration tools require minimal latency. The 25 Gbps dedicated connection maintains stable, low-latency performance by bypassing the public internet while providing sufficient bandwidth to prevent congestion during peak periods. For industries requiring millisecond-level speed—such as high-frequency trading, online gaming, or telehealth—Direct Connect’s predictable performance offers competitive advantages while maintaining security through private connectivity.

Industries benefiting include: high-frequency trading, online gaming, telehealth.

### 5. Cost Control
The 25 Gbps package offers a cost-effective solution to expand network capacity without over-provisioning. Organizations that previously had to choose between insufficient 10 Gbps connections or excessive 100 Gbps connections can now select an optimal balance, often saving 50–60% compared to the 100 Gbps alternative. Megaport’s flexible platform also allows businesses to adjust bandwidth as demands change, supporting cost optimization across the application lifecycle while ensuring required performance for modern cloud workloads.

---

## Benefits of Deploying AWS Direct Connect 25 Gbps with Megaport

The following sections highlight the benefits of deploying Direct Connect 25 Gbps with Megaport.

### 1. Private, Secure Data Transfer
Megaport’s hosted connections provide a private path to AWS, bypassing the public internet, enhancing data privacy, reducing exposure to common security threats, and ensuring compliance for sensitive workloads. Private connectivity is increasingly critical as regulations like GDPR, HIPAA, and industry-specific requirements impose stricter controls on data movement and protection. The 25 Gbps tier delivers this security without compromising the performance needed for modern data-intensive applications.

### 2. Ease of Use
Megaport’s self-service portal enables customers to provision, scale, and manage Direct Connect connections in minutes. This flexibility allows teams to quickly adapt to changing project demands without incurring manual management costs. Organizations can establish connections to AWS Regions almost in real-time, rather than waiting weeks or months for traditional telecom circuits, accelerating cloud initiatives and reducing time-to-value for new projects.

### 3. Global Reach
Megaport’s presence in over 975 data centers across 26+ countries provides near-ubiquitous access to Direct Connect locations. Organizations with distributed footprints can standardize a consistent connection approach across AWS Regions, simplifying architecture and operations while maintaining high performance. This global reach is particularly valuable for multinational businesses operating across time zones or organizations with strict data sovereignty requirements.

### 4. Flexibility and Scalability
As demand increases, customers can flexibly adjust bandwidth via the Megaport portal. This flexibility allows IT teams to scale cost-effectively while maintaining optimal performance for critical workloads. The 25 Gbps tier offers an ideal intermediate solution, deployable as a long-term option or as a stepping stone for a broader cloud network strategy.

---

## Getting Started with AWS and Megaport 25 Gbps

The following sections guide you on how to use AWS and Megaport with a 25 Gbps hosted connection.

### Prerequisites
1. An active Megaport account with billing enabled.  
2. An AWS account with Direct Connect access.

### Step 1: Create a Megaport Cloud Router (MCR)
1. Log in to the Megaport Portal.  
2. Select +Add Service and choose MCR (Megaport Cloud Router) as shown in Figure 1. Ensure the MCR supports at least 25 Gbps capacity, as this determines the maximum speed available for your hosted connection.  
3. Follow the on-screen instructions to complete setup. More details can be found in the Creating MCR Documentation.

### Step 2: Create a Hosted Connection from Megaport to AWS
1. In the Megaport Portal, select your MCR and click + Add Connection.  
2. Choose AWS Direct Connect from the Cloud options.  
3. Provide the necessary information and follow the instructions:  
   - Creating a Hosted Connection  
   - Connection Name: a descriptive name for your connection.  
   - Service Level Reference: provide a unique identifier for billing or tracking purposes.  
   - Rate Limit: set to 25,000 Mbps to provision a 25 Gbps connection.  
4. Submit and deploy the connection.  

You can also create hosted VIFs and other connection types (e.g., public VIF, transit VIF), depending on your use case.  

### Step 3: Accept the Hosted Connection in AWS
1. Log in to the AWS Console and navigate to AWS Direct Connect.  
2. In the navigation pane, select Connections.  
3. Select the hosted connection and choose View details.  
4. Select the confirmation checkbox and click Accept.  

### Step 4: Create a Virtual Interface for the Hosted Connection
1. After accepting the connection, select it and choose Create Virtual Interface as shown in Figure 3.  
2. Choose the interface type – typically Private to access a VPC.  
3. Configure as follows:  
   - Virtual interface name  
   - VLAN ID (must match the VLAN used in Megaport configuration)  
   - BGP ASN (your default or AWS-provided)  
   - BGP peer IP address (AWS provides one side; you specify your side)  
4. Gateway association: select a Virtual Private Gateway or AWS Transit Gateway attached to your VPC.  
5. Click Create.  

### Step 5: Configure BGP on the Megaport MCR
1. Return to the Megaport Portal.  
2. Edit the Virtual Cross Connect (VXC) to match the BGP details provided by AWS.  
3. Enter the required information:  
   - BGP peer IP addresses (yours and AWS’s)  
   - Your ASN (or AWS-assigned ASN)  
4. Save and apply the configuration.  

---

## Conclusion
In this article, we explored how AWS Direct Connect 25 Gbps hosted connections via Megaport can transform your cloud connectivity strategy. We covered key use cases such as large-scale cloud migrations, data-intensive applications, hybrid cloud deployments, and latency-sensitive workloads. You learned how this solution provides private, secure data transfer with flexible scalability, while offering significant cost savings compared to 100 Gbps alternatives. We also provided step-by-step guidance for setting up a 25 Gbps hosted connection using Megaport’s self-service platform.

### Call to Action
- Assess your current and future network throughput requirements.  
- Explore 25 Gbps hosted connection options on the AWS Direct Connect Partners page.  
- Visit Megaport’s AWS solution page to learn more or start self-service provisioning.

---

## About the Authors

**Mokshith Kumar**  
Senior GTM Solutions Architect – Core Networking at AWS, supporting ISVs and FSI in North America.  
- Role: Develop GTM strategy, lead strategic initiatives, drive AWS networking adoption.  
- Interests: Swimming, music.

**Miranda Li**  
Senior Solutions Architect at AWS, specializing in ISVs and cloud-native architecture.  
- 4 years of experience supporting ISV innovation and scaling on AWS.  
- Expertise: IaaS, networking architecture, security, data analytics.  
- Interests: Badminton, running, outdoor activities.
