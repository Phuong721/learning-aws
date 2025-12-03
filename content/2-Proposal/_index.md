---
title: "Proposal"
date: 2025-09-10
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

In this section, you need to summarize the contents of the workshop that you **plan** to conduct.

# Blood Donation Support System
## AWS Solution for Blood Donation Support Software

### 1. Executive Summary
Blood Donation Support System (BDSS)** is a web platform that supports the management and connection of blood donors with medical facilities. The project was developed by a group of students in Ho Chi Minh City to optimize the blood donation process, reduce the burden of searching for donors and improve the efficiency of medical communication.

The system is built on **AWS Cloud architecture**, using **Amazon EC2**, **Amazon RDS**, **API Gateway**, **Cognito** and **CI/CD Pipeline (GitLab + CodePipeline)** for automatic deployment. BDSS supports four user groups (Guest, Member, Staff, Admin), providing features for searching, registering for blood donation, managing blood banks, tracking blood donation processes and visual reporting.

### 2. Problem Statement
### What’s the Problem?
Healthcare facilities currently manage blood donation processes manually or through disparate tools. Finding donors who match blood type or region is difficult, especially in emergency situations. In addition, data storage systems are not synchronized, making it difficult to analyze, report and optimize blood donation campaigns.

### The Solution
Developed a **comprehensive blood donation support platform on AWS Cloud**, with functions for blood donation management, searching for donors and blood needers by blood type or geographic location, integrating user authentication via Amazon Cognito, and data governance on Amazon RDS. The frontend was deployed via **Route 53 + CloudFront**, the backend via **API Gateway – EC2**, a MySQL database on **Amazon RDS**, and an automated CI/CD pipeline using **GitLab – CodePipeline**.

### Benefits and Return on Investment
Reduce the time it takes to find a matching donor by 60–70%. Increase the accuracy of blood type and location information. Optimize operating costs with a flexible, pay-as-you-go cloud architecture. Improve response to blood emergencies

### 3. Solution Architecture
The platform employs a serverless AWS architecture to manage data from 5 Raspberry Pi-based stations, scalable to 15. Data is ingested via AWS IoT Core, stored in an S3 data lake, and processed by AWS Glue Crawlers and ETL jobs to transform and load it into another S3 bucket for analysis. Lambda and API Gateway handle additional processing, while Amplify with Next.js hosts the dashboard, secured by Cognito. The architecture is detailed below:

![Blood Donation Support Software Architecture](/images/2-Proposal/edge_bdss.png)

![Blood Donation Support System Platform Architecture](/images/2-Proposal/platform_bdss.png)

The system is divided into **4 main layers**:

1. *Edge Networking Layer:*
*Route 53* manages domain and DNS routing.
*CloudFront* increases page loading speed and delivers static content.
*AWS WAF* protects against web attacks (SQL injection, DDoS).

2. *Application & Data Layer:*
*Amazon EC2*: Deploys backend API and handles main business.
*Amazon RDS (MySQL)*: Stores blood donor data, blood types, donation history.
*API Gateway*: Communicates between frontend and backend.
*Elastic Load Balancer (ELB)*: Distributes load to EC2 instances.
*NAT Gateway & Internet Gateway*: Supports secure Internet connection.

3. *CI/CD & DevOps Layer:*
*GitLab*: Source code management.
*AWS CodePipeline, CodeBuild*: Deploy and update automatically.

4. *Monitoring & Security Layer:*
*Amazon Cognito*: Authentication and authorization (Guest, Member, Staff, Admin).
*CloudWatch, CloudTrail, IAM, Secrets Manager*: Monitoring, security, system alerts.
*SNS*: Send notifications when there is an event (blood emergency, suitable donor).

### 4. Technical Implementation
*Implementation Phases*
1. *Analysis & Design (January)*
* Gather requirements, define use cases, design ERD and AWS architecture.

2. *Infrastructure & Pipeline Setup (February)*
* Configure Route 53, CloudFront, EC2, RDS and CI/CD on AWS.

3. *Development & Testing (March-April)*
* Build main modules: blood donation registration, search, blood bank management.
* Integrate Cognito and SNS alert system.

4. *Deployment & Operation (May)*
* Deploy the official product and monitor with CloudWatch.

**Yêu cầu kỹ thuật chính:**
*Frontend:* React/Next.js hoặc Angular (deploy qua S3/CloudFront).
*Backend:* Node.js/Express trên EC2, giao tiếp qua REST API Gateway.
*Database:* Amazon RDS MySQL, tối ưu query và backup định kỳ.
*CI/CD:* GitLab → CodeBuild → CodePipeline → EC2.
*Auth:* Cognito (4 vai trò: Guest, Member, Staff, Admin).
*Alert & Logs:* SNS + CloudWatch + CloudTrail.

### 5. Timeline & Milestones
| Timeline | Phase | Key Results |
| ------------- | ---------------------------- | ------------------------------------------------ |
| **Month 1** | Requirements analysis & design | AWS architecture + use case diagram |
| **Month 2** | Infrastructure & pipeline setup | EC2, RDS, API Gateway operational |
| **Month 3–4** | Development & testing | Key modules finalized |
| **Month 5** | Live deployment | System stable, with Dashboard reporting |

### 6. Budget Estimation
| Services | Estimated Cost/Month (USD) | Notes |
| ---------------------------- | ---------------------------- | -------------------- |
| EC2 (t2.micro) | 3.50 | Backend REST API |
| Amazon RDS (MySQL) | 2.80 | 20 GB storage |
| API Gateway | 0.50 | 5,000 requests |
| CloudFront + S3 | 0.80 | Website + CDN |
| Route 53 | 0.50 | Domain & DNS |
| Cognito | 0.10 | <100 users |
| CloudWatch + Logs | 0.30 | Monitoring & Alerting |
| CI/CD (CodePipeline, CodeBuild) | 0.40 | Automated Deployment |
| **Total** | **8.9 USD/month** | ~106.8 USD/year |

> Total costs may vary based on AWS Free Tier or spot instance usage.

### 7. Risk Assessment
| Risk | Impact | Probability | Mitigation |
| -------------------------- | ---------- | ---------- | ----------------------- |
| Internet Outage | Medium | Medium | Redundancy on EC2 Backup |
| DDoS Attack | High | Low | AWS WAF + CloudFront |
| User Data Corruption | High | Low | RDS Backup + IAM Restricted Access |
| Cost Overrun | Medium | Low | AWS Budget Alert |
| CI/CD Deployment Disruption | Low | Medium | Pipeline Testing Before Merging |

### 8. Expected Outcomes
*Technology:* Cloud-native system, automatic CI/CD, multi-user support and high security.
*Application:* Helps medical facilities manage blood donations effectively, minimizing manual processes.
*Expansion:* Can be replicated for many other hospitals, integrating AI to analyze blood group needs or predict upcoming blood donations.

