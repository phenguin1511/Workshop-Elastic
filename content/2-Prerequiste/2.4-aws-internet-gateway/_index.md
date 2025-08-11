---
title: "Create Internet Gateway"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>2.4 </b>"
---

## 1. Introduction

An **Internet Gateway (IGW)** is a component that enables a VPC to connect to the Internet.  
The IGW is attached to a VPC and used in public subnets through a route table.

---

## 2. Steps to Create an Internet Gateway

1. In the **VPC Console**, select **Internet Gateways** from the left-hand menu.

   ![Internet Gateways Menu](/images/2.prerequisite/igw-1.png)

2. Click **Create internet gateway**.

   ![Create IGW](/images/2.prerequisite/igw-2.png)

3. Enter the following details:
   - **Name tag**: `redis-ha-igw`  
     > *This name helps easily identify the IGW serving the `redis-ha-vpc`.*

4. Click **Create internet gateway** to proceed.

5. After creation, select **Attach to VPC** and attach it to the `redis-ha-vpc`.

   ![Attach IGW](/images/2.prerequisite/igw-3.png)

---

## 3. Configure Route Table for Internet Access

1. Open **Route Tables** in the **VPC Console**.
2. Select the route table associated with the **Public Subnet**.
3. Click **Edit routes** → **Add route**:
   - **Destination**: `0.0.0.0/0`  
   - **Target**: Internet Gateway (`redis-ha-igw`)
4. Save the changes.

   ![Route IGW](/images/2.prerequisite/igw-4.png)

---

## 💡 Technical Notes

- **0.0.0.0/0** means allowing Internet access from all IP addresses.  
  ➜ Only apply this to **public subnets** containing resources that require Internet access (e.g., Bastion Host).  
- Ensure **NACL** and **Security Group** rules are configured properly to limit allowed ports and source IPs.
- An IGW can be attached to **only 1 VPC**.
- Each VPC needs **only 1 IGW**, which can serve multiple public subnets.
