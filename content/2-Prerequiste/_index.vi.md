---
title : "Các bước chuẩn bị"
date :  2025-08-10 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

{{% notice info %}}
Bạn cần tạo sẵn **1 Linux instance** thuộc **public subnet** và **1 Windows instance** thuộc **private subnet** để thực hiện bài thực hành này.
{{% /notice %}}

Để tìm hiểu cách tạo EC2 instance và VPC với public/private subnet, bạn có thể tham khảo bài lab:
  - [Giới thiệu về Amazon EC2](https://000004.awsstudygroup.com/vi/)
  - [Làm việc với Amazon VPC](https://000003.awsstudygroup.com/vi/)

Ngoài ra, để sử dụng **AWS Systems Manager** quản lý Windows instance và các instance khác, chúng ta cần cấp quyền thông qua **IAM Role**.

---

## 🔍 Tóm tắt các thành phần cần chuẩn bị

1. **IAM Role**
   - Tạo IAM Role với quyền `AmazonSSMManagedInstanceCore`.
   - Gắn Role này vào các EC2 instance để Systems Manager có thể quản lý.

2. **VPC**
   - Tạo VPC với CIDR block `10.0.0.0/16`.
   - Quy hoạch IP tránh trùng với mạng nội bộ hiện có.

3. **Subnet**
   - **Public subnet** (VD: `10.0.10.0/24`) để đặt Linux Bastion Host.  
   - **Private subnet** (VD: `10.0.1.0/24`) để đặt Windows instance.  
   - Tạo ở các Availability Zone khác nhau nếu cần **HA**.

4. **Internet Gateway (IGW)**
   - Tạo IGW và gắn vào VPC.
   - Cho phép public subnet truy cập Internet.

5. **Route Table**
   - Public Route Table: có route `0.0.0.0/0` trỏ tới IGW.
   - Private Route Table: không có route ra IGW, chỉ kết nối nội bộ hoặc qua NAT Gateway (nếu cần).

---

### Nội dung chi tiết
- [Chuẩn bị VPC và EC2 Instance](2.1-createec2/)  
- [Tạo IAM Role](2.2-createiamrole/)
