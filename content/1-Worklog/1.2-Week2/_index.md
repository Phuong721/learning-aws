---
title: "Worklog Week 2"
date: 2025-09-15
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Learn and practice AWS network setup using VPC, Subnet, Route Table, Internet Gateway, NAT Gateway, and security mechanisms.  
* Configure EC2 instances in subnets and test connectivity.  
* Set up Hybrid DNS with Route 53 Resolver.  
* Explore and deploy VPC Peering and AWS Transit Gateway.  

### Tasks to implement this week:
| Day | Task | Start Date | End Date | Reference |
| --- | ---- | ---------- | -------- | --------- |
| Mon | - Introduction to Amazon VPC and AWS Site-to-Site VPN (Module 02-Lab03-01) <br> - Subnets (Module 02-Lab03-01.1) <br> - Route Table (Module 02-Lab03-01.2) <br> - Internet Gateway (IGW) (Module 02-Lab03-01.3) <br> - NAT Gateway (Module 02-Lab03-01.4) | 15/09/2025 | 15/09/2025 | <https://000003.awsstudygroup.com/> |
| Tue | - Configure Security Group (Module 02-Lab03-02.1) <br> - Network ACLs (Module 02-Lab03-02.2) <br> - VPC Resource Map (Module 02-Lab03-02.3) | 16/09/2025 | 16/09/2025 | <https://000003.awsstudygroup.com/> |
| Wed | - Create VPC (Module 02-Lab03-03.1) <br> - Create Subnet (Module 02-Lab03-03.2) <br> - Create Internet Gateway (Module 02-Lab03-03.3) <br> - Create Route Table for Outbound Internet Routing via IGW (Module 02-Lab03-03.4) <br> - Create Security Groups (Module 02-Lab03-03.5) | 17/09/2025 | 17/09/2025 | <https://000010.awsstudygroup.com/> |
| Thu | - Create EC2 Instances in Subnets (Module 02-Lab03-04.1) <br> - Test connection (Module 02-Lab03-04.2) <br> - Create NAT Gateway (Module 02-Lab03-04.3) <br> - EC2 Instance Connect Endpoint (Module 02-Lab03-04.5) | 18/09/2025 | 18/09/2025 | <https://000010.awsstudygroup.com/> |
| Fri | - Set up Hybrid DNS with Route 53 Resolver (Module 02-Lab10-01) <br> - Generate Key Pair (Module 02-Lab10-02.1) <br> - Initialize CloudFormation Template (Module 02-Lab10-02.2) <br> - Configure Security Group (Module 02-Lab10-02.3) <br> - Connect to RDGW (Module 02-Lab10-03) | 19/09/2025 | 19/09/2025 | <https://000019.awsstudygroup.com/> |
| Sat | - DNS setup: Route 53 Outbound Endpoint (Module 02-Lab10-05.1) <br> - Create Resolver Rules (Module 02-Lab10-05.2) <br> - Create Inbound Endpoints (Module 02-Lab10-05.3) <br> - Test results (Module 02-Lab10-05.4) <br> - Clean up resources (Module 02-Lab10-06) | 20/09/2025 | 20/09/2025 | <https://000019.awsstudygroup.com/> |
| Sun | - VPC Peering setup: Introduction (Module 02-Lab19-01) <br> - Initialize CloudFormation Templates (Module 02-Lab19-02.1) <br> - Create Security Group (Module 02-Lab19-02.2) <br> - Create EC2 instance (Module 02-Lab19-02.3) <br> - Update Network ACLs (Module 02-Lab19-03) <br> - Create peering connection (Module 02-Lab19-04) <br> - Configure Route Tables (Module 02-Lab19-05) <br> - Enable Cross-Peer DNS (Module 02-Lab19-06) <br> - Clean up resources (Module 02-Lab19-07) <br> - AWS Transit Gateway setup: Introduction (Module 02-Lab20-01) <br> - Preparation steps (Module 02-Lab20-02) <br> - Create Transit Gateway (Module 02-Lab20-03) <br> - Create TGW Attachments (Module 02-Lab20-04) <br> - Create TGW Route Tables (Module 02-Lab20-05) <br> - Add TGW Routes to VPC Route Tables (Module 02-Lab20-06) <br> - Clean up resources (Module 02-Lab20-07) | 21/09/2025 | 21/09/2025 | <https://000020.awsstudygroup.com/> |

### Week 2 Results:

* AWS Networking:
  * Created and configured VPC, Subnet, Route Table, Internet Gateway, NAT Gateway, Security Groups.  
  * Deployed EC2 instances in subnets and verified connectivity.  
  * Configured EC2 Instance Connect Endpoint for easier access.

* Hybrid DNS:
  * Created Key Pairs and initialized CloudFormation Templates.  
  * Configured Security Groups and connected to RDGW.  
  * Created Route 53 Outbound/Inbound Endpoints, set up Resolver Rules, and verified results.  
  * Cleaned up DNS resources after testing.

* VPC Peering & Transit Gateway:
  * Established VPC Peering, configured Route Tables, and enabled Cross-Peer DNS.  
  * Created AWS Transit Gateway, attachments, route tables, and added routes to VPC route tables.  
  * Cleaned up resources to avoid unexpected costs.

* Self-assessment:
  * Gained hands-on experience with AWS networking, Hybrid DNS, VPC Peering, and Transit Gateway.  
  * Successfully deployed, tested, and cleaned up resources.  
  * Ready for the following weeks with more advanced knowledge.
