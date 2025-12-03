---
title: "Worklog Week 8"
date: 2025-10-27
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it verbatim** for your official internship report.
{{% /notice %}}


### Week 9 Objectives:

* Understand the architectural requirements for the project.
* Become proficient with draw.io to design system diagrams.
* Understand the relationships between AWS services in the architecture: Networking, Compute, Database, CI/CD, Monitoring.
* Complete the **Network Architecture Diagram** and submit it for mentor review.


### Tasks for this week:
| Day | Task | Start Date | Completion Date | Reference |
| --- | ----- | ------------ | ---------------- | ---------- |
| 2 | - Gather architectural requirements from mentors <br> - Define the scope of the diagram (VPC, subnets, routing, frontend, backend, database, CI/CD…) | 2025-10-27 | 2025-10-27 | FCJ Internal |
| 3 | - Start designing the network architecture diagram in draw.io <br> - Create VPC, public/private subnets, Internet Gateway <br> - Add Route 53, CloudFront, S3 FE bucket | 2025-10-28 | 2025-10-28 | AWS Docs |
| 4 | - Add API Gateway, EC2, Security Groups <br> - Design RDS in private subnet <br> - Draw the data flow: FE → CloudFront → API → EC2 → RDS | 2025-10-29 | 2025-10-29 | AWS Architecture Icons |
| 5 | - Integrate CI/CD pipeline (CodePipeline, CodeBuild, CloudFormation) <br> - Add Cognito/Auth and complete the Security Layer | 2025-10-30 | 2025-10-30 | aws.amazon.com |
| 6 | - Optimize diagram layout, adjust colors and borders <br> - Add numbering for request flows <br> - Export the diagram and send it to mentors for review | 2025-10-31 | 2025-10-31 | FCJ Internal |
| 7 | - Receive mentor feedback: update subnets, API flow, security layers <br> - Revise the diagram according to suggestions | 2025-11-01 | 2025-11-01 | Direct discussion |
| Sun | - Summarize lessons learned during the architecture design process <br> - Finalize weekly Worklog | 2025-11-02 | 2025-11-02 |  |


### Week 9 Achievements:

* Completed a full **AWS Network Architecture Diagram** including:
  * Route 53, CloudFront, S3 frontend bucket.
  * API Gateway → EC2 backend.
  * NAT Gateway + Internet Gateway.
  * RDS in private subnet.
  * CI/CD: CodePipeline, CodeBuild, CloudFormation.
  * Monitoring & Security: CloudWatch, CloudTrail, IAM, Secrets Manager, SNS.

* Clearly understood how the components interact:
  * User request flow for FE/BE.
  * Separation of public and private subnets.
  * NAT mechanism for EC2 to access the internet securely.
  * API Gateway → EC2 → RDS data flow.

* Learned how to standardize technical diagrams following AWS best practices:
  * Use of correct AWS icons and proper service grouping.
  * Layered architecture and numbered processing flows.

* Finalized the architecture diagram for reporting and mentor evaluation.
