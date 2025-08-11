---
title: "Tạo Bastion Host"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>3.4.</b>"
---

## 1. Giới thiệu

**Bastion Host** là một EC2 instance đặt trong **public subnet** dùng làm điểm trung gian (jump host) để SSH/RDP vào các instance trong **private subnet**.  
Việc sử dụng Bastion Host giúp hạn chế việc mở cổng truy cập trực tiếp vào private subnet từ Internet.

---

## 2. Các bước tạo Bastion Host

1. Mở **AWS Management Console** → **EC2** → **Launch Instance**.
   
   ![Launch Instance](/images/2.prerequisite/bation-host-1.png)

2. **Cấu hình cơ bản**:
   - **Name**: `redis-bastion`
   - **OS**: Amazon Linux 2 (tương thích tốt với môi trường AWS)
   - **Instance type**: `t3.micro` (đủ cho nhiệm vụ SSH trung gian)

   ![Instance Config](/images/2.prerequisite/bation-host-2.png)

3. **Networking**:
   - **Subnet**: Chọn **Public Subnet** (VD: `public-subnet-bastion`)
   - **Auto-assign Public IP**: Bật **Enable** để có IP Public
   - **Security Group**: Chọn `SG_Bastion` (đã cấu hình cho phép SSH từ IP quản trị)

   ![Networking Config](/images/2.prerequisite/bation-host-3.png)

4. **Key pair**:
   - Tạo mới hoặc chọn key pair hiện có để SSH vào instance.

   ![Key Pair](/images/2.prerequisite/bation-host-4.png)

5. Nhấn **Launch Instance** để khởi tạo.

---

## 3. Sau khi tạo

- Instance `redis-bastion` sẽ xuất hiện trong danh sách **EC2 Instances** với trạng thái *running*.
- Dùng key pair đã chọn để SSH vào Bastion Host từ máy quản trị:
  ```bash
  ssh -i <your-key.pem> ec2-user@<Public-IP-Bastion>

Với Public-IP-Bastion là Ipv4 vừa tạo từ EC2 Instance

![Key Pair](/images/2.prerequisite/bation-host-5.png)

Khi chạy chúng ta được kết quả sau:

![Key Pair](/images/2.prerequisite/bation-host-6.png)

Để test xem đã kết nối được chưa hãy thử:
```bash
ping 8.8.8.8
crul http://google.com
```

## 4. Cài đặt Redis CLI
```bash
sudo dnf install -y tar gzip make gcc
curl -O http://download.redis.io/redis-stable.tar.gz
tar xzvf redis-stable.tar.gz
cd redis-stable
make
sudo make install

```
✅ Sau khi chạy xong, kiểm tra phiên bản redis-cli:

```bash
redis-cli --version
```
![Key Pair](/images/2.prerequisite/bation-host-7.png)

💡 Lưu ý kỹ thuật
Bảo mật SSH:
Chỉ cho phép IP quản trị truy cập port 22 (không dùng 0.0.0.0/0 trừ khi là môi trường lab).

Quản lý phiên kết nối:
Có thể sử dụng AWS Systems Manager Session Manager để thay thế SSH, giảm nhu cầu mở port 22 ra Internet.

Chi phí:
Bastion Host nên dùng instance loại nhỏ, và tắt khi không cần để tiết kiệm.

Logging:
Cân nhắc bật CloudWatch Logs hoặc dùng Session Manager để ghi lại lịch sử truy cập.