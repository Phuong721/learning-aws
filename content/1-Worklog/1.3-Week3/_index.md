---
title: "Worklog Week 3"
date: 2025-09-17
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The following information is for reference only. Please **do not copy verbatim** into your official report, including this warning.
{{% /notice %}}


### Goals for Week 3:

* Understand the basics of **AWS storage and security services**.  
* Get familiar with **Amazon S3**, **IAM (Identity and Access Management)**, and **CloudWatch** for system management and monitoring.  

### Tasks to be completed this week:
| Day | Task | Start Date | Completion Date | Reference |
| --- | ---- | ---------- | ---------------- | ---------- |
| 2 | - Introduction to **Amazon S3** <br>&emsp; + Concept and role of S3 <br>&emsp; + Bucket & Object <br>&emsp; + Storage Classes (Standard, IA, Glacier) <br>&emsp; + Basic access control | 15/09/2025 | 15/09/2025 | <https://000048.awsstudygroup.com/> |
| 3 | - **Practice 1:** <br>&emsp; + Create an S3 bucket <br>&emsp; + Upload / Download files <br>&emsp; + Configure access permissions (Public / Private) <br>&emsp; + Test a simple lifecycle policy | 16/09/2025 | 16/09/2025 | <https://000048.awsstudygroup.com/> |
| 4 | - Learning about **IAM**: <br>&emsp; + Users, Groups, Roles <br>&emsp; + Policies and permissions <br>&emsp; + Practice assigning IAM User permissions for S3 | 17/09/2025 | 17/09/2025 | <https://000049.awsstudygroup.com/> |
| 5 | - **Practice 2:** <br>&emsp; + Create IAM User and Group <br>&emsp; + Assign S3 ReadOnly / FullAccess permissions <br>&emsp; + Test login with the new IAM User | 18/09/2025 | 18/09/2025 | <https://000049.awsstudygroup.com/> |
| 6 | - Introduction to **CloudWatch**: <br>&emsp; + CloudWatch Metrics <br>&emsp; + CloudWatch Logs <br>&emsp; + CloudWatch Alarms <br>&emsp; + Use case: monitoring EC2 and S3 | 19/09/2025 | 19/09/2025 | <https://000057.awsstudygroup.com/> |
| 7 | - **Practice 3 + Summary:** <br>&emsp; + Configure CloudWatch Alarm for EC2 CPU usage <br>&emsp; + Send notification via SNS <br>&emsp; + Summarize the workflow (S3 → IAM → CloudWatch) | 20-21/09/2025 | 21/09/2025 | <https://000057.awsstudygroup.com/> |


### Achievements in Week 3:

* **Amazon S3**:
  * Understood buckets, objects, and storage classes (Standard, IA, Glacier).  
  * Successfully created a bucket, uploaded/downloaded files, and configured Public/Private access.  
  * Learned how to apply lifecycle policies for automatic file management.  

* **IAM (Identity and Access Management)**:
  * Understood the difference between Users, Groups, and Roles.  
  * Learned how to write and attach policies to IAM Users.  
  * Created a new IAM User, assigned S3 ReadOnly/FullAccess, and verified login.  

* **CloudWatch**:
  * Understood the concepts of Metrics, Logs, and Alarms.  
  * Configured an alarm for EC2 CPU usage.  
  * Integrated with SNS to receive email notifications.  

* **End-of-week practical skills**:
  * Integrated the basic AWS services: S3 (storage) + IAM (access control) + CloudWatch (monitoring).  
  * Can independently set up and combine these services in an AWS practice environment.  
  * Built a foundational understanding of securing and monitoring AWS resources.  
