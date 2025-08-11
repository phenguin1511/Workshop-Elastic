---
title: "Tạo Redis Cluster trên ElastiCache"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>3.3.</b>"
---

## 1. Giới thiệu

**Amazon ElastiCache for Redis** là dịch vụ Redis managed của AWS, hỗ trợ triển khai nhanh chóng Redis cluster với khả năng tự động backup, scaling và Multi-AZ.  
Trong phần này, chúng ta sẽ tạo **Redis Cluster** để phục vụ cho bài lab.

---

## 2. Mở Redis OSS Caches

1. Trong **AWS Management Console**, điều hướng đến **Amazon ElastiCache**.
2. Ở menu bên trái, chọn **Redis OSS caches**. 

   ![Redis OSS caches](/images/2.prerequisite/prerequisite-14.png)

---

## 3. Bắt đầu tạo cache

1. Chọn **Create cache**.  
   ![Create cache](/images/2.prerequisite/prerequisite-15.png)

---

## 4. Cấu hình cơ bản

1. **Configuration**: Chọn **Redis OSS**.
2. **Creation method**: Chọn **Design Your Own Cache**.
3. **Cluster mode**: Chọn **Disabled** (single shard).  
   ![Cluster Mode](/images/2.prerequisite/prerequisite-16.png)

---

## 5. Thông tin Cluster

- **Name**: `redis-cluster`  
- **Description**: *Tùy chọn, dùng để mô tả mục đích cluster*.

**Location**:  
- Chọn **AWS Cloud**  

  ![Cache Settings](/images/2.prerequisite/redis-cluster-1.png)

**Multi-AZ**: Chọn **Enable** để đảm bảo tính sẵn sàng cao.

---

## 6. Cache Settings

- Cấu hình theo hình minh họa:  
  ![Cache Settings](/images/2.prerequisite/redis-cluster-1.png)

---

## 7. Advanced Settings

- Cấu hình nâng cao theo ảnh hướng dẫn:  
  ![Cache Settings](/images/2.prerequisite/redis-cluster-2.png)  
  ![Cache Settings](/images/2.prerequisite/redis-cluster-3.png)  
  ![Cache Settings](/images/2.prerequisite/redis-cluster-4.png)

---

## 8. Hoàn tất

- Sau khi cấu hình xong, chọn **Create** để tạo Redis Cluster.

---

## 💡 Lưu ý kỹ thuật

- **Cluster Mode Disabled**: đơn giản hơn cho môi trường lab hoặc workload nhỏ, nhưng không scale theo chiều ngang.  
- **Multi-AZ**: giúp Redis tự động failover khi một AZ gặp sự cố.  
- **Security Group**: cần mở port 6379 cho các nguồn được phép (VD: Bastion Host hoặc App Server).  
- **Parameter Group**: có thể tuỳ chỉnh thêm nếu cần cấu hình đặc biệt cho Redis (VD: persistence, eviction policy).

