---
title : "Triển Khai Redis Cluster"
date : 2025-08-10
weight : 3
chapter : false
pre : "<b>3.</b>"
---

## Các bước triển khai Redis Cluster trên AWS

### 1. Security Group
- Tạo **`SG_Redis`**.
- Mở **cổng 6379**.
- Chỉ cho phép truy cập từ **`SG_Bastion`**.

---

### 2. Subnet Group
- Tạo **`redis-subnet-group`**.
- Bao gồm các **private subnet** ở nhiều **Availability Zone** (*Multi-AZ*).

---

### 3. Redis Cluster
- **Engine**: Redis.
- **Cluster Mode**: Enabled.
- **Node type**: tùy nhu cầu (VD: `cache.t3.micro`).
- **Shard**: ≥ 1.
- **Replica**: ≥ 1.
- **VPC**: `redis-ha-vpc`.
- **Subnet Group**: `redis-subnet-group`.
- **Security Group**: `SG_Redis`.

---

### 4. Bastion Host
- EC2 Linux trong **public subnet**.
- SG cho phép SSH từ **IP quản trị**.
- Cài đặt **`redis-cli`** để kết nối Redis qua **private endpoint**.

---

### 5. Kiểm tra kết nối
Từ Bastion Host:
```bash
redis-cli -h <redis-endpoint> -p 6379
ping
set key1 "Hello Redis"
get key1
```
💡 Lưu ý bảo mật & HA
Không public Redis ra Internet.

Bật replication và Multi-AZ để tăng khả năng chịu lỗi.

Quản lý truy cập bằng Security Group và cấu hình AUTH nếu cần.

Theo dõi CloudWatch metrics và Redis slow log để giám sát hiệu suất.