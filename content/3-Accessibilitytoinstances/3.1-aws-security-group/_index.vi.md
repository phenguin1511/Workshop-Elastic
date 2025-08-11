---
title: "Tạo Security Groups"
date: 2025-08-10
weight: 1
chapter: false
pre: "<b>3.1.</b>"
---

## 1. Giới thiệu

**Security Group (SG)** là firewall ảo của AWS, kiểm soát inbound và outbound traffic cho EC2 instance.  
Security Group hoạt động ở cấp **instance level** (khác với NACL hoạt động ở cấp subnet).

---

## 2. Tạo Security Group cho Bastion Host

1. Truy cập **AWS Management Console** → **VPC** → **Security Groups**.
2. Nhấn **Create security group**.
3. Cấu hình:
   - **Security group name**: `SG_Bastion`
   - **VPC**: chọn VPC `redis-ha-vpc`
4. **Inbound rules**:
   - **Type**: SSH (TCP port 22)
   - **Source**: Địa chỉ IP quản trị (VD: `203.x.x.x/32`)
   
   ![Inbound SSH](/images/2.prerequisite/sc-group-1.png)

5. **Outbound rules**:
   - Mặc định cho phép tất cả outbound (`0.0.0.0/0`).

---

## 3. Tạo Security Group cho Redis

1. Chọn **Create security group**.
2. Cấu hình:
   - **Security group name**: `SG_Redis`
   - **VPC**: `redis-ha-vpc`
3. **Inbound rules**:
   - **Type**: Custom TCP
   - **Port range**: `6379` (Redis TLS)
   - **Source**: `SG_Bastion` và/hoặc `SG_AppServer`
   
   ![Inbound Redis](/images/2.prerequisite/sc-group-2.png)

4. **Outbound rules**:
   - Giữ mặc định cho phép toàn bộ outbound hoặc giới hạn theo yêu cầu bảo mật.

---

## 4. Kết quả

Sau khi tạo xong, bạn sẽ có:

![SG List](/images/2.prerequisite/sc-group-3.png)

- `SG_Bastion`: Cho phép SSH từ IP quản trị vào Bastion Host.
- `SG_Redis`: Chỉ cho phép truy cập cổng Redis từ Bastion Host hoặc App Server.

---

## 💡 Lưu ý kỹ thuật

- Chỉ mở **cổng cần thiết**; tránh dùng `0.0.0.0/0` cho các cổng nhạy cảm như 22 hoặc 6379.
- Có thể dùng **Security Group Reference** (VD: `SG_Bastion`) thay vì IP để dễ quản lý khi scaling.
- Outbound mặc định là **Allow All**, nhưng có thể giới hạn để tăng bảo mật.
- Security Group **stateful**: Nếu inbound cho phép, thì outbound tự động cho phép trả lời.

