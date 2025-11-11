---
title: "Worklog Week 2"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The following information is for reference only. Please **do not copy verbatim** into your official report, including this warning.
{{% /notice %}}


### Goals for Week 2:

* Connect and get to know members of the First Cloud Journey.  
* Understand the basics of AWS services, and how to use the Console & CLI.  

### Tasks to be completed this week:
| Day | Task | Start Date | Completion Date | Reference |
| --- | ---- | ---------- | ---------------- | ---------- |
| 2 | - Introduction to EC2 <br>&emsp; + EC2 concept <br>&emsp; + Instance Types (t2.micro, t3, m5...) <br>&emsp; + AMI (Amazon Machine Image) <br>&emsp; + Basic EBS | 08/09/2025 | 08/09/2025 | <https://000002.awsstudygroup.com/> |
| 3 | - **Practice 1:** <br>&emsp; + Launch an EC2 instance (Amazon Linux 2) <br>&emsp; + Understand basic configuration during setup <br>&emsp; + Learn about Key Pair for connection | 09/09/2025 | 09/09/2025 | <https://000002.awsstudygroup.com/> |
| 4 | - Security and Networking: <br>&emsp; + Security Groups (firewall for EC2) <br>&emsp; + Elastic IP (static IP) <br>&emsp; + Basic networking (default VPC, Subnet) | 10/09/2025 | 10/09/2025 | <https://000003.awsstudygroup.com/> |
| 5 | - **Practice 2:** <br>&emsp; + Connect to EC2 via SSH with key pair <br>&emsp; + Practice remote access and operations on Linux instance <br>&emsp; + Test Elastic IP assignment | 11/09/2025 | 11/09/2025 | <https://000003.awsstudygroup.com/> |
| 6 | - Storage management: <br>&emsp; + Attach additional EBS Volume to EC2 <br>&emsp; + Mount and check capacity <br>&emsp; + Learn about basic snapshots | 12/09/2025 | 12/09/2025 | <https://000004.awsstudygroup.com/> |
| 7 | - **Practice 3 + Summary:** <br>&emsp; + Launch another instance for practice <br>&emsp; + Attach / detach EBS volume <br>&emsp; + Review the full process (Launch → Connect → Elastic IP → EBS) | 13/09/2025 | 13/09/2025 | <https://000004.awsstudygroup.com/> |


### Achievements in Week 2:

* Gained solid understanding of **Amazon EC2** basics:  
  * Different instance types (t2.micro, t3, m5...) and their purposes.  
  * AMI (Amazon Machine Image) and how to choose an OS when launching a virtual machine.  
  * EBS (Elastic Block Store) and its role in storing data for EC2.  

* Successfully practiced **launching an EC2 instance** on AWS Console:  
  * Selected AMI (Amazon Linux 2).  
  * Chose a suitable instance type (Free Tier).  
  * Created and downloaded a Key Pair for connection.  

* Learned about **Security Groups** and understood how to configure firewall rules for an instance.  

* Practiced with **Elastic IP**: created, attached, and tested stability of a static IP compared to the default Public IP.  

* Became proficient in **SSH connection to EC2**:  
  * Used `.pem` key pair to connect.  
  * Checked system status and ran basic commands on the Linux instance.  

* Managed **storage with EBS**:  
  * Attached an additional EBS volume to an instance.  
  * Mounted, formatted, and verified available capacity.  
  * Understood what snapshots are and when to use them for backup.  

* **End-of-week practical skills**:  
  * Completed the full workflow: **Launch → Connect → Elastic IP → Attach EBS → Verify snapshot**.  
  * Able to repeat the steps independently.  

* Gained strong integration between theory and practice in managing EC2 and its related resources.  
