---
title: "Create Security Groups"
date: 2025-08-10
weight: 1
chapter: false
pre: "<b>3.1.</b>"
---

## 1. Introduction

**Security Group (SG)** is AWS’s virtual firewall that controls inbound and outbound traffic for EC2 instances.  
Security Groups operate at the **instance level** (different from NACL, which operates at the subnet level).

---

## 2. Create Security Group for Bastion Host

1. Go to **AWS Management Console** → **VPC** → **Security Groups**.
2. Click **Create security group**.
3. Configure:
   - **Security group name**: `SG_Bastion`
   - **VPC**: select VPC `redis-ha-vpc`
4. **Inbound rules**:
   - **Type**: SSH (TCP port 22)
   - **Source**: Administrator’s IP address (e.g., `203.x.x.x/32`)
   
   ![Inbound SSH](/images/2.prerequisite/sc-group-1.png)

5. **Outbound rules**:
   - By default, allow all outbound (`0.0.0.0/0`).

---

## 3. Create Security Group for Redis

1. Click **Create security group**.
2. Configure:
   - **Security group name**: `SG_Redis`
   - **VPC**: `redis-ha-vpc`
3. **Inbound rules**:
   - **Type**: Custom TCP
   - **Port range**: `6379` (Redis TLS)
   - **Source**: `SG_Bastion` and/or `SG_AppServer`
   
   ![Inbound Redis](/images/2.prerequisite/sc-group-2.png)

4. **Outbound rules**:
   - Keep default allow-all outbound, or restrict according to security requirements.

---

## 4. Result

After creation, you will have:

![SG List](/images/2.prerequisite/sc-group-3.png)

- `SG_Bastion`: Allows SSH from the admin IP to the Bastion Host.
- `SG_Redis`: Only allows Redis port access from Bastion Host or App Server.

---

## 💡 Technical Notes

- Only open **necessary ports**; avoid using `0.0.0.0/0` for sensitive ports like 22 or 6379.
- You can use **Security Group Reference** (e.g., `SG_Bastion`) instead of IP for easier management when scaling.
- Default outbound is **Allow All**, but it can be restricted for enhanced security.
- Security Groups are **stateful**: If inbound is allowed, the corresponding outbound response is automatically allowed.
