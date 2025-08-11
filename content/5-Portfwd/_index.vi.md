---
title: "Dọn dẹp tài nguyên"
date: 2025-08-10
weight: 5
chapter: false
pre: "<b>5.</b>"
---

## Dọn dẹp tài nguyên

Sau khi hoàn tất lab, cần xóa các tài nguyên đã tạo để tránh phát sinh chi phí.

---

### ✅ 1. Xóa EC2 Instance
1. Vào **EC2** → **Instances**.
2. Chọn instance **redis-bastion**.
3. Nhấn **Instance state** → **Terminate instance**.
4. Chọn **Yes, terminate** để xác nhận.

💡 *Lưu ý:*  
- Sau khi terminate, instance sẽ mất vĩnh viễn, không thể khôi phục.  
- Nếu dùng **Elastic IP** gán cho Bastion Host, nhớ release Elastic IP trong **EC2 → Elastic IPs** để tránh phí duy trì.

---

### ✅ 2. Xóa ElastiCache
1. Vào **ElastiCache** → **Redis OSS**.
2. Chọn cluster Redis đã tạo → **Delete**.
3. Xóa **Subnet Group** nếu không còn sử dụng:
   - Vào **ElastiCache** → **Subnet Groups** → chọn group → **Delete**.

💡 *Lưu ý:*  
- Việc xóa Redis cluster sẽ xóa toàn bộ dữ liệu trong đó.  
- Nếu đang bật **automatic backups**, cần xóa snapshot thủ công trong **ElastiCache → Snapshots**.

---

### ✅ 3. Xóa VPC và các thành phần liên quan
1. Vào **VPC** → chọn **VPC redis-ha-vpc**.
2. Nhấn **Actions** → **Delete VPC**.
3. Xác nhận xóa.

💡 *Lưu ý:*  
- Khi xóa VPC, các tài nguyên liên quan sẽ **tự động xóa** gồm:
  - Route Tables
  - Internet Gateway (IGW)
  - Subnets (Public & Private)
  - Security Groups trong VPC
- Nếu VPC đang gắn với **NAT Gateway**, cần xóa NAT Gateway trước (vì NAT GW tính phí theo giờ).

---

## 🔍 Checklist trước khi rời lab

- [ ] Đã terminate toàn bộ EC2 instances.
- [ ] Đã release Elastic IP (nếu có).
- [ ] Đã xóa Redis cluster và snapshot.
- [ ] Đã xóa Subnet Groups.
- [ ] Đã xóa NAT Gateway (nếu có).
- [ ] Đã xóa VPC và các tài nguyên liên quan.
