---
title: "Create Redis Cluster on ElastiCache"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>3.3.</b>"
---

## 1. Introduction

**Amazon ElastiCache for Redis** is AWS’s managed Redis service, enabling quick deployment of Redis clusters with automatic backup, scaling, and Multi-AZ support.  
In this section, we will create a **Redis Cluster** for the lab.

---

## 2. Open Redis OSS Caches

1. In the **AWS Management Console**, navigate to **Amazon ElastiCache**.
2. In the left menu, select **Redis OSS caches**. 

   ![Redis OSS caches](/images/2.prerequisite/prerequisite-14.png)

---

## 3. Start Creating a Cache

1. Select **Create cache**.  
   ![Create cache](/images/2.prerequisite/prerequisite-15.png)

---

## 4. Basic Configuration

1. **Configuration**: Select **Redis OSS**.
2. **Creation method**: Choose **Design Your Own Cache**.
3. **Cluster mode**: Select **Disabled** (single shard).  
   ![Cluster Mode](/images/2.prerequisite/prerequisite-16.png)

---

## 5. Cluster Information

- **Name**: `redis-cluster`  
- **Description**: *Optional, used to describe the purpose of the cluster*.

**Location**:  
- Select **AWS Cloud**  

  ![Cache Settings](/images/2.prerequisite/redis-cluster-1.png)

**Multi-AZ**: Choose **Enable** to ensure high availability.

---

## 6. Cache Settings

- Configure according to the illustration:  
  ![Cache Settings](/images/2.prerequisite/redis-cluster-1.png)

---

## 7. Advanced Settings

- Configure advanced options according to the guide images:  
  ![Cache Settings](/images/2.prerequisite/redis-cluster-2.png)  
  ![Cache Settings](/images/2.prerequisite/redis-cluster-3.png)  
  ![Cache Settings](/images/2.prerequisite/redis-cluster-4.png)

---

## 8. Completion

- After finishing the configuration, select **Create** to create the Redis Cluster.

---

## 💡 Technical Notes

- **Cluster Mode Disabled**: Simpler for lab environments or small workloads but does not support horizontal scaling.  
- **Multi-AZ**: Allows Redis to automatically failover when one AZ encounters an issue.  
- **Security Group**: Ensure port 6379 is open only to allowed sources (e.g., Bastion Host or App Server).  
- **Parameter Group**: Can be customized if special Redis configurations are required (e.g., persistence, eviction policy).
