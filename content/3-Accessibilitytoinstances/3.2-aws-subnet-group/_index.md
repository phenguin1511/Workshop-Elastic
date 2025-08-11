---
title: "Create ElastiCache Subnet Group"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>3.2.</b>"
---

## Create ElastiCache Subnet Group

### 1. Open the Subnet Groups page in ElastiCache
- Go to **AWS Management Console**.
- Navigate to **ElastiCache** → **Subnet Groups**.
- Select **Create**.

---

### 2. Enter Subnet Group information
- **Name**: `redis-ha-subnet-group`
- **Subnets**: Select **3 Private Subnets** in AZ1, AZ2, AZ3 that were created earlier.

![ElastiCache Subnet Group](/images/2.prerequisite/prerequisite-13.png)

---

**Notes**:  
- Only select **Private Subnets** to enhance security for the Redis Cluster.
- The Subnets must be in the same VPC created in the previous step.
