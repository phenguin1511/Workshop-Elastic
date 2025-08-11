---
title: "Tạo ElastiCache Subnet Group"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>3.2.</b>"
---

## Tạo ElastiCache Subnet Group

### 1. Mở trang Subnet Groups trong ElastiCache
- Truy cập **AWS Management Console**.
- Điều hướng đến **ElastiCache** → **Subnet Groups**.
- Chọn **Create**.

---

### 2. Nhập thông tin Subnet Group
- **Name**: `redis-ha-subnet-group`
- **Subnets**: Chọn **3 Private Subnets** ở AZ1, AZ2, AZ3 đã tạo trước đó.

![ElastiCache Subnet Group](/images/2.prerequisite/prerequisite-13.png)

---

**Lưu ý**:  
- Chỉ chọn **Private Subnets** để tăng cường bảo mật cho Redis Cluster.
- Các Subnets phải nằm trong cùng một VPC đã tạo ở bước trước.
