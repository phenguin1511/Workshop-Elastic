---
title : "Preparation Steps"
date : 2025-08-10
weight : 2
chapter : false
pre : "<b> 2. </b>"
---

{{% notice info %}}
You will need to prepare **1 Linux instance** in a **public subnet** and **1 Windows instance** in a **private subnet** to complete this hands-on lab.
{{% /notice %}}

To learn how to create an EC2 instance and a VPC with public/private subnets, refer to:
  - [Introduction to Amazon EC2](https://000004.awsstudygroup.com/en/)
  - [Working with Amazon VPC](https://000003.awsstudygroup.com/en/)

Additionally, to use **AWS Systems Manager** to manage your Windows instance and other instances, you must grant permissions via an **IAM Role**.

---

## 🔍 Summary of Required Components

1. **IAM Role**
   - Create an IAM Role with the `AmazonSSMManagedInstanceCore` policy.
   - Attach this Role to your EC2 instances so that Systems Manager can manage them.

2. **VPC**
   - Create a VPC with the CIDR block `10.0.0.0/16`.
   - Plan the IP range carefully to avoid conflicts with your existing network.

3. **Subnets**
   - **Public subnet** (e.g., `10.0.10.0/24`) for the Linux Bastion Host.  
   - **Private subnet** (e.g., `10.0.1.0/24`) for the Windows instance.  
   - Optionally create them in different Availability Zones for **high availability (HA)**.

4. **Internet Gateway (IGW)**
   - Create an IGW and attach it to the VPC.
   - Enable Internet access for the public subnet.

5. **Route Tables**
   - Public Route Table: add a route `0.0.0.0/0` pointing to the IGW.
   - Private Route Table: no route to the IGW; can only connect internally or via a NAT Gateway (if needed).

---

### Detailed Sections
- [Prepare VPC and EC2 Instances](2.1-createec2/)  
- [Create IAM Role](2.2-createiamrole/)
