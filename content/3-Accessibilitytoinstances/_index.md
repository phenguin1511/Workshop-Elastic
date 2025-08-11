---
title : "Deploy Redis Cluster"
date : 2025-08-10
weight : 3
chapter : false
pre : "<b>3.</b>"
---

## Steps to Deploy Redis Cluster on AWS

### 1. Security Group
- Create **`SG_Redis`**.
- Open **port 6379**.
- Only allow access from **`SG_Bastion`**.

---

### 2. Subnet Group
- Create **`redis-subnet-group`**.
- Include **private subnets** in multiple **Availability Zones** (*Multi-AZ*).

---

### 3. Redis Cluster
- **Engine**: Redis.
- **Cluster Mode**: Enabled.
- **Node type**: as needed (e.g., `cache.t3.micro`).
- **Shard**: ≥ 1.
- **Replica**: ≥ 1.
- **VPC**: `redis-ha-vpc`.
- **Subnet Group**: `redis-subnet-group`.
- **Security Group**: `SG_Redis`.

---

### 4. Bastion Host
- Linux EC2 in a **public subnet**.
- SG allows SSH from **admin IP**.
- Install **`redis-cli`** to connect to Redis via **private endpoint**.

---

### 5. Test Connection
From Bastion Host:
```bash
redis-cli -h <redis-endpoint> -p 6379
ping
set key1 "Hello Redis"
get key1
```
💡 Security & HA Notes
Do not expose Redis to the Internet.

Enable replication and Multi-AZ for higher fault tolerance.

Manage access using Security Group and configure AUTH if needed.

Monitor CloudWatch metrics and Redis slow log for performance tracking.