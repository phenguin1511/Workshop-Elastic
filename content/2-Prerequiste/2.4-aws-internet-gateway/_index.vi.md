---
title: "Tạo Internet Gateway"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>2.4 </b>"
---

## 1. Giới thiệu

**Internet Gateway (IGW)** là thành phần cho phép VPC kết nối ra Internet.  
IGW được gắn vào VPC và sử dụng trong các public subnet thông qua route table.

---

## 2. Các bước tạo Internet Gateway

1. Trong **VPC Console**, chọn **Internet Gateways** từ menu bên trái.

   ![Internet Gateways Menu](/images/2.prerequisite/igw-1.png)

2. Nhấn **Create internet gateway**.

   ![Create IGW](/images/2.prerequisite/igw-2.png)

3. Nhập thông tin:
   - **Name tag**: `redis-ha-igw`  
     > *Tên này giúp dễ dàng nhận diện IGW phục vụ cho VPC `redis-ha-vpc`.*

4. Nhấn **Create internet gateway** để khởi tạo.

5. Sau khi tạo, chọn **Attach to VPC** và gắn vào VPC `redis-ha-vpc`.

   ![Attach IGW](/images/2.prerequisite/igw-3.png)

---

## 3. Cấu hình Route Table để ra Internet

1. Mở **Route Tables** trong **VPC Console**.
2. Chọn route table gắn với **Public Subnet**.
3. Nhấn **Edit routes** → **Add route**:
   - **Destination**: `0.0.0.0/0`  
   - **Target**: Internet Gateway (`redis-ha-igw`)
4. Lưu lại thay đổi.

   ![Route IGW](/images/2.prerequisite/igw-4.png)

---

## 💡 Lưu ý kỹ thuật

- **0.0.0.0/0** nghĩa là cho phép truy cập ra Internet từ mọi địa chỉ IP.  
  ➜ Chỉ áp dụng cho **public subnet** chứa tài nguyên cần truy cập Internet (VD: Bastion Host).  
- Đảm bảo rằng **NACL** và **Security Group** được cấu hình hợp lý để hạn chế các port và IP truy cập.
- Một IGW có thể gắn tối đa **1 VPC**.
- Mỗi VPC chỉ cần **1 IGW**, có thể phục vụ nhiều subnet công khai.

